#Socialshop Partener API V1.0.0
日期         |  版本       | 作者  |说明
------------|------------|-------|------
2018-07-16  |V1.0.0      |段振民  |  用户
2018-07-16  |V1.0.0      |李海燕  |  商品
2018-07-16  |V1.0.0      |徐东升  |  订单、支付
2018-07-16  |V1.0.0      |申士佳  |  邮件通知、追踪
## 1. 接口规则定义说明
### 1.1 功能描述
接口规则定义说明
### 1.2 请求地址
> 以下接口所有请求的地址均为： <br>
[${ctx } = https://xxx.xxx/](#)

### 1.3 返回格式:ResultDTO的json格式
```json  
{   “code”:1
	“msg:”success”
	“data”:object
}

``` 
### 1.4 code定义-与目标错误码保持一致
code说明       |code状态      
------------|-----------
成功状态                   |  1
未登录USER_NOT_LOGIN	      |401
验证失败BE_ATTACKED	      |99998
参数校验失败INVALID_PARAMS  |	20000
保存失败SAVE_FAILED	      |20001
获取图片失败GET_FILE_ERROR  |	20002
上传图片失败UPLOAD_ERROR	  |20003
删除失败DELETE_FAILED	  |20004
产品不存在PRODUCT_NOT_EXISTS	|20005
NOT_FRIEND	              |20006
MAKE_IMAGE_DIR_FAILED	  |20007
CREATE_IMAGE_FILE_FAILED  |20008
SAVE_SHORT_URL_FAILED	  |20009
LONGURL_NOT_EXISTS	      |20010
PRODTITLE	              |99997
未知错误UNKNOWN	          |99999
	|
用户类--	|
邮箱不能为空	        |30001
请输入正确的邮箱地址	|30002
邮箱已存在	        |10031
密码不能为空          |30004
请输入至少6位的密码    |30005
邀请人不存在          |30006


## 2. 用户模块
### 2.1.1 功能描述
获取邀请人头像和昵称（不需要登录）
### 2.1.2 请求说明
> 请求方式：POST<br>
请求URL ：[/${ctx}/user/partner/inviter/getUserInfo](#)

### 2.1.3 请求参数
参数名       |参数类型    |是否必填    |参数说明
------------|-----------|-----------|-------
userId   |string     |  是       |邀请人id
### 2.1.4 返回参数
参数名       |参数类型       |参数说明
------------|-----------   |-----------
userId      |string        |邀请人id
nickname    |string        |邀请人昵称
userImagePath   |string    |邀请人头像地址
code        |int           |返回码 1:成功  30006：邀请人不存在
msg         |string        |  
data       |               |
### 2.1.5 返回成功实例
```json  
{
	"code":1,
	"msg":"successful",
	"data":{
	"token":"3fc6ffd3627a4b5a80dcbed82cc6b545",
	"userId":"ss201807201546170001801",
	"friendCheck":false,
	"dlChannel":null,
	"imOauthUrl":null,
	"saas":null,
	"appId":null,
	"userImagePath":"",
	"nickName":"123456",
	"webToken":"8539e89f55c34f0fbe52510e5727c672",
	"buyerAppId":null,
	"sellerAppId":null,
	"domain":null,
	"step":null,
	"loginEmail":"123456@qq.com"
}
}
``` 

### 2.1.6 返回失败实例
```json  
{
	"code":30006,
	"msg":"邀请人不存在",
	"data":null
}
``` 

### 2.2.1 功能描述
保存被邀请人邮箱和密码（不需要登录）
### 2.2.2 请求说明
> 请求方式：POST<br>
请求URL ：[/${ctx}/user/partner/invitee/regPartner](#)

### 2.2.3 请求参数
参数名       |参数类型    |是否必填    |参数说明
------------|-----------|-----------|-------
preUserId   |string     |  是       |邀请人id
email       |string     |  是       |被邀请人邮箱
userPwd     |string     |  是       |被邀请人密码
locale      |string     |  是       |语言类型
### 2.2.4 返回参数
参数名       |参数类型       |参数说明
------------|-----------   |-----------
userId      |string       |被邀请人id
nickname    |string        |被邀请人昵称
userImagePath   |string    |被邀请人头像地址
code        |int           |返回码   1:成功  30001：邮箱不能为空   30002：请输入正确的邮箱地址  10031：邮箱已存在  30004：密码不能为空  30005：请输入至少6位的密码
msg         |string        |  
data       |               |
### 2.2.5 返回成功实例
```json  
{
	"code":1,
	"msg":"successful",
	"data":{
	"token":"3fc6ffd3627a4b5a80dcbed82cc6b545",
	"userId":"ss201807201546170001801",
	"friendCheck":false,
	"dlChannel":null,
	"imOauthUrl":null,
	"saas":null,
	"appId":null,
	"userImagePath":"",
	"nickName":"123456",
	"webToken":"8539e89f55c34f0fbe52510e5727c672",
	"buyerAppId":null,
	"sellerAppId":null,
	"domain":null,
	"step":null,
	"loginEmail":"123456@qq.com"
}
}
``` 

### 2.2.6 返回失败实例
```json  
{
	"code":10031,
	"msg":"邮箱地址已被注册，请输入新的邮箱地址注册",
	"data":null
}
``` 

## 2.3.1 功能描述
修改用户状态为激活
### 2.3.2 请求说明
> 请求方式：POST<br>
请求URL ：[/${ctx}/user/partner/invitee/activePartner](#)

### 2.3.3 请求参数
参数名       |参数类型    |是否必填    |参数说明
------------|-----------|-----------|-------
preUserId   |string     |  是       |邀请人id
email       |string     |  是       |被邀请人邮箱
userPwd     |string     |  是       |被邀请人密码
locale      |string     |  是       |语言类型
### 2.3.4 返回参数
参数名       |参数类型       |参数说明
------------|-----------   |-----------
code        |int           |返回码   1:成功  30002：请输入正确的邮箱地址   
msg         |string        |  
data       |               |
### 2.3.5 返回成功实例
```json  
{
	"code":1,
	"msg":"successful",
	"data":""
}
``` 

### 2.3.6 返回失败实例
```json  
{
	"code":30002,
	"msg":"请输入正确的邮箱地址",
	"data":""
}
```

## 3. 商品模块
### 3.1.1 功能描述
获取活动商品详情
### 3.1.2 请求说明
> 请求方式：POST<br>
请求URL ：[/${ctx}/product/partner/toppart/productdetail](#)

### 3.1.3 请求参数
参数名       |参数类型    |是否必填    |参数说明
------------|-----------|-----------|-------
channelType |string     |  是       |渠道：1表示h5
productId   |string     |  是       |商品id
(邀请人从域名汇总去)
### 3.1.4 返回参数
参数名       |参数类型       |参数说明
------------|-----------   |-----------
isActivityProduct   |Boolean        |是否活动商品
isShowActivityDoc   |Boolean        |是否展示活动文案，注：具体文案在前端处理，后端只处理是否展示
isShowPartenerRight |Boolean        |是否展示合伙人权益文案，注：具体文案在前端处理，后端只处理是否展示
userId              |String         |用户id
productPics         |List           |图片数组  
productName         |string         |产品名称
productPrice        |Double         |价格
currency            |String         |货币
currencyIcon        |String         |货币符号
skuInfos            |List           |产品规格说明
stock               |Long           |库存量
descriptions        |string         |详细描述
origProductPrice    |Double         |原始商品价格
origCurrency        |String         |原始币种
origCurrencyIcon    |String         |原始币种货币符号
### 3.1.5 返回成功实例
```json  
{
    "code": 1,
    "data": {
        "currency": "CNY",
        "currencyIcon": "￥",
        "exchangeRate": 6.74,
        "isActivityProduct": true,
        "isShowActivityDoc": true,
        "isShowPartenerRight": true,
        "origCurrency": "USD",
        "origCurrencyIcon": "$",
        "origProductPrice": 6,
        "productId": "100004416",
        "productName": "gakgnoih3igio2nonbogq",
        "productPics": [
            "http://nstatic.socialshops.com/image/socialshops/pic/17/af/0a/68bc4008768ba57229da5f2ec517af0a1_1024x768.jpg",
            "http://nstatic.socialshops.com/image/socialshops/pic/34/31/2d/64453b3e5cbb1e66c3f06e335d34312d1_1024x768.jpg",
            "http://nstatic.socialshops.com/image/socialshops/pic/fa/ef/dc/3bb54464da3190d05f56555822faefdc1_1024x768.jpg"
        ],
        "productPrice": 40.44,
        "skuInfos": [
            {
                "purchasePrice": 11,
                "skuAttrs": [
                    {
                        "attrId": "1000",
                        "attrName": "modelName",
                        "attrValId": "1000",
                        "attrValName": "XXXXXXX"
                    }
                ],
                "skuCode": "fafaeaf",
                "skuId": "100004416_1532142670",
                "skuPrice": 80.88
            },
            {
                "purchasePrice": 5,
                "skuAttrs": [
                    {
                        "attrId": "1001",
                        "attrName": "modelName",
                        "attrValId": "1001",
                        "attrValName": "XXX"
                    }
                ],
                "skuCode": "",
                "skuId": "100004416_1532142671",
                "skuPrice": 40.44
            }
        ],
        "userId": "ss201807121051510001001"
    },
    "msg": "1",
    "success": true
}


``` 

###3.1.6 返回失败实例
```json  
{
    "code":20005,
    "msg":"产品不存在",
    "data":"
}
``` 

## 4. 订单模块（不需要登录）
### 4.1.1 功能描述
增加订单地址
### 4.1.2 请求说明
> 请求方式：POST<br>
请求URL ：[/${ctx}/order/partner/address](#)

### 4.1.3 请求参数
参数名       |参数类型    |是否必填    |参数说明
------------|-----------|-----------|-------
userId      |String     |  是         |用户id
firstName   |string   |  是         |联系人姓名
lastName    |string   |  是         |联系人姓名
streetAdress1 |string |  是         |详细地址1
streetAdress2 |string |  否         |详细地址2
city        |string   |  是         |城市
countryCode |string   |  是         |国家code
stateCode   |string   |  是         |州/省会code
zipCode     |string   |  是         |邮编
mobileNum   |string   |  是         |电话号码
VATNum      |string   |  否         |税号
### 4.1.4 返回参数
参数名       |参数类型       |参数说明
------------|-----------   |-----------
code        |int        |返回码  1:成功  20001：firstName为空  20001：lastName为空  20003：详细地址为空  20004：国家为空  20005：城市、州为空  20006：邮编为空  20007：电话号码为空  20008：税号为空  20009：税号格式不正确
msg         |string        |  
data        |string        |地址id
### 4.1.5 返回成功实例
```json  
{
	"code": 1,
	"message": "",
	"data": ” "OR20170317224044000100148"
}

``` 

### 4.1.6 返回失败实例
```json  
{
	"code": 01007,
	"msg": "税号为空",
	"data": ""
}
``` 
### 4.2.1 功能描述
增加订单
### 4.2.2 请求说明
> 请求方式：POST<br>
请求URL ：[/${ctx}/order/partner/orderInfo](#)

### 4.2.3 请求参数
参数名       |参数类型    |是否必填    |参数说明
------------|-----------|-----------|-------
productId   |string     |  是         |产品id
inviterId   |string     |  是         |邀请人id
userId      |long       |  是         |注册人id
addressId   |long       |  是         |地址id
baseparm    |           |             |基础param
### 4.2.4 返回参数
参数名       |参数类型       |参数说明
------------|-----------   |-----------
code        |int           |返回码 1:成功  0:失败
msg         |string        |   
data        |string        |订单id
### 4.2.5 返回成功实例
```json 
 {
         	"code": 1,
         	"message": "",
         	"data": ” "OR20170317224044000100148"
 }
``` 

### 4.2.6 返回失败实例
```json  
{
	"code": 0,
	"msg": "添加订单失败",
	"data": ""
}
``` 



### 4.3.1 功能描述
获取国家列表
### 4.3.2 请求说明
> 请求方式：GET<br>
请求URL ：[/${ctx}/common/partner/country](#)

### 4.3.3 请求参数
   无
### 4.3.4 返回参数
参数名       |参数类型       |参数说明
------------|-----------   |-----------
code        |int           |返回码   1:成功 0:失败
msg         |string        |  
data        |              |
### 4.3.5 返回成功实例
```json  
{
	"code"：
	1,
	"msg": "",
	"data": [{
		"id": 1,
		"name": "美国"
	}, {
		"id": 2,
		"name": "日本"
	}]
}
``` 

### 4.3.6 返回失败实例
```json  
{
	"code": 0,
	"msg": "系统内部异常",
	"data": ""
}
```
``` 

## 5. 支付模块（不需要登录）
### 5.1.1 功能描述
创建支付订单
### 5.1.2 请求说明
> 请求方式：GET<br>
请求URL ：[/${ctx}/payment/partner/pay](#)

### 5.1.3 请求参数
参数名       |参数类型    |是否必填    |参数说明
------------|-----------|-----------|-------
orderNo     |string     |  是       |订单号
userId      |string     |  是       |用户id
baseParam   |           |           |基本参数
### 5.1.4 返回参数
参数名       |参数类型       |参数说明
------------|-----------   |-----------
code        |int           |返回码 1:成功 0:失败
msg         |string        |

### 5.1.5 返回成功实例
```json  
{
	"code": 1,
	"msg": "",
	"data": {
		"paymentId": "61281861V2211602PLHS5FLQ", //支付订单号
		"approvalUrl": "https://www.sandbox.paypal.com/cgi-bin/webscr ? cmd  = _express - checkout & token = EC - 25 G825504V216013P ", //支付页
		"state": "created" //支付订单状态
	}
}
``` 

### 5.1.6 返回失败实例
```json  
{
	"code": 0,
	"msg": "创建支付订单失败",
	"data": ""
}
``` 

### 5.2.1 功能描述
支付成功
### 5.2.2 请求说明
> 请求方式：GET<br>
请求URL ：[/${ctx}/payment/partner/pay/return](#)

### 5.2.3 请求参数
略
### 5.2.4 返回参数
无(redirect)

### 5.3.1 功能描述
支付失败
### 5.3.2 请求说明
> 请求方式：GET<br>
请求URL ：[/${ctx}/payment/partner/pay/cancel](#)

### 5.3.3 请求参数
略
### 5.3.4 返回参数
无(redirect)
## 6. 跟踪与邮件模块
### 6.1.1 功能描述
邮件通知
### 6.1.2 节点
节点：支付成功后同时给邀请人和被邀请人发送相关邮件
发送方式: KafkaTemplate

### 6.1.3 请求参数
参数名       |参数类型    |是否必填    |参数说明
------------|-----------|-----------|-------
locale      |String     |  是       |语言eg:zh_CN
params      |Map<String, String>    |  是       |参数格式
Params(1)   |string     |  是       |邀请人邮箱
Params(2)   |string     |  否       |被邀请人邮箱
Params(3)   |string     |  是       |用户注册的账号
### 6.1.4 返回参数
参数名       |参数类型       |参数说明
------------|-----------   |-----------
true/false  |boolean       |返回码  1:成功  


### 6.2.1 功能描述
追踪
### 6.2.2 请求说明
> 请求方式：POST<br>
请求URL ：[/${ctx}/ /track](#)

### 6.2.3 请求参数
参数名       |参数类型    |是否必填    |参数说明
------------|-----------|-----------|-------
pid      |String     |  是       |商品ID
sid      |string     |  是       |卖家id	
et       |string     |  是       |refer url
userId   |string     |  否       |买家 id
token    |string     |  是       |token id
href     |string     |  是       |事件名称
version  |string     |  是       |
locale   |string     |  是       |语言 eg: zh_CN
channelId |string    |  是       |
vid      |string     |  是       |访客id
email    |string     |  是       |
### 6.2.4 返回参数
参数名       |参数类型       |参数说明
------------|-----------   |-----------
true/false  |int           |              













