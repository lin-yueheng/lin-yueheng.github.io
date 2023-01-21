---
title: miniProgram
date: 2023-01-20 18:15:21
cover: assets/wallpaper-2572384.jpg
tags:
---

<h2 align="center">微信小程序每周排行Controlle参考</h2>

```JAVA
package com.software.controller;

import com.baomidou.mybatisplus.core.conditions.query.LambdaQueryWrapper;
import com.baomidou.mybatisplus.core.conditions.query.QueryWrapper;
import com.software.dao.GroupDao;
import com.software.dao.PersonDao;
import com.software.dao.wolfDao;
import com.software.domain.tb_avg;
import com.software.domain.wolfTeam;
import com.software.service.allGroup_Excel_Service;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.io.IOException;
import java.util.ArrayList;
import java.util.List;

@RestController
@RequestMapping("groups")
public class GroupController {
    @Autowired
    GroupDao groupDao;
    @Autowired
    PersonDao personDao;
    @Autowired
    wolfDao wolfDao;

    //插入从所有组别的excel表中的获取到的值,放到allGroup野狼队
    @PostMapping("insert")
    public void saveGroup() throws IOException {
        //获取从excel表中拿到的时间集合和名称集合
        allGroup_Excel_Service aes=new allGroup_Excel_Service();
        aes.ByExcelOfNameAndTime();
        ArrayList<String> listName=aes.listName;
        ArrayList<String> listTime=aes.listTime;
        ArrayList<String> listGroup=aes.listGroup;
        ArrayList<Float> floatArrayList=new ArrayList<>();

        for (String s : listTime) {
            if (s.equals("")) {
                floatArrayList.add(0.00F);
            } else
                floatArrayList.add(Float.parseFloat(s));
        }

        //将获取到的值存到数据库中
        for (int i = 0; i < listName.size(); i++) {
            if (floatArrayList.get(i)>0) {
                wolfTeam wolfTeam = new wolfTeam();
                wolfTeam.setName(listName.get(i));
                wolfTeam.setId(i + 1);
                wolfTeam.setMinstime(floatArrayList.get(i));
                wolfTeam.setGroupname(listGroup.get(i));
                wolfDao.insert(wolfTeam);
            }
        }
    }

    //查询数据库表里面的所有组别的数据
    @GetMapping("getAll")
    public List<wolfTeam> getAll(){
        QueryWrapper<wolfTeam> queryWrapper=new QueryWrapper<>();
        queryWrapper.orderByDesc(String.valueOf(4));
        return wolfDao.selectList(queryWrapper);
    }

    //查询野狼组别平均时长
    @GetMapping("getAllGroupAvg")
    public List<tb_avg> getAllGroupAvg(){
        QueryWrapper<tb_avg> queryWrapper=new QueryWrapper<>();
        queryWrapper.orderByDesc(String.valueOf(3));
        return groupDao.selectList(queryWrapper);
    }

    //视觉组(^_-)
    @PostMapping("vision")
    public void vision(){
        LambdaQueryWrapper<wolfTeam> queryWrapper=new LambdaQueryWrapper<>();
        queryWrapper.eq(wolfTeam::getGroupname,"视觉组(^_-)");
        List<wolfTeam> wolfTeams = wolfDao.selectList(queryWrapper);

        //将此组所有时长取平均值存放在avg表
        tb_avg tb_avg=new tb_avg();
        tb_avg.setGroupname1(wolfTeams.get(3).getGroupname());
        //循环取平均数
        int avg = 0;
        for (wolfTeam team : wolfTeams) {
            avg += team.getMinstime();
        }
        tb_avg.setAvgtime1(avg/wolfTeams.size());
        groupDao.insert(tb_avg);
    }

    //电控组(^_-)
    @PostMapping("electric")
    public void electric(){
        LambdaQueryWrapper<wolfTeam> queryWrapper=new LambdaQueryWrapper<>();
        queryWrapper.eq(wolfTeam::getGroupname,"电控组(^_-)");
        List<wolfTeam> wolfTeams = wolfDao.selectList(queryWrapper);

        //将此组所有时长取平均值存放在avg表
        tb_avg tb_avg=new tb_avg();
        tb_avg.setGroupname1(wolfTeams.get(3).getGroupname());
        //循环取平均数
        int avg = 0;
        for (wolfTeam team : wolfTeams) {
            avg += team.getMinstime();
        }
        tb_avg.setAvgtime1(avg/wolfTeams.size());
        groupDao.insert(tb_avg);
    }

    //机械组(^_-)
    @PostMapping("machine")
    public void machine(){
        LambdaQueryWrapper<wolfTeam> queryWrapper=new LambdaQueryWrapper<>();
        queryWrapper.eq(wolfTeam::getGroupname,"机械组(^_-)");
        List<wolfTeam> wolfTeams = wolfDao.selectList(queryWrapper);

        //将此组所有时长取平均值存放在avg表
        tb_avg tb_avg=new tb_avg();
        tb_avg.setGroupname1(wolfTeams.get(3).getGroupname());
        //循环取平均数
        int avg = 0;
        for (wolfTeam team : wolfTeams) {
            avg += team.getMinstime();
        }
        tb_avg.setAvgtime1(avg/wolfTeams.size());
        groupDao.insert(tb_avg);
    }

    //软件组(^_-)
    @PostMapping("software")
    public void software(){
        LambdaQueryWrapper<wolfTeam> queryWrapper=new LambdaQueryWrapper<>();
        queryWrapper.eq(wolfTeam::getGroupname,"软件组(^_-)");
        List<wolfTeam> wolfTeams = wolfDao.selectList(queryWrapper);

        //将此组所有时长取平均值存放在avg表
        tb_avg tb_avg=new tb_avg();
        tb_avg.setGroupname1(wolfTeams.get(3).getGroupname());
        //循环取平均数
        int avg = 0;
        for (wolfTeam team : wolfTeams) {
            avg += team.getMinstime();
        }
        tb_avg.setAvgtime1(avg/wolfTeams.size());
        groupDao.insert(tb_avg);
    }

    //硬件组(^_-)
    @PostMapping("hardware")
    public void hardware(){
        LambdaQueryWrapper<wolfTeam> queryWrapper=new LambdaQueryWrapper<>();
        queryWrapper.eq(wolfTeam::getGroupname,"硬件组(^_-)");
        List<wolfTeam> wolfTeams = wolfDao.selectList(queryWrapper);

        //将此组所有时长取平均值存放在avg表
        tb_avg tb_avg=new tb_avg();
        tb_avg.setGroupname1(wolfTeams.get(3).getGroupname());
        //循环取平均数
        int avg = 0;
        for (wolfTeam team : wolfTeams) {
            avg += team.getMinstime();
        }
        tb_avg.setAvgtime1(avg/wolfTeams.size());
        groupDao.insert(tb_avg);
    }
}

```

