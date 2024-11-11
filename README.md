
当前仓库主体是设计一些 Printer驱动的一些方法调用之类的.
MultiSendRecv
IBidiSpl::MultiSendRecv




顺便记录一些打印机相关的知识点或是仓库:


https://github.com/michaelknigge/pclparaphernalia PCL 打印.









###打印机协议

打印机目前遇到三种协议，ipp，printer-job-language，lpd三种协议。他们的默认端口分别是631，9100和515.

9100端口的printer-job-language，又称为RAW协议。目前遇到的问题是，此端口发送数据，打印机直接打印，除非发送正确的printer-job-language协议内容。

631端口的ipp协议，更多的是用来获取打印机属性的GET_PRINTER_ATTRIBUTES。

515端口的lpd（Line Printer Daemon Protocol).它使用TCP/IP协议共享服务器上的打印机资源。服务器以Daemon的方式运行一个进程，客户机通过lp,lpr,lpd,lprm等命令实现添加打印，查询及删除打印队列等操作。（目前激光打印机除了极少数型号以外都不支持LPD协议）

This way you can get a (possibly very long) status report about the queue on the host, if lpd is running and the host is reachable. As root, enter the following command:

echo -e "\004<queue>" \
  | netcat -w 2 -p 722 <host> 515
        
If lpd does not respond, it is either inactive or there are basic network problems. If lpd responds, the response should indicate why queue on host cannot be used for printing. Examples:

Example 5.1. Error Message of lpd
lpd: your host does not have line printer access lpd: queue does not exist printer: spooling disabled printer: printing disabled

[https://www.novell.com/documentatio](https://www.novell.com/documentation/suse91/suselinux-adminguide/html/ch05s08.html)
