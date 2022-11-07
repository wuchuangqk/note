# netstat

## 查看端口占用

```powershell
netstat -ano | findstr 8080
```

```
PS C:\Users\wuchu> netstat -ano | findstr 8080
协议		本机地址								外部地址								状态						PID
TCP    0.0.0.0:8080           0.0.0.0:0              LISTENING       4576
TCP    127.0.0.1:7563         127.0.0.1:8080         ESTABLISHED     16136
TCP    127.0.0.1:8080         127.0.0.1:7563         ESTABLISHED     4576
TCP    192.168.3.20:6291      192.168.3.20:8080      ESTABLISHED     16136
TCP    192.168.3.20:8080      192.168.3.20:6291      ESTABLISHED     4576
```

通过pid查看进程名称

```powershell
tasklist | findstr 4576
```

```
PS C:\Users\wuchu> tasklist | findstr 4576
node.exe                      4576 Console                    4    216,148 K
```

# taskkill

强制结束进程

参数之间用空格隔开

| 参数 | 说明                                 |
| ---- | ------------------------------------ |
| /f   | 强制结束                             |
| /t   | 子进程一并结束                       |
| /pid | 通过pid来结束进程，/pid 4576         |
| /im  | 通过进程名称来结束进程，/im node.exe |

