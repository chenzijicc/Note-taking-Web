#### java 机器码生成

```java
package com.fz.util;

import com.alibaba.fastjson.JSON;
import sun.misc.BASE64Encoder;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.nio.charset.StandardCharsets;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;
import java.util.HashMap;
import java.util.Map;
import java.util.Objects;
import java.util.Scanner;

public class computerUtil2 {

    /**
     * 获取CPU序列号
     * @return
     * @throws IOException
     */
    public static String getCPUSerialNumber() {
        String next;
        try {
            Process process = Runtime.getRuntime().exec(new String[]{"wmic", "cpu", "get", "ProcessorId"});
            process.getOutputStream().close();
            Scanner sc = new Scanner(process.getInputStream());
            String serial = sc.next();
            next = sc.next();
        } catch (IOException e) {
            throw new RuntimeException("获取CPU序列号失败");
        }
        return next;
    }

    /**
     * 获取 硬盘序列号(Windows)
     * @return
     * @throws IOException
     * @throws InterruptedException
     */
    public static String getHardDiskSerialNumber() {
        try {
            Process process = Runtime.getRuntime().exec(new String[]{"wmic", "path", "win32_physicalmedia", "get", "serialnumber"});
            process.getOutputStream().close();
            Scanner sc = new Scanner(process.getInputStream());
            String serial = sc.next();
            return sc.next();
        } catch (IOException e) {
            throw new RuntimeException("获取硬盘序列号失败");
        }
    }

    /**
     * bois版本号(linux)
     *
     * @return
     */
    public static String getBoisVersion() {
        String result = "";
        Process p;
        try {
            // 管道
            p = Runtime.getRuntime().exec("sudo dmidecode -s bios-version");
            BufferedReader br = new BufferedReader(new InputStreamReader(p.getInputStream()));
            String line;
            while ((line = br.readLine()) != null) {
                result += line;
                break;
            }
            br.close();
        } catch (IOException e) {
            System.out.println("获取主板信息错误");
        }
        return result;
    }

    /**
     * 获取系统序列号(linux)
     *
     * @return
     */
    public static String getUUID() {
        String result = "";
        try {
            Process process = Runtime.getRuntime().exec("sudo dmidecode -s system-uuid");
            InputStream in;
            BufferedReader br;
            in = process.getInputStream();
            br = new BufferedReader(new InputStreamReader(in));
            while (in.read() != -1) {
                result = br.readLine();
            }
            br.close();
            in.close();
            process.destroy();
            System.out.println("获取序列号："+result);
        } catch (Throwable e) {
            e.printStackTrace();
        }
        return result;
    }

    private static String getSplitString(String str, String split, int length) {
        int len = str.length();
        StringBuilder temp = new StringBuilder();
        for (int i = 0; i < len; i++) {
            if (i % length == 0 && i > 0) {
                temp.append(split);
            }
            temp.append(str.charAt(i));
        }
        return temp.toString();
    }

    /**
     * 获取window or linux机器码
     * @return
     */
    public static String getWindowNumber(String type){
        if (Objects.isNull(type)){
            return "";
        }
        Map<String,Object> codeMap=new HashMap<>(2);
        String result = "";
        if ("linux".equals(type)){
            String boisVersion = getBoisVersion();
            codeMap.put("boisVersion",boisVersion);
            System.out.println("boisVersion：" + boisVersion);
            String uuid = getUUID();
            codeMap.put("uuid",uuid);
            System.out.println("uuid：" + uuid);
            String codeMapStr = JSON.toJSONString(codeMap);
            String serials = saltingMD5(codeMapStr);
            result= getSplitString(serials, "-", 4);
        }else if ("window".equals(type)){
            String processorId = getCPUSerialNumber();
            codeMap.put("ProcessorId",processorId);
            System.out.println("ProcessorId：" + processorId);
            String serialNumber = getHardDiskSerialNumber();
            codeMap.put("SerialNumber",serialNumber);
            System.out.println("SerialNumber：" + serialNumber);
            String codeMapStr = JSON.toJSONString(codeMap);
            String serials = saltingMD5(codeMapStr);
            result= getSplitString(serials, "-", 4);
        }else {

        }
        return result;
    }

    /**
     * 生成md5
     *
     * @param message
     * @return
     */
    public static String saltingMD5(String message) {
        String md5str = "";
        try {
            // 1 创建一个提供信息摘要算法的对象，初始化为md5算法对象
            MessageDigest md = MessageDigest.getInstance("MD5");

            // 2 将消息变成byte数组
            byte[] input = message.getBytes();

            // 3 计算后获得字节数组,这就是那128位了
            byte[] buff = md.digest(input);

            // 4 把数组每一字节（一个字节占八位）换成16进制连成md5字符串
            md5str = bytesToHex(buff);

        } catch (Exception e) {
            e.printStackTrace();
        }
        return md5str;
    }

    /**
     * 二进制转十六进制
     *
     * @param bytes
     * @return
     */
    public static String bytesToHex(byte[] bytes) {
        StringBuffer md5str = new StringBuffer();
        // 把数组每一字节换成16进制连成md5字符串
        int digital;
        for (int i = 0; i < bytes.length; i++) {
            digital = bytes[i];

            if (digital < 0) {
                digital += 256;
            }
            if (digital < 16) {
                md5str.append("0");
            }
            md5str.append(Integer.toHexString(digital));
        }
        return md5str.toString().toUpperCase();
    }

    public static void main(String[] args) {
        String windowNumber = getWindowNumber("window");
        System.out.println("机器码：" + windowNumber);
    }
}

```