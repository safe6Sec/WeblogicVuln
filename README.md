# WeblogicVuln
记录weblogic的一些漏洞原理。方便回忆复习。     

weblogic的cve真是多的一批！   
 


# list

主要分三类洞：1.基于t3协议导致的反序列化，2.基于xml导致的反序列化，3.其他漏洞如ssrf，文件上传   

由于cve实在太多，挑几个有代表性的出来看。

## 基于t3协议

### CVE-2015-4852
原理：由t3协议引起的反序列漏洞，完全未过滤。可直接cc链打过去。   
重点：理解t3协议构成，攻击前提熟悉cc链。    


### CVE-2016-0638
原理：由t3协议引起的反序列漏洞，对CVE-2015-4852的黑名单补丁绕过。使用StreamMessageImpl包装cc链绕过黑名单。    
重点：理解StreamMessageImpl是如何包装的。理解readExternal方法   

### CVE-2016-3510
原理：由t3协议引起的反序列漏洞，对CVE-2015-4852的黑名单补丁绕过。使用MarshalledObject包装cc链绕过黑名单。    
重点：理解MarshalledObject是如何包装的。理解readResolve方法   


### CVE-2017-3248
原理：利用JRMP进行反序列化，也属于CVE-2015-4852的补丁绕过。使用了全新的方式进行反序列。    
重点：重点理解Registry+UnicastRef的方式

### CVE-2018-2628
原理：还是利用JRMP进行反序列化，Registry被拉黑。采用直接反序列化UnicastRef的方式绕过，或者使用java.rmi.activation.Activator代替Registry类。

### CVE-2018-2893
原理：用streamMessageImpl封装一下JRMP即可绕过上一个补丁。


### CVE-2018-3248
原理：用RMIConnectionImpl_Stub代替RemoteObjectInvocationHandler进行绕过。


### CVE-2020-2551
原理：利用IIOP进行反序列化,理解rmi和jndi就能理解这个洞。     
重点：重点类JtaTransactionManager。利用bind发送恶意序列化对象。理解RMI全部攻击方式。https://www.anquanke.com/post/id/257452#h2-0

### CVE-2020-2555
原理：用了一条全新的利用链，sink有点像cc1的，source用的是cc5的BadAttributeValueExpException触发limitFilter的toString方法。
重点：多了两个全新类ReflectionExtractor和LimitFilter组成的利用链，ReflectionExtractor是kink点。理解cc5即可理解此链。




## 基于xml

### CVE-2017-3506

### CVE-2017-10271


## 其他

### CVE-2018-2894



