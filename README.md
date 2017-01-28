# HyperIdentity 开发文档（中文版）

## 服务授权

- 回调方式

通过跳转至 `https://HYPERIDENTITY_DOMAIN/web/?callback=CALLBACK_URL#auth` 并在 `CALLBACK_URL` 处接受回调参数 `client_token` ，可以实现对用户身份的简单确认。收到的 `client_token` 可以通过 `POST` 方式提交到 `https://HYPERIDENTITY_DOMAIN/identity/verify/verify_client_token` (格式: `client_token=SOME_TOKEN`) 来验证合法性，具体返回值请自行尝试。此方式无需用户在个人中心进行手动授权，但只能获取到用户的 ID 和用户名。

- 服务授权方式

首先，你需要在你自己的账户下创建服务，并保存好 `serviceId`（公开） 和 `secretKey`（保密） 。使用这种方式，你的账户必须绑定手机号码。用户在个人中心完成手动授权后，你将能够调用高级接口。

目前开放的高级接口有：

- 向用户事件流中加入事件: addEvent

调用方法：

向 `http://127.0.0.1:6522/services/api/add_event` POST 数据:

`serviceId=YOUR_SERVICE_ID&secretKey=YOUR_SECRET_KEY&eventTitle=TestEvent&eventDescription=TestDescription&userId=TARGET_USER_ID`
