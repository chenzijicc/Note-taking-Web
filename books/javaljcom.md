#### java 连接com
[jar包](http://chenziji.top/upload/2022/11/mfz-rxtx-2.2-20081207-win-x64.zip)
```java
package com.fz;

import gnu.io.CommPortIdentifier;
import gnu.io.PortInUseException;
import gnu.io.SerialPort;
import gnu.io.SerialPortEvent;
import gnu.io.SerialPortEventListener;
import gnu.io.UnsupportedCommOperationException;

import java.io.*;
import java.util.Enumeration;
import java.util.TooManyListenersException;

public class SimpleRead implements Runnable,SerialPortEventListener {
    static CommPortIdentifier portId;

    static Enumeration portList;

    InputStream inputStream;

    SerialPort serialPort;

    Thread readThread;

    public static void main(String[] args) {

        String com="2";
        if(args!=null&&args.length>=1)
            com=args[0];

        portList = CommPortIdentifier.getPortIdentifiers();
        // 检索系统串口  
        while (portList.hasMoreElements()) {
            portId = (CommPortIdentifier) portList.nextElement();

            /*如果端口类型是串口，则打印出其端口信息*/
            if (portId.getPortType() == CommPortIdentifier.PORT_SERIAL) {
                System.out.println("------------------------");
                System.out.println("系统可用串口: "+portId.getName());
                System.out.println("------------------------");
                // 指定COM口  
                if (portId.getName().equals("COM"+com)) {
                    System.out.println("找到COM"+com+"口,初始化...");
                    SimpleRead reader = new SimpleRead();
                }else{
                    System.out.println("无法找到COM"+com+"口,请重新指定...");
                }
            }
        }
    }

    public SimpleRead() {
        try {
            // 打开COM串口 2000 设置毫秒数 超时等待时间

            serialPort = (SerialPort) portId.open("SimpleReadApp",2000);
            System.out.println("COM口打开成功！");

        } catch (PortInUseException e) {
            System.out.println("端口被占用");
        }
        try {
            inputStream = serialPort.getInputStream();
           /* OutputStream outputStream = serialPort.getOutputStream();
            InputStream in = new FileInputStream("E:\\b.txt");
            byte[] bytes = new byte[2];
            int n;
            while ((n = in.read(bytes)) != -1) {
                outputStream.write(bytes,0,n); //这里同样的不写n也会出现bug
            }
            in.close();*/

            System.out.println("获得输入流...");
        } catch (IOException e) {
        }
        //进行端口监听,当事件发生自动调用 serialEvent方法  
        try {
            serialPort.addEventListener(this);
        } catch (TooManyListenersException e) {
        }
        serialPort.notifyOnDataAvailable(true);

        //设置通讯位  
        try {
            System.out.println("设置通讯位...");
            serialPort.setSerialPortParams(115200,// 设置波特率  
                    SerialPort.DATABITS_8,// 数据位数  
                    SerialPort.STOPBITS_1,// 停止位  
                    SerialPort.PARITY_NONE);// 奇偶位  
        } catch (UnsupportedCommOperationException e) {
        }

        // 启动线程，监听  
        readThread = new Thread(this);//线程负责每接收一次数据休眠20秒钟  
        readThread.start();
    }

    public void run() {
        try {
            System.out.println("监听...");
            Thread.sleep(20000);//休息20秒  

        } catch (Exception e) {
        }
    }
    // 处理侦听到的串口事件  
    public synchronized void serialEvent(SerialPortEvent event) {
        //    System.out.println("接收数据...\r\n");

        switch (event.getEventType()) {
            case SerialPortEvent.BI://BI - 通讯中断.
            case SerialPortEvent.OE://OE - 溢位错误.
            case SerialPortEvent.FE://FE - 帧错误.
            case SerialPortEvent.PE://PE - 奇偶校验错.
            case SerialPortEvent.CD://CD - 载波检测.
            case SerialPortEvent.CTS://CTS - 清除发送.
            case SerialPortEvent.DSR://DSR - 数据设备准备好.
            case SerialPortEvent.RI://RI - 　振铃指示.
            case SerialPortEvent.OUTPUT_BUFFER_EMPTY://OUTPUT_BUFFER_EMPTY - 输出缓冲区已清空
                break;
            case SerialPortEvent.DATA_AVAILABLE://DATA_AVAILABLE - 有数据到达


               /* byte[] readBuffer = new byte[10000];

                try {
                    //读数据
                    while (inputStream.available() > 0) {
                        int numBytes = inputStream.read(readBuffer);
                    }

                    String str=new String(readBuffer);
                    if(str.equals("exit")){
                        inputStream.close();serialPort.close();
                    }
                    //输出内容
                    System.out.println("<------开始------->");
                    System.out.println(str+"==============");
                    System.out.println("<------结束------->");
                    System.out.println("                    ");




                } catch (IOException e) {
                }*/

               try {
                   byte[] bytes = new byte[1024];
                   OutputStream os = new FileOutputStream("E:\\b.txt");
                   while (inputStream.available() > 0) {
                       int numBytes = inputStream.read(bytes);
                       os.write(bytes,0,numBytes);
                   }

               }catch (Exception e){

               }




                break;
        }
    }

}  
```