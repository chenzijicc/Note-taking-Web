#### 把文件写入MySQL数据库
```java
package com.fz.util;

import java.io.*;
import java.sql.*;

public class WriteAndReadFile {
    //定义方法把文件写入MySQL数据库
    public static void writeFileToMySQL(){
        Connection conn=null;
        PreparedStatement ps=null;
        int result = 0;
        String dbDriver="com.mysql.cj.jdbc.Driver";
        String URL="jdbc:mysql://192.168.0.201/store?useUnicode=true&characterEncoding=utf8&useSSL=false&useJDBCCompliantTimezoneShift=true&serverTimezone=GMT%2B8&allowMultiQueries=true";
        String user="root";
        String pwd="701121";
        try {
            Class.forName(dbDriver);
            conn=DriverManager.getConnection(URL,user,pwd);
            String sql="insert into fz_ddd(file) values (?)";
            ps=conn.prepareStatement(sql);
            ps.setInt(1,1);
            File file =new File("E:\\SSMS-Setup-CHS.exe");
            //用FileInputStream来存文件
            InputStream in = new FileInputStream(file);
            ps.setBinaryStream(1,in,(int)file.length());
            result= ps.executeUpdate();
            in.close();
            if (result>0){
                System.out.println("音频文件写入成功！");
            }else {
                System.out.println("音频文件写入失败！");
            }
        }catch (Exception e){
            e.printStackTrace();
        }finally {
            //释放资源
            if (ps!=null){
                try {
                    ps.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }

            if (conn!=null){
                try {
                    conn.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
    }

    public static void ReadFileToLocal(){
        Connection conn=null;
        PreparedStatement ps=null;
        ResultSet rs=null;
        String dbDriver="com.mysql.cj.jdbc.Driver";
        String URL="jdbc:mysql://192.168.0.201/store?useUnicode=true&characterEncoding=utf8&useSSL=false&useJDBCCompliantTimezoneShift=true&serverTimezone=GMT%2B8&allowMultiQueries=true";
        String user="root";
        String pwd="701121";
        try {
            Class.forName(dbDriver);
            conn=DriverManager.getConnection(URL,user,pwd);
            String sql="select * from fz_ddd where rec=?";
            ps=conn.prepareStatement(sql);
            ps.setInt(1,3);
            rs= ps.executeQuery();

            if (rs.next()){
                InputStream in=rs.getBinaryStream("file");
                OutputStream out=new FileOutputStream("E://jrebel2.jar");
                byte[] temp=new byte[1024];
                int len=-1;
                while ((len=in.read(temp))!=-1){
                    out.write(temp);
                }
                in.close();
                out.close();
                System.out.println("音频文件读取成功！");
            }

        }catch (Exception e){
            e.printStackTrace();
        }finally {
            //释放资源
            if (rs!=null){
                try {
                    rs.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if (ps!=null){
                try {
                    ps.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if (conn!=null){
                try {
                    conn.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }

        }


    }



    public static void main(String[] args) {
//        writeFileToMySQL();
        ReadFileToLocal();
    }


}
```