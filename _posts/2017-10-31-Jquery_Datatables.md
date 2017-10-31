---
layout: post
title: "jquerydatatable"
date: 2017-10-31
description: "jquery"
tag: jquery
---   

# 吐槽
```
前段时间自己接触了bootstrap，然后简单的看了一个项目，自己感受到他的datatable蛮好看的，之前用过easyui，感觉丑的无力吐槽，接着，我就看了一下他用的jquery datatable的实例，自己也学着做了点，虽然出现了很多问题，但最后还是做出来了简单的crud...(网上找的模板，下载下来是html格式，我把它都转成jsp了，因为html貌似不能把后台传入的数据写到页面，所以就换成jsp了，页面呈现是没有任何问题，可在引入js文件的时候，我发现失效了...好吧，有可能是我的springmvc的问题..之前把这些资源文件都做了资源映射(html的时候)..转成jsp就出现一些麻烦事...好吧，我也不知道我在说什么，发现自己菜的不行，进入正题吧。)
```
# 介绍
```
[官网](https://www.datatables.net/)
[中文网](http://www.datatables.club/)
atatables是一款jquery表格插件。它是一个高度灵活的工具，可以将任何HTML表格添加高级的交互功能。

分页，即时搜索和排序
几乎支持任何数据源：DOM， javascript， Ajax 和 服务器处理
支持不同主题 DataTables, jQuery UI, Bootstrap, Foundation
各式各样的扩展: Editor, TableTools, FixedColumns ……
丰富多样的option和强大的API
支持国际化
超过2900+个单元测试
免费开源 （ MIT license ）！ 商业支持
```
# datatable实现crud
```
基本功能官网都能查到...也有很多examples..这里就不说了，直接贴上自己实现的crud把.
```
## tables.jsp(
```
可以直接看table标签那，一些css样式是从网上bootstrap模板下的一个后台管理界面，不必理会，table相应需要的js和css在官网上也有说明(如果是像我这样实现简单功能的话)
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html lang="en">

<head>

<meta charset="utf-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="description" content="">
<meta name="author" content="">

<title>用户列表</title>

<!-- Bootstrap Core CSS -->
<link
	href="../vendor/bootstrap/css/bootstrap.min.css" rel="stylesheet">

<!-- MetisMenu CSS -->
<link href="../vendor/metisMenu/metisMenu.min.css" rel="stylesheet">

<!-- DataTables CSS -->
<link href="../vendor/datatables-plugins/dataTables.bootstrap.css"
	rel="stylesheet">

<!-- DataTables Responsive CSS -->
<link href="../vendor/datatables-responsive/dataTables.responsive.css"
	rel="stylesheet">

<!-- Custom CSS -->
<link href="../dist/css/sb-admin-2.css" rel="stylesheet">


<!-- Custom Fonts -->
<link href="../vendor/font-awesome/css/font-awesome.min.css"
	rel="stylesheet" type="text/css">


<link
	href="../vendor/datatables-editor/css/select.dataTables.min.css"
	rel="stylesheet" type="text/css">
<link
	href="../vendor/datatables-editor/css/buttons.dataTables.min.css"
	rel="stylesheet" type="text/css">
<link href="../vendor/datatables-editor/css/editor.dataTables.min.css"
	rel="stylesheet" type="text/css">
	<script type="text/javascript">
		function cleanCache(){
			  $.ajax({
		             type: "POST",
		             url: "/cleanCache",
		             success: function(data){
		            	 alert("清除成功！");
		             }
		         });
		}
	</script>
	
</head>

<body>
		
			<jsp:include page="head.jsp" flush="true"/>
			<div class="navbar-default sidebar" role="navigation">
				<div class="sidebar-nav navbar-collapse">
					<ul class="nav" id="side-menu">
						<li class="sidebar-search">
							<div class="input-group custom-search-form">
								<input type="text" class="form-control" placeholder="Search...">
								<span class="input-group-btn">
									<button class="btn btn-default" type="button">
										<i class="fa fa-search"></i>
									</button>
								</span>
							</div> <!-- /input-group -->
						</li>
						<li><a href="index.html"><i class="fa fa-dashboard fa-fw"></i>
								Dashboard</a></li>
						<li><a href="#"><i class="fa fa-bar-chart-o fa-fw"></i>
								Charts<span class="fa arrow"></span></a>
							<ul class="nav nav-second-level">
								<li><a href="flot.html">Flot Charts</a></li>
								<li><a href="morris.html">Morris.js Charts</a></li>
							</ul> <!-- /.nav-second-level --></li>
						<li><a href="tables.html"><i class="fa fa-table fa-fw"></i>
								Tables</a></li>
						<li><a href="forms.html"><i class="fa fa-edit fa-fw"></i>
								Forms</a></li>
						<li><a href="#"><i class="fa fa-wrench fa-fw"></i> UI
								Elements<span class="fa arrow"></span></a>
							<ul class="nav nav-second-level">
								<li><a href="panels-wells.html">Panels and Wells</a></li>
								<li><a href="buttons.html">Buttons</a></li>
								<li><a href="notifications.html">Notifications</a></li>
								<li><a href="typography.html">Typography</a></li>
								<li><a href="icons.html"> Icons</a></li>
								<li><a href="grid.html">Grid</a></li>
							</ul> <!-- /.nav-second-level --></li>
						<li><a href="#"><i class="fa fa-sitemap fa-fw"></i>
								Multi-Level Dropdown<span class="fa arrow"></span></a>
							<ul class="nav nav-second-level">
								<li><a href="#">Second Level Item</a></li>
								<li><a href="#">Second Level Item</a></li>
								<li><a href="#">Third Level <span class="fa arrow"></span></a>
									<ul class="nav nav-third-level">
										<li><a href="#">Third Level Item</a></li>
										<li><a href="#">Third Level Item</a></li>
										<li><a href="#">Third Level Item</a></li>
										<li><a href="#">Third Level Item</a></li>
									</ul> <!-- /.nav-third-level --></li>
							</ul> <!-- /.nav-second-level --></li>
						<li><a href="#"><i class="fa fa-files-o fa-fw"></i>
								Sample Pages<span class="fa arrow"></span></a>
							<ul class="nav nav-second-level">
								<li><a href="blank.html">Blank Page</a></li>
								<li><a href="login.html">Login Page</a></li>
							</ul> <!-- /.nav-second-level --></li>
					</ul>
				</div>
				<!-- /.sidebar-collapse -->
			</div>
			<!-- /.navbar-static-side -->
		</nav>

		<div id="page-wrapper">
			<div class="row">
				<div class="col-lg-12">
					<h1 class="page-header">用户列表</h1>
					
				</div>
				<!-- /.col-lg-12 -->
			</div>
			<!-- /.row -->
			<div class="row">
				<div class="col-lg-12">
					<div class="panel panel-default">
						<div class="panel-body">
						<input type="button"  onclick="cleanCache()" value="清除用户权限缓存">
							<table width="100%"
								class="table table-striped table-bordered table-hover"
								id="dataTables-example">
								<thead>
									<tr>
										<th>用户ID</th>
										<th>用户名</th>
										<th>密码</th>
										<th>盐</th>
										<th>匿称</th>
										<th>新建日期</th>
									</tr>
								</thead>
							</table>
							<!-- /.table-responsive -->

						</div>
						<!-- /.panel-body -->
					</div>
					<!-- /.panel -->
				</div>
				<!-- /.col-lg-12 -->
			</div>
			<!-- /.row -->
		</div>

		<!-- jQuery -->
		<script src="../vendor/jquery/jquery.min.js"></script>

		<!-- Bootstrap Core JavaScript -->
		<script src="../vendor/bootstrap/js/bootstrap.min.js"></script>

		<!-- Metis Menu Plugin JavaScript -->
		<script src="../vendor/metisMenu/metisMenu.min.js"></script>

		<!-- DataTables JavaScript -->
		<script src="../vendor/datatables/js/jquery.dataTables.min.js"></script>
		<script src="../vendor/datatables-plugins/dataTables.bootstrap.min.js"></script>
		<script src="../vendor/datatables-responsive/dataTables.responsive.js"></script>
		<script src="../vendor/datatables-editor/js/dataTables.editor.min.js"></script>
		<script
			src="https://cdn.datatables.net/buttons/1.4.0/js/dataTables.buttons.min.js"></script>
		<script
			src="https://cdn.datatables.net/select/1.2.2/js/dataTables.select.min.js"></script>
		<!-- Custom Theme JavaScript -->
		<script src="../dist/js/sb-admin-2.js"></script>
		 <script
		    src="https://cdn.datatables.net/buttons/1.2.1/js/buttons.print.min.js"></script> 
		<script src="../js/tables.js"></script>
</body>

</html>

```
## table.js
```
/* $(document).ready(function() {   });*/
    Date.prototype.Format = function (fmt) { //author: meizz
      var o = {
        "M+": this.getMonth() + 1, //月份
        "d+": this.getDate(), //日
        "h+": this.getHours(), //小时
        "m+": this.getMinutes(), //分
        "s+": this.getSeconds(), //秒
        "q+": Math.floor((this.getMonth() + 3) / 3), //季度
        "S": this.getMilliseconds() //毫秒
      };
      if (/(y+)/.test(fmt)) fmt = fmt.replace(RegExp.$1, (this.getFullYear() + "").substr(4 - RegExp.$1.length));
      for (var k in o)
      if (new RegExp("(" + k + ")").test(fmt)) fmt = fmt.replace(RegExp.$1, (RegExp.$1.length == 1) ? (o[k]) : (("00" + o[k]).substr(("" + o[k]).length)));
      return fmt;
    }
	 var editor;
	 
	 
	    editor = new $.fn.dataTable.Editor( {
	        ajax: function (method, url, d, successCallback, errorCallback) {

	            var output = { data: [] };
	            if ( d.action === 'create' ) {
	                $.each( d.data, function (key, value) {

	                    $.ajax({
	                        url:"/user/add",//
	                        type:"post",
	                        async:false,
	                        data:value,
	                        success:function (datas) {
	                            var userInfo = JSON.parse(datas)["data"];
	                            alert()
	                            value.id = userInfo["id"]
	                        }
	                    });
	                    output.data.push( value );
	                } );
	            }else if ( d.action === 'edit' ) {
	                $.each( d.data, function (id, value) {
	                    value.id =id;
	                    $.ajax({
	                        url:"/user/update",
	                        type:"post",
	                        async:false,
	                        data:value,
	                        success:function (datas) {
	                            alert("修改成功");
	                        }
	                    });

	                    output.data.push( value );

	                } );
	            }else if ( d.action === 'remove' ) {
	                $.each( d.data, function (id, value) {
	                    value.id =id;
	                    $.ajax({
	                        url:"/user/delete",
	                        type:"post",
	                        async:false,
	                        data:value,
	                        success:function (datas) {
	                            alert("删除成功");
	                        }
	                    });

	                    output.data.push( value );

	                } );
	            }

	            successCallback( output );

	        },
	        table: "#dataTables-example",
	        idSrc:  'id',
	        serverSide: true,
	        fields: [ {
	                label: "账号:",
	                name: "username"
	            }, {
	                label: "密码:",
	                name: "password"
	            }, {
	                label: "盐:",
	                name: "salt"
	            }, {
	                label: "别名:",
	                name: "nike"
	            }
	        ]
	    } );
	  
	    
	 var table = $('#dataTables-example').DataTable({
		dom: "Bfrtip",
	    select: {
	        style:    'os',
	        selector: 'td:first-child'
	    },
	    responsive: true,
		ajax: {
			url : "/user/list",
			async:false
		},
		responsive : true,
		columns: [
		            { "data": "id" },
		            { "data": "username" },
		            { "data": "password" },
		            { "data": "salt" },
		            { "data": "nike" },
		            { data: "created" 
		            ,render: function(data) { 
		            		if(data==null)
		            			return '';
		            	    return new Date(data).Format("yyyy年MM月dd日 hh:mm:ss"); 
		            	}  
		            }
		        ],
		buttons: [
		            { extend: "create", text:"新建", editor: editor },
		            { extend: "edit",  text:"修改", editor: editor },
		            { extend: "remove", text:"删除",editor: editor }
		        ],
		 oLanguage: {
              "sProcessing": "正在加载中......",
              "sLengthMenu": "每页显示 _MENU_ 条记录",
              "sZeroRecords": "对不起，查询不到相关数据！",
              "sEmptyTable": "表中无数据存在！",
              "sInfo": "当前显示 _START_ 到 _END_ 条，共 _TOTAL_ 条记录",
              "sInfoFiltered": "数据表中共为 _MAX_ 条记录",
              "sSearch": "搜索",
              "oPaginate": {
                  "sFirst": "首页",
                  "sPrevious": "上一页",
                  "sNext": "下一页",
                  "sLast": "末页"
              }
          } //多语言配置
	});


```
## controller
```
package com.johnny.controller;

import java.util.HashMap;
import java.util.List;
import java.util.Map;

import org.apache.logging.log4j.LogManager;
import org.apache.logging.log4j.Logger;
import org.apache.shiro.authz.annotation.Logical;
import org.apache.shiro.authz.annotation.RequiresPermissions;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.ResponseBody;

import com.alibaba.fastjson.JSON;
import com.johnny.model.User;
import com.johnny.service.UserService;
import com.johnny.shiro.CustomRealm;
import com.johnny.util.HgbResult;
import com.johnny.util.UserException;

@Controller
public class UserController {
	
	private  final Logger logger = LogManager.getLogger(UserController.class.getName());
	
	@Autowired
	private UserService userService;
	
	@Autowired
	private CustomRealm customRealm;
	
	//返回用户列表
	@RequestMapping(value="/user/list",method=RequestMethod.GET)
	@RequiresPermissions(value={"user:query","user:*"},logical = Logical.OR)
	@ResponseBody
	public String getUserList()throws Exception{
		logger.info("go userlist~");
		List<User> list = userService.findUserList();
		Map<String,List> map = new HashMap<>();
		map.put("data", list);
		return JSON.toJSONString(map);
	}
	//根据用户id查询用户信息
	@RequestMapping("/user/{id}")
	@ResponseBody
	public User getUserById(@PathVariable Integer id)throws Exception{
		User user = userService.findUserById(id);
		if(user == null){
			throw new UserException("未找到用户信息");
		}
		return user;
	}
	//新增用户
	@RequestMapping(value="/user/add", method=RequestMethod.POST)
	@RequiresPermissions(value={"user:add","user:*"},logical = Logical.OR)
	@ResponseBody
	public String addUser(User u)throws Exception{
		logger.info("add User~");
		HgbResult result = userService.addUser(u);
		return JSON.toJSONString(result);
	}
	//删除
	@RequestMapping(value="/user/delete", method=RequestMethod.POST)
	@RequiresPermissions(value={"user:delete","user:*"},logical = Logical.OR)
	@ResponseBody
	public String deleteUser(@RequestParam int id)throws Exception{
		logger.info("delete User~"+id);
		HgbResult result = userService.deleteUser(id);
		return JSON.toJSONString(result);
	}
	@RequestMapping(value="/user/update", method=RequestMethod.POST)
	@RequiresPermissions(value={"user:edit","user:*"},logical = Logical.OR)
	@ResponseBody
	public String updateUser(User u)throws Exception{
		logger.info("update User~");
		HgbResult result = userService.updateUser(u);
		return JSON.toJSONString(result);
	}
	/**
	 * 清除缓存
	 * @param u
	 * @return
	 * @throws Exception
	 */
	@RequestMapping(value="/cleanCache", method=RequestMethod.POST)
	@RequiresPermissions("user:*")
	@ResponseBody
	public String cleanCache()throws Exception{
		logger.info("cleanCache Success!");
		customRealm.clearCached();
		return JSON.toJSONString(new HgbResult("1","success",null));
	}
}

```
## service
```
package com.johnny.service.impl;

import java.util.Date;
import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import com.johnny.dao.UserMapperCustom;
import com.johnny.model.User;
import com.johnny.service.UserService;
import com.johnny.util.HgbResult;
import com.johnny.util.UserException;

@Service
public class UserServiceImpl implements UserService {
	
	@Autowired
	private UserMapperCustom userMapper;
	
	@Override
	public List<User> findUserList() throws Exception {
		List<User> list = null;
		list = userMapper.findUserList();
		return list;
	}

	@Override
	public User findUserById(int id) throws Exception {
		User u = userMapper.findUserById(id);
		return u;
	}

	@Override
	public HgbResult addUser(User u) throws Exception {
		u.setCreated(new Date());
		userMapper.addUser(u);
		return new HgbResult("1","success",u);
	}

	@Override
	public HgbResult deleteUser(int id) throws Exception {
		userMapper.deleteUser(id);
		return new HgbResult("1","success",null);
	}

	@Override
	public HgbResult updateUser(User u) throws Exception {
		if(u.getUsername().equals(""))
			u.setUsername(null);
		else if(u.getPassword().equals(""))
			u.setPassword(null);
		else if(u.getSalt().equals(""))
			u.setSalt(null);
		else if(u.getNike().equals(""))
			u.setNike(null);
		userMapper.updateUser(u);
		return new HgbResult("1","success",null);
	}

}

```
## mapper.xml
```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd" >
<mapper namespace="com.johnny.dao.UserMapperCustom" >
 	<select id="findUserList" resultType="com.johnny.model.User">
 		select * from user
 	</select>
 	
 	<select id="findUserById" parameterType="int" resultType="com.johnny.model.User">
 		select * from user
 		where id = #{id}
 	</select>
 	
 	<insert id="addUser" parameterType="com.johnny.model.User">
 		Insert into user(username,password,salt,nike,created)
 		values(#{username},#{password},#{salt},#{nike},#{created})
 	</insert>
 	<delete id="deleteUser" parameterType="int">
 		DELETE FROM user WHERE id = #{id} 
 	</delete>
 	<update id="updateUser" parameterType="com.johnny.model.User">
 		UPDATE user as u
		<set>
			<if test="username != null">username=#{username},</if>
			<if test="password != null">password=#{password},</if>
			<if test="salt != null">salt=#{salt},</if>
			<if test="nike != null">nike=#{nike}</if>
		</set>
		WHERE u.id = #{id}
 	</update>
</mapper>
```
## sql
```
CREATE TABLE `user` (
  `id` int(11) NOT NULL AUTO_INCREMENT COMMENT '用户id',
  `username` varchar(255) DEFAULT NULL COMMENT '用户名',
  `password` varchar(255) DEFAULT NULL COMMENT '密码',
  `salt` varchar(255) DEFAULT NULL COMMENT '盐',
  `nike` varchar(255) DEFAULT NULL COMMENT '别名',
  `created` datetime DEFAULT NULL COMMENT '创建时间',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=27 DEFAULT CHARSET=utf8;

```
# 效果
![](/images/mybatisnxgc/a.jpg)
![](/images/mybatisnxgc/b.jpg)
![](/images/mybatisnxgc/c.jpg)
![](/images/mybatisnxgc/d.jpg)