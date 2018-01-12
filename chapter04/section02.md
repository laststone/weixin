# 被动回复消息

当用户发送消息给公众号时（或某些特定的用户操作引发的事件推送时），会产生一个POST请求，开发者可以在响应包中返回特定XML结构，来对该消息进行响应（现支持回复文本、图片、图文、语音、视频、音乐）。严格来说，发送被动响应消息其实并不是一种接口，而是对微信服务器发过来消息的一次回复。

假如服务器无法保证在五秒内处理并回复，必须做出下述回复，这样微信服务器才不会对此作任何处理，并且不会发起重试（这种情况下，可以使用客服消息接口进行异步回复），否则，将出现严重的错误提示。详见下面说明：

1. （推荐方式）直接回复success
2. 直接回复空串（指字节长度为0的空字符串，而不是XML结构体中content字段的内容为空）

**一旦遇到以下情况，微信都会在公众号会话中，向用户下发系统提示“该公众号暂时无法提供服务，请稍后再试”：**

1. 开发者在5秒内未回复任何内容
2. 开发者回复了异常数据，比如JSON数据等

## 回复的消息类型

1. 文本消息
2. 图片消息
3. 语音消息
4. 视频消息
5. 音乐消息
6. 图文消息

## 回复文本消息

```XML
<xml>
<ToUserName><![CDATA[toUser]]></ToUserName>
<FromUserName><![CDATA[fromUser]]></FromUserName>
<CreateTime>12345678</CreateTime>
<MsgType><![CDATA[text]]></MsgType>
<Content><![CDATA[你好]]></Content>
</xml>
```
![回复文本消息](/images/reply_text_msg.png)