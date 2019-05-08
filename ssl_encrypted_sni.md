# Enrypted SNI
1. 只在tls1.3及以后生效
>> tls1.2会将证书明文传递给客户端，所以相当于没有做；tls1.3中会对server hello之后的所有消息进行加密

2. 

实现方案：
1. server将dh的public key放在dns上，client访问dns取到server的public key
2. client将生成一对临时的dh public/private key，与server的public Key生成一个对称加密的密钥
3. client将public key与加密后的sni发给server
4. server收到后，计算出对称加密的密钥，解出sni

疑点：
1. dns的明文性：监听者可以直接拿到用户要访问的域名
>> 需要用dns over tls or dns over https

2. server端的public key的前向安全性的问题
>> 定时更新dns中的public key

3. server端支持多对dh public/private key,从而支持dns cache的老的public key

4. dh算法的性能如何？nginx以及其他的云服务商如何撑住的？


