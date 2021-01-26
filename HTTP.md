## HTTP 接口

> 服务器地址为 demo 里的 server 地址  
> 所有接口都为 POST,参数为 json 格式放在 body 中,token 拼接在 url 上  
> HEADER:Content-Type:application/json; charset=utf-8  
> 例子: http://服务器地址/api/v1/chat/sendText?token=your_token

## 发送消息类型

### 发送文本消息

URI: /api/v1/chat/sendText  
METHOD:`POST`  
参数:  
toUser string // 接收人 username  
content string // 发送的文本内容
atList []string // 被@人的 username 数组,内容中也需要包含@昵称+空格+内容,例如@小明 你好

### 发送图片消息

URI: /api/v1/chat/sendPic  
METHOD:`POST`  
参数:  
toUser string // 接收人 username  
imgUrl string // 图片的网络地址

### 发送表情/动图消息

URI: /api/v1/chat/sendEmoji  
METHOD:`POST`  
参数:  
toUser string // 接收人 username  
gifUrl string 非必须 // 图片的网络地址  
emojiMd5 string 非必须 // 接收到 xml 中的 md5 字段值  
emojiTotalLen string 非必须 // 接收到 xml 中的 len 字段值

> 不建议直接使用 gifUrl 参数来直接发送动图 有一定几率失败  
> 最好的方式还是通过接收到的表情消息 xml 中解析出 md5 和 len 来发送,这时候 gifUrl 可为空

### 发送视频消息

URI: /api/v1/chat/sendVideo  
METHOD:`POST`  
参数:  
toUser string // 接收人
videoUrl string // 视频地址  
videoThumbUrl // 视频缩略图地址

### 发送语音消息

URI: /api/v1/chat/sendVoice  
METHOD:`POST`  
参数:  
toUser string // 接收人 username  
silkUrl string // 音频文件地址,silk 格式

---

## 下载消息资源

### 下载消息中的图片

URI: /api/v1/chat/downloadImage  
METHOD:`POST`  
参数:  
xml string // 收到的消息 xml

### 下载消息中的视频

URI: /api/v1/chat/downloadVideo  
METHOD:`POST`  
参数:  
xml string // 收到的消息 xml

### 下载消息中的音频

URI: /api/v1/chat/downloadVoice  
METHOD:`POST`  
参数:  
xml string // 收到的消息 xml  
newMsgId string // 消息 id

---

## 群内操作

### 踢出群成员(机器人必须为管理员身份)

URI: /api/v1/chatroom/delChatRoomMember  
METHOD:`POST`  
参数:  
chatroom string // 相关群 id  
memberList []string // 批量踢出的成员 id
