# text_blind_watermark

文本隐水印，用来把一段信息嵌入到一段明文中，使信息隐密不可见，并且旁人无法察觉到嵌入后明文的变化。

经测试，在这些场景下信息隐藏比较完美
- [x] MacBook 版本的 Chrome 浏览器，包括知乎网页版、微博网页版等。
- [x] 微信、钉钉。Mac/Iphone 版均可
- [x] 苹果备忘录
- [x] 用 Chrome 打开 github.com 上的代码文件和文本文件（但md文件不行）
- [x] 用复制/黏贴 (ctrl+c/v) 的方式在上述平台之间黏贴
- [x] 欢迎补充

不太行的
- Safari 浏览器



在线演示: [https://www.guofei.site/pictures_for_blog/app/text_watermark/v1.html](https://www.guofei.site/pictures_for_blog/app/text_watermark/v1.html)

视频展示：[https://www.bilibili.com/video/BV1m3411s7kT](https://www.bilibili.com/video/BV1m3411s7kT)

## 如何使用

安装

```bash
>pip install text_blind_watermark
```


### 把信息不可见地嵌入到文本中

```python
from text_blind_watermark import TextBlindWatermarkThin

# 密码
password = '20190808'
# 要嵌入的信息
watermark = 'github.com/guofei9987'
text_blind_wm = TextBlindWatermarkThin(password=password)

wm = text_blind_wm.embed(watermark=watermark)
# This is example，you can put wm everywhere
text_embed = '这句话中有盲' + wm + '水印，你能提取出来吗？'
print(text_embed)
```


### 从文本中提取不可见的信息

```python
text_blind_wm_new = TextBlindWatermarkThin(password=password)
wm_extract = text_blind_wm_new.extract(text_embed)
print('提取内容：', wm_extract)
```

>github.com/guofei9987

## 更稳定的版本
### 张三：把隐秘消息嵌入到另一段文本中

```python
from text_blind_watermark import TextBlindWatermark

watermark = "绝密：两点老地方见！"
text = "这句话中有盲水印，你能提取出来吗？" * 16
password = "20190808"

twm = TextBlindWatermark(password=password)
twm.read_wm(watermark=watermark)
twm.read_text(text=text)
text_embed = twm.embed()

print("打上盲水印之后:")
print(text_embed)
```

显示的明文可以粘贴到任何地方

*It uses AES to encrypt*

### 李四：拿到明文，解出暗文

```python
from text_blind_watermark import TextBlindWatermark
password = "20190808"

twm_new = TextBlindWatermark(password=password)
wm_extract = twm_new.extract(text_embed)
print("解出的盲水印：")
print(wm_extract)
```

