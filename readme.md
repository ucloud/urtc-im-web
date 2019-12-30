# im-sdk-web

* [Client 类](#client)
* [version 属性](#version)
* [setServers 方法](#setservers)

---
<a name='client'></a>
## 安装
```
npm install urtc-im 
```

or

```
<script src= "http://urtcsdk.cn-bj.ufileos.com/UCloudIMSdk_web.js"></script>
```

## 一、Client 类

Client 类包含以下方法：

* [构建函数 - 创建客户端](#client-constructor)
* [joinRoom 方法 - 加入房间](#client-joinroom)
* [close 方法 - 离开房间](#client-close)
* [sendMsg 方法 - 发消息](#client-sendMsg)
* [sendGlobal 方法 - 发广播](#client-sendglobal)
* [authCall 方法 - 设置房间连麦权限](#client-authcall)
* [getUser 方法 - 获取当前用户信息](#client-getuser)
* [getAdminUsers 方法 - 获取 admin 列表](#client-adminusers)
* [getDefaultUsers 方法 - 获取 default 列表](#client-defaultusers)
* [getWhiteboard 方法 - 获取白板 uuid 以及 token](#client-getwhiteboard)
* [on 方法 - 绑定事件处理函数](#client-on)
* [off 方法 - 解绑事件处理函数](#client-off)
* [sendNotice  方法 - 发送公告](#client-sendnotice)
* [sendCustomMsg  方法 - 发送自定义消息](#client-sendcustommsg)
* [sendCustomPeerMsg  方法 - 发送点对点自定义消息](#client-sendcustommsg)
* [applyCall  方法 - 发起连麦请求](#client-applycall)
* [replyCall  方法 - 应答连麦请求](#client-replycall)
* [getRoomInfo  方法 - 房间信息](#client-getRoomInfo)
<!-- * [getUsers 方法 - 获取房间全部用户 (admin 以及 default)](#client-getusers) -->

<a name="client-constructor"></a>

### 1. 构建函数

用于创建一个 URTC Client 对象，示例代码：

```
import urtc_im from '../@sdk';
let {Client,setServers } = urtc_im;
new Client(AppId);
```

#### 参数说明

- AppId: string 类型，必传，可从 UCloud 控制台查看

<a name="client-joinroom"></a>

### 2.joinRoom 方法

加入房间，示例代码：

```
client.joinRoom(RoomId, UserId, UserType, UserName, onSuccess, onFailure)
```

#### 参数说明

- RoomId: string 类型，必传，可从 UCloud 控制台查看
- UserId: string 类型，必传，用户 ID
- UserType: string 类型 (admin 或者 default)，必传，用户角色  
- onSuccess: function 类型，选传，方法调用成功时执行的回调函数，函数说明如下
```
function onSuccess(data) {}
```
- onFailure: 选传，函数类型，方法调用失败时执行的回调函数。
```
function(Err) {}
```
Err 为错误信息

<a name ="client-close"></a>

### 3 close 方法 
离开房间，关闭 IM，示例代码：
```
client.sendMsg(
    '测试',
    function(data){
        console.log(client.getUser()),console.log(data)
    },
    function(err){
        console.log(err)
    }
)
```

<a name ="client-sendmsg"></a>

### 4 sendMsg 方法
发送聊天消息，示例代码：
```
client.sendMsg(
    msg,
    onSuccess,
    onError,
)
```
#### 参数说明

- msg: string 类型，必传，聊天文字
- onSuccess: function 类型，选传，方法调用成功时执行的回调函数，函数说明如下
```
function onSuccess(data) {}
```
- onFailure: 选传，函数类型，方法调用失败时执行的回调函数。

<a name ="client-sendglobal"></a>

### 5 sendGlobal 方法
推送广播，示例代码：

#### 参数说明
参考 [sendMsg](#client-sendmsg)

<a name ="client-authcall"></a>

### 6 sendGlobal 方法
推送广播，示例代码：
```
client.authCall(
    flag,
    onSuccess,
    onError,
)
```
#### 参数说明
- flag,  string 类型 （open or close）, 开始 or 关闭房间连麦的权限，管理员角色设置
- onSuccess,onError 参考 [sendMsg](#client-sendmsg)

<a name ="client-authcall"></a>

### 6 authCall 方法
推送广播，示例代码：
```
client.authCall(
    flag,
    onSuccess,
    onError,
)
```
#### 参数说明
- flag,  string 类型 （open or close）, 开始 or 关闭房间连麦的权限，管理员角色设置
- onSuccess,onError 参考 [sendMsg](#client-sendmsg)

<a name ="client-getuser"></a>

### 7 getUser 方法
当前用户信息，示例代码：
```
const result = client.getUser()
```
#### 返回值说明

- result: User 类型，类型说明如下

<a name='user'></a>

User:

```
{
  UserId: string ,  // 为用户 ID
  UserType: string, // 用户类型
  UserName: string, // 用户名称
}
```

<a name ="client-getusers"></a>

<!-- ### 8 getUsers 方法
获取房间所有用户信息，示例代码：
```
const result = client.getUsers()
```
#### 返回值说明

- result: Object 类型，类型说明如下

```
{
  AdminUsers: Array<user>,
  defaultUsers: Array<user>,
}
``` -->

<a name ="#client-adminusers"></a>

### 8 getAdminUsers 方法
获取房间 admin 用户，示例代码：
```
const result = client.getAdminUsers()
```
#### 返回值说明

- result: Array<user> 类型，类型说明如下

<a name ="client-defaultusers"></a>

### 9 getDefaultUsers 方法
获取房间 default 用户，示例代码：
```
const result = client.getDefaultUsers()
```
#### 返回值说明

- result: Array<user> 类型 

<a name ="client-getwhiteboard"></a>

### 10 getWhiteboard 方法
获取房间白板信息
```
const result = client.getWhiteboard();
```
#### 返回值说明

- result: Array<user> 类型，类型说明如下
```
{
    uuid: string,  加入白板 id
    token: string, 加入白板 token
} 
```

<a name="client-on"></a>

### 11 on 方法

给事件绑定监听函数，示例代码：

```
client.on(EventType, Listener)
```

#### 参数说明

- EventType: string 类型， 必传，目前有  | "Msg" 收到消息
| "Ban" 禁言
| "Id" 白板 ID 推送
| "Broadcast" 广播
| "Users" 用户加入
| "Bulletin" 公告
| "CallAuth" 连麦权限
| "CallApply" 发起上麦申请
| "CallReply" 上麦回复
| "CustomContent" 自定义消息
| "CustomContentPeers"; 点对点自定义消息 这些事件可绑定监听函数
- Listener: function 类型，事件监听函数

<a name="client-off"></a>

### 12 off 方法

解除绑定事件的监听函数，示例代码：

```
client.off(EventType, Listener)
```

#### 参数说明

- EventType: 参见 on 方法
- Listener: 为调用 on 方法时绑定的监听函数

<a name="client-sendnotice"></a>

### 13 sendNotice 方法

发布公告（公告信息可在获取房间信息中获取），示例代码：

```
client.off(EventType, Listener)
```

#### 参数说明

- EventType: 参见 on 方法
- Listener: 为调用 on 方法时绑定的监听函数

<a name="client-sendcustommsg"></a>

### 14 sendCustomMsg 方法

发布自定义消息（公告信息可在获取房间信息中获取），示例代码：

```
client.sendCustomMsg(
    type,
    content,
    onSuccess，
    onError
)
```

#### 参数说明

- type:  string 类型，自定义 type 值
- content: string 类型，自定义消息主体

<a name="client-sendcustompeermsg"></a>

### 15 sendCustomPeerMsg 方法

发布点对点自定义消息（公告信息可在获取房间信息中获取），示例代码：

```
client.sendCustomPeerMsg(
    userId,
    type,
    content,
    onSuccess，
    onError
)
```

#### 参数说明
- userId: string 类型， 接收方 id
- type:  string 类型，自定义 type 值
- content: string 类型，自定义消息主体

<a name="client-applycall"></a>

### 16 applyCall 方法

发起连麦请求，示例代码：

```
client.applyCall(
    userId,
    flag,
    onSuccess，
    onError
)
```

#### 参数说明
- userId: string 类型， 接收方 id
- flag:  string 类型，apply 申请 or cancel 取消

<a name="client-replycall"></a>

### 17 replyCall 方法

连麦回复请求，示例代码：

```
client.replyCall(
    userId,
    flag,
    onSuccess，
    onError
)
```

#### 参数说明
- userId: string 类型， 接收方 id
- flag:  string 类型，agree 同意 or refuse 拒绝

<a name="client-getRoomInfo"></a>

### 18 getRoomInfo 方法

获取房间信息，示例代码：
```
const result = client.getRoomInfo()
```
#### 返回值说明

- result: object 类型，类型说明如下

```
{
    RoomId: string,     //房间 id
    Bulletin: string,   //房间公告
    CallOperation: string,  //房间连麦权限
    applayList: string, //房间连麦列表
}
```

<a name='version'></a>
## 二、version 属性

version 属性用于显示当前 sdk 的版本

---

<a name='setservers'></a>

## 三、setServers 方法

可配置 URTC_IM 服务的域名

```
let {Client,setServers } = urtc_im;
setServers({
    api:'http://localhost:8080'
});
```
