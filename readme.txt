卸载源码运行的openfire。

策略：
I：用户在线的情况
服务器发送message-》RoutingTableImpl.java routePacket(*) ->messageRouter.saveMessage().  将message保存到ofMessageSend表中。 --》把message发送到用户

II: 用户离线的情况
--服务器发送message-》RoutingTableImpl.java routePacket(*) ->messageRouter.saveMessage(). 将message保存到ofMessageSend表中。因为用户离线所以routed 是false。  messageRouter.routingFailed(jid, packet);  -》把message保存到ofoffline表中。

--当用户上线时，PresenceUpdateHandler.java 的 initSession(ClientSession session)  中检测到用户上线。查找ofoffline，发送message，同时删除ofoffline下的message（OfflineMessageStore.java   getMessages(String username, boolean delete)) 	

==============================
源码的openfire已经运行后，要先停止这个openfire。停止命令如下：
netstat -ano | findstr "5222"
taskkill /f /pid 进程号


=======
admin 密码是admin
==========
这个参数需要进行设置
服务器： pushMessageForClient -》服务器设置-》idle connections Policy 


+++++++++++++++++++++++++++++++++++++
+++++++++++++++App++++++++++++++++++++++
+++++++++++++++++++++++++++++++++++++
+++++++++++++++++++++++++++++++++++++

App在前端时，每隔1min会ping服务器。用户不掉线。
app在后端时，ping 5次 后掉线


 
问题（10min内的测试结果）:1. 亮屏，APP在后台： -- ping 的次数          结论： 一直在ping（sendServerPing()）。
                          --重新链接的次数      结论：一直在重连，直到可以链接上

     2. 灭屏，APP在后天： -- ping 的次数         //华为mate8 有内置app kill掉  server
                          --重新链接的次数      //华为mate8 有内置app kill掉  server
     3. 亮屏，APP在前台： --Ping的次数          结论： 一直在ping（sendServerPing()）。
                          --重连次数           结论：一直在重连，直到可以链接上   （connectionFailed(): registering reconnect in 20s）

     4. 灭屏，APP在前台：--Ping的次数           结论： 一直在ping（sendServerPing()）
                          --重连次数             结论：一直在重连，直到可以链接上

问题： 亮屏，断开WiFi---》一直在ping。当wifi重新链接上后，user链接上