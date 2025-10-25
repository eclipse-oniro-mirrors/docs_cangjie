# IPC与RPC通信开发指导

## 场景介绍

客户端和服务端使用消息队列进行通信。

## 客户端和服务端通信示例

- 定义服务端

```cangjie
class Stub <: RemoteObject {
    public init(descriptor: String) {
        super(descriptor)
    }

    public func onRemoteMessageRequest(code: Int32, data: MessageSequence, reply: MessageSequence, option: MessageOption): Bool {
        match(code) {
            case 1 =>
                // 按照客户端写入顺序读取对应数据，具体看业务逻辑
                // 此处是根据后面客户端发送消息给服务端做的示例
                let ret = MyParcelable()
                data.readParcelable(ret)
                // 发送数据给客户端
                let ashmem = Ashmem.create("ashmem", 1024)
                ashmem.writeDataToAshmem([1, 2, 3], 3, 0)
                let mes = MyParcelable(1, "this is stub", ashmem)
                reply.writeParcelable(mes)
                return true
            case _ => return false
        }
    }
}

// 服务端和客户端共用的自定义序列化对象
class MyParcelable <: Parcelable {
    // 整型数据
    var num: Int32 = 0
    // 字符串数据
    var str: String = ''
    // 匿名共享内存对象
    var ashmem: Ashmem

    init() {
        this.ashmem = Ashmem.create("ashmem", 1024)
    }

    init(num: Int32, str: String, ashmem: Ashmem) {
        this.num = num
        this.str = str
        this.ashmem = ashmem
    }
    public func marshalling(messageSequence: MessageSequence): Bool {
        messageSequence.writeInt(this.num)
        messageSequence.writeString(this.str)
        messageSequence.writeAshmem(this.ashmem)
        return true
    }
    public func unmarshalling(messageSequence: MessageSequence): Bool {
        this.num = messageSequence.readInt()
        this.str = messageSequence.readString()
        this.ashmem = messageSequence.readAshmem()
        return true
    }
}
```

- 定义客户端

```cangjie
import kit.IPCKit.*

let option = MessageOption()
let data = MessageSequence.create()
let reply = MessageSequence.create()

// 准备发送给服务端的数据
let ashmem = Ashmem.create("ashmem", 1024)
ashmem.writeDataToAshmem([3, 2, 1], 3, 0)
let mes = MyParcelable(0, "this is proxy", ashmem)
data.writeParcelable(mes)

let proxy = IRemoteObject()
proxy.sendMessageRequest(1, data, reply, option)
// 从reply中读取服务端发送的数据
let ret = MyParcelable()
reply.readParcelable(ret)
```