java安全主要分为4个部分：<br/>
jca(java cryptography Architeture  java 加密体系结构  ) <br/>
JCE( java cryptography Extension java 加密拓展包) <br/>
jsse (java cryptography socket extension java 安全套接字扩展包) <br/>
jaas(java authentication and authentication service java 鉴别与安全服务)<br/>
安全提供公司一般有：sun,bouncy castle(BC)等。。<br/>
在jdk 的jre 的lib 中的security文件夹下有java.security文件内有当前安全提供者列表(provider list)<br/>
java中加密方式主要是由provider(提供者)概念实现的<br/>
类Provider:<br/>
代表这一个提供者，可以获得该提供者的信息，<br/>
类Security <br/>
管理安全提供者 它可以获取所有安全提供者信息:<br/>
Provider[] providers=Security.getProviders();<br/>
		for(int i=0;i<providers.length;i++){<br/>
			Provider p=providers[i];<br/>
			System.out.println(p+":");<br/>
			for(Map.Entry<Object, Object> entry:p.entrySet()){<br/>
				System.out.println("\t"+entry.getKey()+" |v| "+entry.getValue());<br/>
			}<br/>
		}<br/>
这样可以打印所有安全提供者信息<br/>
类AlgorithmParameter 此类是密码参数不透明规范，他实现自AlgorithmParameterSpi(所有不透明参数都要实现此接口)<br/>
可以通过getAlgorithmParameterSpec获取透明规范的参数<br/>
透明表示规范：在这种表示中，用户可以通过相应规范类中定义的某个get方法来分别访问每个值<br/>
不透明表示规范: 在这种表示中，不可以直接访问个参数域，只能得到与参数集相关联的算法名以及该参数集的某类编码。<br/>
消息摘要算法:MessageDigest jdk1.7支持MD2 MD5 SHA-1 SHA-256  SHA-384 SHA-512 6种摘要算法，摘要名不区分大小写<br/>
还有DigestInputStream,DigestOutputStream 用作流处理进行消息摘要，每一个字符都会update,前提是其中on(boolean on) method是开启的(true),着脸个流处理类分别继承于FilterOutputStream和FilterInputStream<br/>
<br/>
Key接口：<br/>
key 接口是所有密钥接口的顶层接口，一切与加密解密有关的操作都离不开key接口，他又三个主要自接口：<br/>
SecretKey 对称密钥顶层接口 DES,AES 等多种対衬密码算法密钥均可通过该接口提供，PBE(javax.cryto.interface.PBE)接口提供PEB算法定义并继承了该接口。Mac算法实现过程中，通过SecretKey接口提供秘密密钥，通常使用的是SecretKey接口的实现类ScretKeySpec<br/>
PublicKey 非対衬接口公钥<br/>
privateKey 非対衬接口私钥<br/>
DH,RSA,DSA,EC等多种非对称密钥接口均继承了着脸个接口，RSA和DSA以及EC接口均在java.security.interface包中<br/>
keyPair 类<br/>
非对称密钥对，包含两个信息，公钥和私钥<br/>
keyPairGenerator 非対衬密钥对生成器<br/>
keyFactory 类 也是用于生成公钥私钥<br/>
SecureRandom 继承Random 安全随机数生成器 他的默认算法是SHA1PRNG<br/>