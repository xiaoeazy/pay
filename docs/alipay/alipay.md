# Alipay Api

> ###### 即时到账
>[https://doc.open.alipay.com/doc2/detail?treeId=62&articleId=103566&docType=1](https://doc.open.alipay.com/doc2/detail?treeId=62&articleId=103566&docType=1)
> ###### 即时到账交易接口
>[https://doc.open.alipay.com/doc2/detail.htm?spm=a219a.7629140.0.0.2IkYt2&treeId=62&articleId=104743&docType=1](https://doc.open.alipay.com/doc2/detail.htm?spm=a219a.7629140.0.0.2IkYt2&treeId=62&articleId=104743&docType=1)
> ##### 即时到账有密退款接口
[https://doc.open.alipay.com/doc2/detail.htm?spm=a219a.7629140.0.0.lnoshk&treeId=62&articleId=104744&docType=1](https://doc.open.alipay.com/doc2/detail.htm?spm=a219a.7629140.0.0.lnoshk&treeId=62&articleId=104744&docType=1)
> ##### 即时到账 － 签名与验签
>[https://doc.open.alipay.com/doc2/detail.htm?spm=a219a.7629140.0.0.5AyTO2&treeId=62&articleId=104741&docType=1](https://doc.open.alipay.com/doc2/detail.htm?spm=a219a.7629140.0.0.5AyTO2&treeId=62&articleId=104741&docType=1)
> ##### 移动支付
>[https://doc.open.alipay.com/doc2/detail?treeId=59&articleId=103563&docType=1](https://doc.open.alipay.com/doc2/detail?treeId=59&articleId=103563&docType=1)
> ##### 移动支付 － 签名机制
[https://doc.open.alipay.com/doc2/detail.htm?spm=a219a.7629140.0.0.x3fZFd&treeId=59&articleId=103927&docType=1](https://doc.open.alipay.com/doc2/detail.htm?spm=a219a.7629140.0.0.x3fZFd&treeId=59&articleId=103927&docType=1)

## 即时到账交易接口
### 支付宝即时到账交易接口快速通道
在PC端选择支付宝支付后，提交支付表单跳转到支付宝支付页面进行支付宝扫码支付或登录支付
#### 方法
建立支付宝即时到账(create_direct_pay_by_user)请求, 以表单HTML形式构造（默认）以POST方式提交表单

 **AlipaySubmit.buildRequest(String, String, String, String)**
#### 方法参数
- String outTradeNo 商户订单号
- String subject 商品名称
- String totalFee 付款金额（分）
- String body 商品描述

#### 返回
提交表单HTML文本
### 页面跳转同步通知
支付宝对商户的请求数据处理完成后，会将处理的结果数据通过系统程序控制客户端页面自动跳转的方式通知给商户网站。这些处理结果数据就是页面跳转同步通知参数。
#### 方法
可以使用com.boyuanitsm.pay.alipay.bean.SyncReturn接收同步通知参数， 收到通知后务必验证签名，以免造成资金损失
### 服务器异步通知
支付宝对商户的请求数据处理完成后，会将处理的结果数据通过服务器主动通知的方式通知给商户网站。这些处理结果数据就是服务器异步通知参数。
##### 方法
可以使用com.boyuanitsm.pay.alipay.bean.AyncNotify接收异步通知参数，收到通知后务必验证签名，以免造成资金损失

## 即时到账有密退款接口
### 支付宝即时到账批量退款有密接口快速通道
用户成功支付后，由于各种原因需要退款，提交表单到支付宝页面，需要输入支付密码才可以提交退款操作
#### 方法
建立即时到账批量退款有密接口(refund_fastpay_by_platform_pwd)请求, 以表单HTML形式构造（默认）以POST方式提交表单

**AlipaySubmit.buildRequest(String, String, String)**
#### 方法参数
- String batchNo 退款批次号
- String batchNum 退款笔数
- String detailData 退款详细数据

#### 返回
提交表单HTML文本

## 即时到账 － 签名与验签
### 签名
生成签名结果，一般情况下无需调用，已在AlipaySubmit.buildRequest内部调用

**AlipaySubmit.buildRequestMysign(Map<String, String>)**
#### 方法参数
- Map<String, String> sPara 要签名的Map

#### 返回
签名结果字符串
### 验签
验证消息是否是支付宝发出的合法消息，在同步通知和异步通知接收到支付宝消息时调用

**AlipayNotify.verifyRequest(Map requestParams)**
#### 方法参数
- Map requestParams request.getParameterMap()

#### 返回
验证结果

## 移动支付 － 签名机制
### 签名

#### 方法
支付接口待签名字符串生成

**AlipayMobilePaymentSign.pay(String, String, String)**
#### 方法参数
- String outTradeNo 商户订单号
- String subject 商品名称
- String totalFee 付款金额（分）

#### 返回
主要包含商户的订单信息，key=“value”形式，以&连接
