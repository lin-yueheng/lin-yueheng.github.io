---
title: excel-space
date: 2023-01-20 18:15:34
cover: assets/Snipaste_2023-01-20_23-23-54.png
tags:
---


```java
package com.ityueheng.service;

import com.ityueheng.pojo.Student;
import org.apache.poi.ss.usermodel.Font;
import org.apache.poi.ss.usermodel.HorizontalAlignment;
import org.apache.poi.ss.usermodel.VerticalAlignment;
import org.apache.poi.xssf.usermodel.XSSFCellStyle;
import org.apache.poi.xssf.usermodel.XSSFRow;
import org.apache.poi.xssf.usermodel.XSSFSheet;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.sql.*;
import java.util.ArrayList;
import java.util.List;

public class DB_Excel {
    public static void main(String[] args) {
        setDb_Excel();
    }

    public static void setDb_Excel() {
        String path = "D:\\IDEA-Javaweb\\202110098141\\grade.xlsx";
        List<Student> list = new ArrayList<Student>();
        //把数据传到集合中去，数据库区
        try {
            Class.forName("com.mysql.jdbc.Driver");
            String url = "jdbc:mysql://localhost:3306/db1?useSSL=true&useUnicode=true&characterEncoding=utf-8&serverTimezone=GMT%2B8&allowPublicKeyRetrieval=true";
            String username = "root";
            String password = "123456";
            Connection connection = DriverManager.getConnection(url, username, password);
            Statement statement = connection.createStatement();
            ResultSet resultSet = statement.executeQuery("select * from student");
            while (resultSet.next()) {
                Student student = new Student();
                student.setStu_name(resultSet.getString(1));
                student.setStu_number(resultSet.getString(2));
                student.setStu_grade(resultSet.getString(3));
                student.setProcessing_num(resultSet.getString(4));
                list.add(student);
            }
        } catch (
                SQLException e) {
            throw new RuntimeException(e);
        } catch (ClassNotFoundException e) {
            throw new RuntimeException(e);
        }

        //传到excel区
        try {
            //输入流，先读取文件里面的数据
            FileInputStream fileInputStream = new FileInputStream(path);
            //向一个工作簿中传入数据
            XSSFWorkbook workbook = new XSSFWorkbook(fileInputStream);
            //第一个工作表
            XSSFSheet xssfSheet = workbook.getSheetAt(0);
            XSSFRow xssfRow = xssfSheet.createRow(5);
            FileOutputStream fileOutputStream = new FileOutputStream(path);

            //读取颜色
            XSSFCellStyle style = workbook.createCellStyle();   //红色样式
            XSSFCellStyle style2 = workbook.createCellStyle();  //绿色样式
            /*
             * 水平垂直居中
             */
            style.setAlignment(HorizontalAlignment.CENTER);
            style.setVerticalAlignment(VerticalAlignment.CENTER);

            //写进去序号、学生的姓名以及学号

            int p = 1;


            //字体颜色为红色
            Font font = workbook.createFont();
            font.setColor((short) 2);
            style.setFont(font);

            //字体颜色为绿色
            Font fontG = workbook.createFont();
            fontG.setColor((short) 11);
            style2.setFont(fontG);

            //循环遍历数据库中的数据
            for (Student student : list) {
                String stu_name = student.getStu_name();
                String stu_number = student.getStu_number();
                String stu_grade = student.getStu_grade();
                String processing_num = student.getProcessing_num();

                //测试
                System.out.println(stu_number);

                boolean flag = true;     //判断if语句是否执行

                //匹配excel中的学号，从而把对应的实验几的成绩录进去
                for (int j = 6; j <= xssfSheet.getLastRowNum(); j++) {
                    xssfRow = xssfSheet.getRow(j);
                    //根据数据库中的学生学号来写入相对应的实验成绩
                    if (stu_number.equals(xssfRow.getCell(2).getStringCellValue())) {
                        //测试
                        System.out.println("这个是学号哇！！！！！！！！！！！！！！！！！！！！！！！！！！！");



                        switch (processing_num) {
                            case "实验一" -> xssfRow.createCell(3).setCellValue(stu_grade);
                            case "实验二" -> xssfRow.createCell(4).setCellValue(stu_grade);
                            case "实验三" -> xssfRow.createCell(5).setCellValue(stu_grade);
                            case "实验四" -> xssfRow.createCell(6).setCellValue(stu_grade);
                            case "实验五" -> xssfRow.createCell(7).setCellValue(stu_grade);
                            case "实验六" -> xssfRow.createCell(8).setCellValue(stu_grade);
                            case "实验七" -> xssfRow.createCell(9).setCellValue(stu_grade);
                            case "实验八" -> xssfRow.createCell(10).setCellValue(stu_grade);
                            case "实验九" -> xssfRow.createCell(11).setCellValue(stu_grade);
                        }

                        //实验成绩不足60，标红
                        for (int k = 3; k < 12; k++) {
                            if (xssfRow.getCell(k) != null) {
                                int grade = Integer.parseInt(xssfRow.getCell(k).getStringCellValue());
                                if (grade < 60) {
                                    xssfRow.getCell(k).setCellStyle(style);
                                }
                            }
                        }

                        //实验成绩大于80分，标绿优秀
                        for (int k = 3; k < 12; k++) {
                            if (xssfRow.getCell(k) != null) {
                                int grade = Integer.parseInt(xssfRow.getCell(k).getStringCellValue());
                                if (grade > 80) {
                                    xssfRow.getCell(k).setCellStyle(style2);
                                }
                            }
                        }

                        flag = false;
                        break;
                    }
                }

                if (flag) {
                    for (int j = 6; j <= xssfSheet.getLastRowNum(); j++) {
                        if (!stu_number.equals(xssfRow.getCell(2).getStringCellValue())) {
                            //excel表中没有对应的学号，则把该学生的信息在尾部录进去
                            xssfRow = xssfSheet.getRow(xssfSheet.getLastRowNum() + p);
                            if (xssfRow == null) {
                                int i1 = xssfSheet.getLastRowNum() + p - 7;
                                xssfRow = xssfSheet.createRow(xssfSheet.getLastRowNum() + p);
                                xssfRow.createCell(0).setCellValue(++i1);
                                xssfRow.createCell(1).setCellValue(stu_name);
                                xssfRow.createCell(2).setCellValue(stu_number);


                                switch (processing_num) {
                                    case "实验一" -> xssfRow.createCell(3).setCellValue(stu_grade);
                                    case "实验二" -> xssfRow.createCell(4).setCellValue(stu_grade);
                                    case "实验三" -> xssfRow.createCell(5).setCellValue(stu_grade);
                                    case "实验四" -> xssfRow.createCell(6).setCellValue(stu_grade);
                                    case "实验五" -> xssfRow.createCell(7).setCellValue(stu_grade);
                                    case "实验六" -> xssfRow.createCell(8).setCellValue(stu_grade);
                                    case "实验七" -> xssfRow.createCell(9).setCellValue(stu_grade);
                                    case "实验八" -> xssfRow.createCell(10).setCellValue(stu_grade);
                                    case "实验九" -> xssfRow.createCell(11).setCellValue(stu_grade);
                                }
                                //实验成绩小于60分，标红
                                for (int k = 3; k < 12; k++) {
                                    if (xssfRow.getCell(k) != null) {
                                        int grade = Integer.parseInt(xssfRow.getCell(k).getStringCellValue());
                                        if (grade < 60) {
                                            xssfRow.getCell(k).setCellStyle(style);
                                        }
                                    }
                                }

                                //实验成绩大于80分，标绿优秀
                                for (int k = 3; k < 12; k++) {
                                    if (xssfRow.getCell(k) != null) {
                                        int grade = Integer.parseInt(xssfRow.getCell(k).getStringCellValue());
                                        if (grade > 80) {
                                            xssfRow.getCell(k).setCellStyle(style2);
                                        }
                                    }
                                }
                            }
                        }
                    }
                }
            }

            //成绩总评
//            获取每一行的总分数，然后相加起来
            for (int j = 6; j < xssfSheet.getLastRowNum() + 1; j++) {
                int count = 0;
                xssfRow = xssfSheet.getRow(j);
                for (int k = 3; k < 12; k++) {
                    if (xssfRow.getCell(k) != null) {
                        count += Integer.parseInt(xssfRow.getCell(k).getStringCellValue());
                    }
                }
                xssfRow.createCell(12).setCellValue(count);

                //将老师的个人签名读取并放到excel中

            }


//            System.out.println("成功向Excel表中传入" + xssfRow.getPhysicalNumberOfCells() + "行数据！！！");
            fileOutputStream.flush();
            workbook.write(fileOutputStream);
            fileOutputStream.close();
        } catch (
                IOException s) {
            System.out.println(s);
        }
    }
}

```
