---
title: 通过Python爬取链家所有房源和小区
top: false
cover: false
toc: true
mathjax: true
date: 2019-03-17 21:36:52
password:
summary:
tags: [Python,Python爬虫]
categories: Python爬虫
---

# 通过Python爬取链家所有房源和小区信息
链家房源爬虫，基于scrapy框架，数据存储在MongoDB

由于链家的限制房源列表最多显示1000页，3000条数据，所以这里通过小区信息爬取所有房源。

```
# -*- coding: utf-8 -*-
import scrapy
from scrapy import Selector
import json
import re

from house_spider.items import LianjiaVillageItem, LianjiaHouseItem

class LianjiaSpider(scrapy.Spider):
    name = 'lianjia'
    allowed_domains = ['cq.lianjia.com']
    start_urls = ['cq.lianjia.com']

    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.base_url = 'https://cq.lianjia.com'

    def start_requests(self):
        request_url = 'https://cq.lianjia.com/xiaoqu/'
        yield scrapy.Request(url=request_url, callback=self.parse_district_links)

    def parse_district_links(self, response):
        """提取地区链接"""
        sel = Selector(response)
        links = sel.css("div[data-role='ershoufang'] div:first-child a::attr(href)").extract()
        for link in links:
            url = self.base_url + link
            yield scrapy.Request(url=url, callback=self.parse_bizcircle_links)

    def parse_bizcircle_links(self, response):
        """提取商圈链接"""
        sel = Selector(response)
        links = sel.css("div[data-role='ershoufang'] div:nth-child(2) a::attr(href)").extract()
        for link in links:
            url = self.base_url + link
            yield scrapy.Request(url=url, callback=self.parse_village_list, meta={"ref": url})

    def parse_village_list(self, response):
        """提取小区链接"""
        sel = Selector(response)
        links = sel.css(".listContent .xiaoquListItem .img::attr(href)").extract()
        for link in links:
            yield scrapy.Request(url=link, callback=self.parse_village_detail)

        # page
        page_data = sel.css(".house-lst-page-box::attr(page-data)").extract_first()
        page_data = json.loads(page_data)
        if page_data['curPage'] < page_data['totalPage']:
            url = response.meta["ref"] + 'pg' + str(page_data['curPage'] + 1)
            yield scrapy.Request(url=url, callback=self.parse_village_list, meta=response.meta)

    def parse_village_detail(self, response):
        """提取小区详情"""
        village_url = response.url
        sel = Selector(response)
        zone = sel.css('.xiaoquDetailbreadCrumbs .l-txt a::text').extract()
        latitude = 0
        longitude = 0
        try:
            html = response.body.decode().replace('\r', '')
            local = html[html.find('resblockPosition:'):html.find('resblockName') - 1]
            m = re.search('(\d.*\d),(\d.*\d)', local)
            longitude = m.group(1)
            latitude = m.group(2)
        except Exception:
            pass

        item = LianjiaVillageItem()
        item['id'] = village_url.replace(self.base_url + '/xiaoqu/', '').replace('/', '')
        item['name'] = sel.css('.detailHeader .detailTitle::text').extract_first()
        item['address'] = sel.css('.detailHeader .detailDesc::text').extract_first()
        item['latitude'] = latitude
        item['longitude'] = longitude
        item['zone'] = ','.join(zone)
        item['year'] = sel.css('.xiaoquInfo .xiaoquInfoItem:nth-child(1) .xiaoquInfoContent::text').extract_first()
        item['build_type'] = sel.css('.xiaoquInfo .xiaoquInfoItem:nth-child(2) .xiaoquInfoContent::text').extract_first()
        item['property_costs'] = sel.css('.xiaoquInfo .xiaoquInfoItem:nth-child(3) .xiaoquInfoContent::text').extract_first()
        item['property_company'] = sel.css('.xiaoquInfo .xiaoquInfoItem:nth-child(4) .xiaoquInfoContent::text').extract_first()
        item['developers'] = sel.css('.xiaoquInfo .xiaoquInfoItem:nth-child(5) .xiaoquInfoContent::text').extract_first()
        item['buildings'] = sel.css('.xiaoquInfo .xiaoquInfoItem:nth-child(6) .xiaoquInfoContent::text').extract_first()
        item['total_house'] = sel.css('.xiaoquInfo .xiaoquInfoItem:nth-child(7) .xiaoquInfoContent::text').extract_first()

        print(item['name'])
        yield item

        # 小区房源 https://cq.lianjia.com/ershoufang/c3620038190566370/
        url = self.base_url + "/ershoufang/c" + item['id'] + "/"
        yield scrapy.Request(url=url, callback=self.parse_house_list, meta={"ref": url})

    def parse_house_list(self, response):
        """提取房源链接"""
        sel = Selector(response)
        # 链家有时小区查询不到数据
        total = sel.css('.resultDes .total span::text').extract_first()
        total = int(total)
        if total > 0:
            # 提取房源链接
            links = sel.css(".sellListContent li .info .title a::attr(href)").extract()
            for link in links:
                yield scrapy.Request(url=link, callback=self.parse_house_detail)
            # 链接分页
            page_data = sel.css(".house-lst-page-box::attr(page-data)").extract_first()
            page_data = json.loads(page_data)
            if page_data['curPage'] == 1 and page_data['totalPage'] > 1:
                price = response.url.replace(self.base_url + '/ershoufang/', '')
                for x in range(2, page_data['totalPage'] + 1, 1):
                    url = self.base_url + '/ershoufang/' + 'pg' + str(x) + price
                    yield scrapy.Request(url=url, callback=self.parse_house_list)

    def parse_house_detail(self, response):
        """提取房源信息"""
        sel = Selector(response)

        item = LianjiaHouseItem()
        item['房屋Id'] = response.url.replace(self.base_url + '/ershoufang/', '').replace('.html', '')
        item['标题'] = sel.css('.title-wrapper .title .main::text').extract_first()
        item['售价'] = sel.css('.overview .content .price .total::text').extract_first()
        item['小区'] = sel.css('.overview .content .aroundInfo .communityName a.info::text').extract_first()
        item['小区ID'] = sel.css('.overview .content .aroundInfo .communityName a.info::attr(href)').extract_first().replace('/xiaoqu/', '').replace('/', '')
        item['房屋户型'] = sel.css('#introduction .base .content ul li:nth-child(1)::text').extract_first()
        item['所在楼层'] = sel.css('#introduction .base .content ul li:nth-child(2)::text').extract_first()
        item['建筑面积'] = sel.css('#introduction .base .content ul li:nth-child(3)::text').extract_first()
        item['户型结构'] = sel.css('#introduction .base .content ul li:nth-child(4)::text').extract_first()
        item['套内面积'] = sel.css('#introduction .base .content ul li:nth-child(5)::text').extract_first()
        item['建筑类型'] = sel.css('#introduction .base .content ul li:nth-child(6)::text').extract_first()
        item['房屋朝向'] = sel.css('#introduction .base .content ul li:nth-child(7)::text').extract_first()
        item['建筑结构'] = sel.css('#introduction .base .content ul li:nth-child(8)::text').extract_first()
        item['装修情况'] = sel.css('#introduction .base .content ul li:nth-child(9)::text').extract_first()
        item['梯户比例'] = sel.css('#introduction .base .content ul li:nth-child(10)::text').extract_first()
        item['配备电梯'] = sel.css('#introduction .base .content ul li:nth-child(11)::text').extract_first()
        item['产权年限'] = sel.css('#introduction .base .content ul li:nth-child(12)::text').extract_first()
        item['挂牌时间'] = sel.css('#introduction .transaction .content ul li:nth-child(1) span:nth-child(2)::text').extract_first()
        item['交易权属'] = sel.css('#introduction .transaction .content ul li:nth-child(2) span:nth-child(2)::text').extract_first()
        item['上次交易'] = sel.css('#introduction .transaction .content ul li:nth-child(3) span:nth-child(2)::text').extract_first()
        item['房屋用途'] = sel.css('#introduction .transaction .content ul li:nth-child(4) span:nth-child(2)::text').extract_first()
        item['房屋年限'] = sel.css('#introduction .transaction .content ul li:nth-child(5) span:nth-child(2)::text').extract_first()
        item['产权所属'] = sel.css('#introduction .transaction .content ul li:nth-child(6) span:nth-child(2)::text').extract_first()
        item['抵押信息'] = sel.css('#introduction .transaction .content ul li:nth-child(7) span:nth-child(2)::attr(title)').extract_first()
        item['房本备件'] = sel.css('#introduction .transaction .content ul li:nth-child(8) span:nth-child(2)::text').extract_first()

        yield item
        
```
![](https://note.youdao.com/yws/public/resource/b668ad7e2986aeae14431f59531ace89/xmlnote/B0C655564F174592844C2DFE897C7265/3118)
![](https://note.youdao.com/yws/public/resource/b668ad7e2986aeae14431f59531ace89/xmlnote/7E5B19AFBC1A4B658B00A1873BEEBD0A/3120)