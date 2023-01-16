# Markdownify for zhihu data

This repo clone from [python-markdownify](https://github.com/matthewwithanm/python-markdownify) and redevelop for zhihu data

## redevelop log

+ convert the tag ```<a>``` to ```[caption](src)``` 
+ convert the tag ```<img>``` to ```![image_caption](image_src)``` 
+ convert the equation to markdown version ``` $ example equation $ ```, in zhihu html data, the equation will convert equation to image and upload to ```https://www.zhihu.com/equation```.
+ convert code to markdown version 
+ fix the relative url to absolute url


## convert example


### convert math equation

code

```
data = '<img src="https://www.zhihu.com/equation?tex=%5Ctheta%5Cin+%5Cmathbb%7BR%7D" alt="\\theta\\in \\mathbb{R}" eeimg="1"/>'
print(md(data)[0])
```

result 

```
$ \theta\in \mathbb{R} $
```

$ \theta\in \mathbb{R} $

### convert code

raw_data

```html
<div class=\"highlight\"><pre><code class=\"language-ahk\">GBKCode := NumGet(GBKChar, 0, &#34;UInt&#34;) ; 这里获取到的编码将为“0xD0D6”。</code></pre></div>
```

code

```
from utils.markdownify_zhihu.markdownify import markdownify as md

data = "<div class=\"highlight\"><pre><code class=\"language-ahk\">GBKCode := NumGet(GBKChar, 0, &#34;UInt&#34;) ; 这里获取到的编码将为“0xD0D6”。</code></pre></div>"
print(md(data)[0])
```

result


``` 
GBKCode := NumGet(GBKChar, 0, "UInt") ; 这里获取到的编码将为“0xD0D6”。
```


### convert table

raw_data

```html
<table data-draft-node="block" data-draft-type="table" data-size="normal" data-row-style="normal"><tbody><tr><th>工具</th><th>Good for</th><th>Bad for</th></tr><tr><td>Evernote</td><td>raw资料收集，工作日志，随时随地有可能需要查看的内容。</td><td>‘严肃的’文字生产，存在隐私和机密（日记等）。</td></tr><tr><td>Leanote/Joplin</td><td>支持原生MD和LaTex，适合作为科研文字的生产平台。可以快速发布blog和生成目录，适合知识的归档。</td><td>不适合：需要检索和长期存放的知识。可靠性目前不如Evernote。</td></tr><tr><td>素签</td><td>对纯文字的记录，适合日记和文学创作（生活的、记录）。</td><td></td></tr><tr><td>LaTex</td><td>非常严肃的出版物（论文，pdf出版物）。</td><td>需要最终生成网页的知识（博文、wiki等），虽然有软件可以将LaTex转成网页，但是还需要将网页手工嵌入网站模板中。共享程度不如博客，阅读群体数量少。</td></tr><tr><td>WordPress/Hexo/Jeklly</td><td>三个主流博客系统，适合知识的输出和共享。</td><td>尚未形成结构和体系的知识。</td></tr><tr><td>Mkdocs (Wiki)</td><td>体系、系统的知识整理。可以通过任意终端查阅、搜索。</td><td>尚未形成结构和体系的知识。需要频繁添加、修改的知识。</td></tr><tr><td>OneNote</td><td>较为通用的知识，需要图片和文字共存，板式结构灵活。</td><td>缺乏对公式、程序代码的支持。</td></tr><tr><td>Tiddly Wiki</td><td>非线性、跳跃的知识管理和归档。</td><td>有明确层次和体系的知识</td></tr></tbody></table>
```

code 
```python
from utils.markdownify_zhihu.markdownify import markdownify as md
data = "<table data-draft-node=\"block\" data-draft-type=\"table\" data-size=\"normal\" data-row-style=\"normal\"><tbody><tr><th>工具</th><th>Good for</th><th>Bad for</th></tr><tr><td>Evernote</td><td>raw资料收集，工作日志，随时随地有可能需要查看的内容。</td><td>‘严肃的’文字生产，存在隐私和机密（日记等）。</td></tr><tr><td>Leanote/Joplin</td><td>支持原生MD和LaTex，适合作为科研文字的生产平台。可以快速发布blog和生成目录，适合知识的归档。</td><td>不适合：需要检索和长期存放的知识。可靠性目前不如Evernote。</td></tr><tr><td>素签</td><td>对纯文字的记录，适合日记和文学创作（生活的、记录）。</td><td></td></tr><tr><td>LaTex</td><td>非常严肃的出版物（论文，pdf出版物）。</td><td>需要最终生成网页的知识（博文、wiki等），虽然有软件可以将LaTex转成网页，但是还需要将网页手工嵌入网站模板中。共享程度不如博客，阅读群体数量少。</td></tr><tr><td>WordPress/Hexo/Jeklly</td><td>三个主流博客系统，适合知识的输出和共享。</td><td>尚未形成结构和体系的知识。</td></tr><tr><td>Mkdocs (Wiki)</td><td>体系、系统的知识整理。可以通过任意终端查阅、搜索。</td><td>尚未形成结构和体系的知识。需要频繁添加、修改的知识。</td></tr><tr><td>OneNote</td><td>较为通用的知识，需要图片和文字共存，板式结构灵活。</td><td>缺乏对公式、程序代码的支持。</td></tr><tr><td>Tiddly Wiki</td><td>非线性、跳跃的知识管理和归档。</td><td>有明确层次和体系的知识</td></tr></tbody></table>"
print(md(data)[0])
```


converted text

```
| 工具 | Good for | Bad for |
| --- | --- | --- |
| Evernote | raw资料收集，工作日志，随时随地有可能需要查看的内容。 | ‘严肃的’文字生产，存在隐私和机密（日记等）。 |
| Leanote/Joplin | 支持原生MD和LaTex，适合作为科研文字的生产平台。可以快速发布blog和生成目录，适合知识的归档。 | 不适合：需要检索和长期存放的知识。可靠性目前不如Evernote。 |
| 素签 | 对纯文字的记录，适合日记和文学创作（生活的、记录）。 |  |
| LaTex | 非常严肃的出版物（论文，pdf出版物）。 | 需要最终生成网页的知识（博文、wiki等），虽然有软件可以将LaTex转成网页，但是还需要将网页手工嵌入网站模板中。共享程度不如博客，阅读群体数量少。 |
| WordPress/Hexo/Jeklly | 三个主流博客系统，适合知识的输出和共享。 | 尚未形成结构和体系的知识。 |
| Mkdocs (Wiki) | 体系、系统的知识整理。可以通过任意终端查阅、搜索。 | 尚未形成结构和体系的知识。需要频繁添加、修改的知识。 |
| OneNote | 较为通用的知识，需要图片和文字共存，板式结构灵活。 | 缺乏对公式、程序代码的支持。 |
| Tiddly Wiki | 非线性、跳跃的知识管理和归档。 | 有明确层次和体系的知识 |
```

markdown 

| 工具 | Good for | Bad for |
| --- | --- | --- |
| Evernote | raw资料收集，工作日志，随时随地有可能需要查看的内容。 | ‘严肃的’文字生产，存在隐私和机密（日记等）。 |
| Leanote/Joplin | 支持原生MD和LaTex，适合作为科研文字的生产平台。可以快速发布blog和生成目录，适合知识的归档。 | 不适合：需要检索和长期存放的知识。可靠性目前不如Evernote。 |
| 素签 | 对纯文字的记录，适合日记和文学创作（生活的、记录）。 |  |
| LaTex | 非常严肃的出版物（论文，pdf出版物）。 | 需要最终生成网页的知识（博文、wiki等），虽然有软件可以将LaTex转成网页，但是还需要将网页手工嵌入网站模板中。共享程度不如博客，阅读群体数量少。 |
| WordPress/Hexo/Jeklly | 三个主流博客系统，适合知识的输出和共享。 | 尚未形成结构和体系的知识。 |
| Mkdocs (Wiki) | 体系、系统的知识整理。可以通过任意终端查阅、搜索。 | 尚未形成结构和体系的知识。需要频繁添加、修改的知识。 |
| OneNote | 较为通用的知识，需要图片和文字共存，板式结构灵活。 | 缺乏对公式、程序代码的支持。 |
| Tiddly Wiki | 非线性、跳跃的知识管理和归档。 | 有明确层次和体系的知识 |


### convert image

### convert title
