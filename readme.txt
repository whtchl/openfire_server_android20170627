ж��Դ�����е�openfire��

���ԣ�
I���û����ߵ����
����������message-��RoutingTableImpl.java routePacket(*) ->messageRouter.saveMessage().  ��message���浽ofMessageSend���С� --����message���͵��û�

II: �û����ߵ����
--����������message-��RoutingTableImpl.java routePacket(*) ->messageRouter.saveMessage(). ��message���浽ofMessageSend���С���Ϊ�û���������routed ��false��  messageRouter.routingFailed(jid, packet);  -����message���浽ofoffline���С�

--���û�����ʱ��PresenceUpdateHandler.java �� initSession(ClientSession session)  �м�⵽�û����ߡ�����ofoffline������message��ͬʱɾ��ofoffline�µ�message��OfflineMessageStore.java   getMessages(String username, boolean delete)) 	

==============================
Դ���openfire�Ѿ����к�Ҫ��ֹͣ���openfire��ֹͣ�������£�
netstat -ano | findstr "5222"
taskkill /f /pid ���̺�


=======
admin ������admin
==========
���������Ҫ��������
�������� pushMessageForClient -������������-��idle connections Policy 


+++++++++++++++++++++++++++++++++++++
+++++++++++++++App++++++++++++++++++++++
+++++++++++++++++++++++++++++++++++++
+++++++++++++++++++++++++++++++++++++

App��ǰ��ʱ��ÿ��1min��ping���������û������ߡ�
app�ں��ʱ��ping 5�� �����


 
���⣨10min�ڵĲ��Խ����:1. ������APP�ں�̨�� -- ping �Ĵ���          ���ۣ� һֱ��ping��sendServerPing()����
                          --�������ӵĴ���      ���ۣ�һֱ��������ֱ������������

     2. ������APP�ں��죺 -- ping �Ĵ���         //��Ϊmate8 ������app kill��  server
                          --�������ӵĴ���      //��Ϊmate8 ������app kill��  server
     3. ������APP��ǰ̨�� --Ping�Ĵ���          ���ۣ� һֱ��ping��sendServerPing()����
                          --��������           ���ۣ�һֱ��������ֱ������������   ��connectionFailed(): registering reconnect in 20s��

     4. ������APP��ǰ̨��--Ping�Ĵ���           ���ۣ� һֱ��ping��sendServerPing()��
                          --��������             ���ۣ�һֱ��������ֱ������������

���⣺ �������Ͽ�WiFi---��һֱ��ping����wifi���������Ϻ�user������