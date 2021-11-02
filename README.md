# WeblogicVuln
记录weblogic的一些漏洞原理。方便回忆复习。   

持续更新，加油！！


# list

## CVE-2015-4852
原理：由t3协议引起的反序列漏洞，完全未过滤。可直接cc链打过去。   
重点：理解t3协议构成，攻击前提熟悉cc链。    


## CVE-2016-0638
原理：由t3协议引起的反序列漏洞，对CVE-2015-4852的黑名单补丁绕过。使用StreamMessageImpl包装cc链绕过黑名单。    
重点：理解StreamMessageImpl是如何包装的。理解readExternal方法   

## CVE-2016-3510
原理：由t3协议引起的反序列漏洞，对CVE-2015-4852的黑名单补丁绕过。使用MarshalledObject包装cc链绕过黑名单。    
重点：理解MarshalledObject是如何包装的。理解readResolve方法   


## CVE-2017-3248
原理：利用JRMP进行反序列化，也属于CVE-2015-4852的补丁绕过。使用了全新的方式进行反序列。    
重点：重点理解Registry+UnicastRef的方式

## CVE-2018-2628
原理：还是利用JRMP进行反序列化，Registry被拉黑。采用直接反序列化UnicastRef的方式绕过，或者使用java.rmi.activation.Activator代替Registry类。

## CVE-2018-2893
原理：用streamMessageImpl封装一下JRMP即可绕过上一个补丁。


## CVE-2018-3248
原理：用RMIConnectionImpl_Stub代替RemoteObjectInvocationHandler进行绕过。

