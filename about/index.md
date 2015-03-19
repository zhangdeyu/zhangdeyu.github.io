---
title: 关于
layout: page
comments: no
---

{{ site.about }}
>####个人简介：
>动物医学专业大四学生党一枚，大一在机缘巧合下开始接触`PHP`，后来开始学习 `JavaScript`、`HTML`、`CSS` ，目前正在努力学习各种知识中。
>####掌握技能：
> - `PHP`
- `HTML`
- `CSS`
- `JavaScript`
- `Java`
>
>####项目开发经验
> - [我们网](http://www.ewe.com.cn)
> - [人文华农](http://c.ewe.com.cn)
> - [湖北华南环保科技](http://www.huanbao8828.com)
> - [光谷医院](http://www.whovh.com)
> - [外卖口袋](http://www.waimaikoudai.com)

----

###联系方式：

{% if site.qq %}
ＱＱ：[{{ site.qq }}](tencent://message/?uin={{ site.qq }})
{% endif %}
网站：[{{ site.name }}]({{ site.url }})

邮箱：[{{ site.email }}](mailto:{{ site.email }})

GitHub : [http://github.com/{{ site.github }}](http://github.com/{{ site.github }})

----

{% if site.weibo %}
[![新浪微博](http://service.t.sina.com.cn/widget/qmd/{{ site.weibo }}/f78fbcd2/1.png)](http://weibo.com/u/{{ site.weibo }})
{% endif %}
