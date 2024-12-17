
# 1 IPv6 addresse of npm package registry dosn't work 

出现的 error 
> ETIMEDOUT Error while installing Node packages on Windows

https://stackoverflow.com/questions/28722515/etimedout-error-while-installing-node-packages-on-windows


测试是否是 ipv6 addresse 无法解析 
```bash
ping -4 registry.npmjs.org # does IPv4 connect?
ping -6 registry.npmjs.org # does IPv6 connect?
npm ping # alternative command
```


windows 上的解决方法 (我试了其他方法, 只有这个方法好用 )
![](image/Pasted%20image%2020241217001220.png)

On Windows, disable IPv6 temporarily:

    Open Control Panel > Network and Sharing Center.
    Select your active network adapter.
    Go to Properties > Uncheck Internet Protocol Version 6 (TCP/IPv6).
    Restart your computer.




Unix 上的解决方法 
https://stackoverflow.com/a/75946605
