import requests
import parsel
import os
# 存储需要爬取的网站
url = 'https://www.xbiquge.la/'
# 进行爬取
response = requests.get(url=url)
# 编码格式
response.encoding = 'utf-8'
# 转成text类型
selector = parsel.Selector(response.text)
#获取前四本标题
novel_name = selector.css('#hotcontent > div.l > div > dl > dt > a::text').getall()
a = 1
# 循环遍历
for i in novel_name:
    print("第%d本:"%(a))
    print(i)
    a = a+1
a = int(input("请问你要获第几本小说"))
# 根据收到的命令进行相应的网址以及书名的获取
li = selector.css('#hotcontent > div.l > div:nth-child(%d) > dl > dt > a::attr(href)'%(a)).get()
b = selector.css('#hotcontent > div.l > div:nth-child(%d) > dl > dt > a::text'%(a)).get()
# 判断是否存在该文件夹
if not os.path.exists(b):
    # 根据书名创建文件夹
    os.makedirs(b)
# 进行爬取
one = requests.get(url=li)
# 编码格式
one.encoding = 'utf-8'
# 转成text类型
selector = parsel.Selector(one.text)
# 获取该书中全部章节的链接
name = selector.css('#list > dl > dd > a::attr(href)').getall()
for i in name:
    two = requests.get(url='https://www.xbiquge.la'+i)
    two.encoding = 'utf-8'
    twos = parsel.Selector(two.text)
    # 章节名字
    title = twos.css('#wrapper > div.content_read > div > div.bookname > h1::text').get()
    #章节内容
    content_list = twos.css('#content::text').getall()
    # 去除网页编码
    content = '\n'.join(content_list)
    # 机械打印如电脑文本文件中
    with open(b+'\\'+title + '.txt', mode="a", encoding="utf-8") as f:
        f.write(title)
        f.write('\n')
        f.write(content)
        f.write('\n')
    # 每章结束后打印名字
    print(title)
