---
layout: post
title: Google Dataset云台操作初体验
categories:
- blog
tags:
- Google Dataset
- 数据分析
- 云服务
- python
---

## 由于工作上的偶然，想要找一些关于SEP专利的数据，想用之前用过的线上数据库搜索引擎——Google Dataset来进行检索，后发现Google开始提供线上数据库的开源分享与分析服务，不嫖白不嫖，于是我期望能通过python调用这个数据库分享的api接口进行数据分析与处理。

### Ⅰ 介绍下Google Dataset搜索🔍工具

写整篇文章代理都不能断，贫穷如我选择免费的节点分享，顺便给大家分享个每日分享全球机场节点的[tg订阅](https://t.me/ssrList)叭。

Google Dataset顾名思义就是Google出品的数据库检索工具，链接为：[https://datasetsearch.research.google.com/](<https://datasetsearch.research.google.com/>)。几年前我在看一篇讲破解指纹识别的文章时，想着自己能不能从网上找点数据训练（虽然后面并没有实际操作，哭了我的机器学习之路什么时候才能开启啊），于是在搜索的过程中发现了这个网站。

![fingerprint](http://qemn845gn.bkt.clouddn.com/dataset.png)

然后在我搜索SEP专利数据时，我发现Google自建了一个共享数据库的应用<strong>BigQuery</strong>。

### Ⅱ 介绍下Google云应用服务

放一个BigQuery的操作手册：[🔗链接](<https://cloud.google.com/bigquery/docs/reference/libraries#command-line>)。

也是在之前看一个python爬取并分析股票数据的文章时，发现作者在处理excel文件时用的Google Cloud里的免费服务，然后我就第一次接触了这个。在发现上述的Google Dataset里的某些数据库可以通过Bigquery接口调用后，我打开了这个[云服务的网站](<https://console.cloud.google.com/apis/api/bigquery.googleapis.com/>)。

### Ⅲ 正题开始

1. 首先的首先，你得拥有一个Google账号（滑稽

2. 开通相应的Google云服务并生成密钥

   进入<https://console.cloud.google.com/apis/credentials/serviceaccountkey>这个页面，service account处选择new service account，name自定，role选择project-->owner，key type不变就选默认的json文件就行，点击生成。

3. 云台端操作

   以后访问时输入：https://console.cloud.google.com/bigquery?project=你的项目名称

![fingerprint](http://qemn845gn.bkt.clouddn.com/bigq.JPG)

4. 本地系统命令行操作（以win10的powershell为例）

   ```powershell
   pip install --upgrade google-cloud-bigquery
   $env:GOOGLE_APPLICATION_CREDENTIALS="存放目录\my-key.json"
   set GOOGLE_APPLICATION_CREDENTIALS=[PATH]
   ```

5. python脚本撰写

   ```python
   from google.cloud import bigquery
   
   def get_info():
       
       client = bigquery.Client()
       query = """
               SELECT *
               FROM `patents-public-data.dsep.disclosures_13`
               WHERE regexp_contains(tc_name,"Information technology")
               AND date > 2010
       """
       query_job = client.query(query)  # Make an API request.
       return query_job
   
   def show(info):
       print("The query data:")
       for row in info:
           # Row values can be accessed by field name or index.
           print("name={}, count={}".format(row[0], row["total_num"]))
   
   def main():
       info = get_info()
       show(info)
       
   main()
   
   ```


