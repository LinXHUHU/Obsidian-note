

# 只发送，接收阻塞的时候 发送间隔20ms间隔

*内存用量  RSS  4160   约为4K*

![[Pasted image 20231109154816.png]]

*运行时  CPU 占比%CPU  不到 0.1%*

![[Pasted image 20231109154846.png]]
# 接收且发送 20ms

*内存用量  RSS  4288   约为4K*
![[Pasted image 20231109161949.png]]

*运行时  CPU 占比%CPU  约为0.5%*
![[Pasted image 20231109162034.png]]





```
export LD_LIBRARY_PATH=/root/XCP_test:$LD_LIBRARY_PATH


cp -a /root/XCP_test/lib* /usr/lib64

```