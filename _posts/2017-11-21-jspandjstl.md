---
layout: post
title: "jsp指令和jstl标签复习"
date: 2017-11-21
description: "常用jsp指令和jstl标签"
tag: 前端
---   
```
复习一下jsp常用的标签，jstl表达式,在将来写项目中可能会用到~~
```

# 一、Include指令 
```
<jsp:include>标签表示包含一个静态的或者动态的文件。 

语法： 
<jsp:include page="path" flush="true" /> 
or 
<jsp:include page="path" flush="true"> 
<jsp:param name="paramName" value="paramValue" /> 
</jsp:include> 

注： 
1、page="path" 为相对路径，或者代表相对路径的表达式。 
2、flush="true" 必须使用flush为true，它默认值是false。 
3、<jsp:param>子句能让你传递一个或多个参数给动态文件，也可在一个页面中 
使用多个<jsp:param> 来传递多个参数给动态文件。 
```
# 二、Forward指令 
```
<jsp:forward>标签表示重定向一个静态html/jsp的文件，或者是一个程序段。 

语法： 
<jsp:forward page="path"} /> 
or 
<jsp:forward page="path"} > 
<jsp:param name="paramName" value="paramValue" />…… 
</jsp:forward> 

注： 
1、page="path" 为一个表达式，或者一个字符串。 
2、<jsp:param> name 指定参数名，value指定参数值。参数被发送到一个动态 
文件，参数可以是一个或多个值，而这个文件却必须是动态文件。要传递多个参 
数，则可以在一个 JSP文件中使用多个<jsp:param>将多个参数发送到一个动态 
文件中。 
```
# 三、UseBean指令 
```
<jsp:useBean>标签表示用来在JSP页面中创建一个BEAN实例并指定它的名字以 
及作用范围。 

语法： 
<jsp:useBean id="name" scope="page | request | session | application" typeSpec /> 
其中typeSpec有以下几种可能的情况： 
class="className" | class="className" type="typeName" | 
beanName="beanName" type="typeName" | type="typeName" | 

注： 
你必须使用class或type，而不能同时使用class和beanName。beanName表示 
Bean的名字，其形式为“a.b.c”。 
```
# 四、GetProperty指令 
```
<jsp:getProperty>标签表示获取BEAN的属性的值并将之转化为一个字符串，然 
后将其插入到输出的页面中。 

语法： 
<jsp:getProperty name="name" property="propertyName" /> 

注： 
1、在使用<jsp:getProperty>之前，必须用<jsp:useBean>来创建它。 
2、不能使用<jsp:getProperty>来检索一个已经被索引了的属性。 
3、能够和JavaBeans组件一起使用<jsp:getProperty>，但是不能与Enterprise 
Java Bean一起使用。 
```
# 五、SetProperty指令 
```
<jsp:setProperty>标签表示用来设置Bean中的属性值。 

语法： 
<jsp:setProperty name="beanName" prop_expr /> 
其中prop_expr有以下几种可能的情形： 
property="*" | property="propertyName" | property="propertyName" 
param="parameterName" | property="propertyName" value="propertyValue" 

注： 
使用 jsp:setProperty 来为一个Bean的属性赋值；可以使用两种方式来实现。 
1、在jsp:useBean后使用jsp:setProperty： 
<jsp:useBean id="myUser" … /> 
… 
<jsp:setProperty name="user" property="user" … /> 
在这种方式中，jsp:setProperty将被执行。 
2、jsp:setProperty出现在jsp:useBean标签内： 
<jsp:useBean id="myUser" … > … 
<jsp:setProperty name="user" property="user" … /> 
</jsp:useBean> 
在这种方式中，jsp:setProperty只会在新的对象被实例化时才将被执行。 

* 在<jsp:setProperty>中的name值应当和<jsp:useBean>中的id值相同。 
```
# 六、Plugin指令 
```
<jsp:plugin>标签表示执行一个applet或Bean，有可能的话还要下载一个Java 
插件用于执行它。 

语法： 
<jsp:plugin 
type="bean | applet" 
code="classFileName" 
codebase="classFileDirectoryName" 
[ name="instanceName" ] 
[ archive="URIToArchive, ..." ] 
[ align="bottom | top | middle | left | right" ] 
[ height="displayPixels" ] 
[ width="displayPixels" ] 
[ hspace="leftRightPixels" ] 
[ vspace="topBottomPixels" ] 
[ jreversion="JREVersionNumber | 1.1" ] 
[ nspluginurl="URLToPlugin" ] 
[ iepluginurl="URLToPlugin" ] > 
[ <jsp:params> 
[ <jsp:param name="parameterName" value="{parameterValue | <%= 
expression %>}" /> ]+ 
</jsp:params> ] 
[ <jsp:fallback> text message for user </jsp:fallback> ] 
</jsp:plugin> 

注： 
<jsp:plugin>元素用于在浏览器中播放或显示一个对象（典型的就是applet和 
Bean),而这种显示需要在浏览器的 java插件。 
当Jsp文件被编译，送往浏览器时，<jsp:plugin>元素将会根据浏览器的版本替 
换成<object>或 者<embed>元素。注意，<object>用于HTML 4.0 ，<embed>用 
于HTML 3.2。 
一般来说，<jsp:plugin>元素会指定对象是Applet还是Bean,同样也会指定 
class的名字，还有位置，另外还会 指定将从哪里下载这个Java插件。 
```
# 七、jsp:fallback
```
<jsp:fallback> text message for user </jsp:fallback>
一段文字用于Java插件不能启动时显示给用户的，如果插件能够启动而applet或Bean不能，那么浏览器会有一个出错信息弹出。


个人感觉除了include...一般都不怎么用...........................
```

下面来jstl吧.


# 1.JSTL标签介绍
```
JSTL是apache对EL表达式的扩展（也就是说JSTL依赖EL），JSTL是标签语言！
JSTL标签使用以来非常方便，它与JSP动作标签一样，只不过它不是JSP内置的标签，需要我们自己导包，以及指定标签库而已！
如果你使用MyEclipse开发JavaWeb，那么在把项目发布到Tomcat时，你会发现，
MyEclipse会在lib目录下存放jstl的Jar包！如果你没有使用MyEclipse开发那么需要自己来导入这个JSTL的Jar包：jstl-1.2.jar。
```
# 2.JSTL标签库
```
JSTL一共包含四大标签库：
core：核心标签库，我们学习的重点；
fmt：格式化标签库，只需要学习两个标签即可；
sql：数据库标签库，不需要学习了，它过时了；
xml：xml标签库，不需要学习了，它过时了。

3.使用taglib指令导入标签库
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt" %>
```

# core标签库常用标签
## 1.out和set标签
```
<c:out value=”aaa”/> 输出aaa字符串常量
<c:out value=”${aaa}” default=”xxx”/> 当${aaa}不存在时，输出xxx字符串
<c:set var=”a” value=”hello”/>
<c:out value="${a }"/>
```
# 2.remove标签
```
<c:remove var="a" scope=”page”/> 删除pageContext中name为a的数据
```
# 3.url标签：该标签会在需要重写URL时添加。
```
<c:url value="/"/> 输出上下文路径：/项目名/
```
# 4.if标签
```
if标签的test属性必须是一个boolean类型的值，如果test的值为true，那么执行if标签的内容，否则不执行。

<c:set var="a" value="1"/>  
<c:if test="${a>100 }">  
<c:out value="${a }"/>  
</c:if>  
```
# 5.choose标签
```
choose标签对应Java中的if/else if/else结构。
when标签的test为true时，会执行这个when的内容。
当所有when标签的test都为false时，才会执行otherwise标签的内容。

<c:set var="score" value="${param.score }"/>  
<c:choose>  
    <c:when test="${score > 100 || score < 0}">错误的分数：${score }</c:when>  
    <c:when test="${score >= 90 }">A级</c:when>  
    <c:when test="${score >= 80 }">B级</c:when>  
    <c:when test="${score >= 70 }">C级</c:when>  
    <c:when test="${score >= 60 }">D级</c:when>  
    <c:otherwise>E级</c:otherwise>  
</c:choose>  
```
# 6.forEach标签[**]
```
orEach当前就是循环标签了，forEach标签有多种两种使用方式：
使用循环变量，指定开始和结束值，类似for(int i = 1; i <= 10; i++) {}；
循环遍历集合，类似for(Object o : 集合)；

<c:forEach>标签用于通用数据循环，它有以下属性
属 性		描 述		是否必须	缺省值
items	   进行循环的项目	   否	         无
begin	      开始条件	           否	          0
end	      结束条件	           否	     集合中的最后一个项目
step	        步长	           否	          1
var	  代表当前项目的变量名	   否	         无
varStatus  显示循环状态的变量	   否	         无


1、循环遍历，输出所有的元素。
<c:foreach items="${list}" var="li">
${li}
</c:foreach>
注意：items 用于接收集合对象，var 定义对象接收从集合里遍历出的每一个元素。同时其会自动转型。
2、循环遍历，输出一个范围类的元素。
<c:foreach items ="${lis}" var = "li " begin="2" end ="12">
${li}
</c:foreach>
注意：begin 定义遍历的开始位置，end定义遍历的结束位置。begin 和end的引号必须写。
3、循环遍历，输出除某个元素以外的元素或输出指定元素。
<c:foreach items="${list}" var ="li" varStatus="status">
<c:if text="${status.count==1}>
${"第一个元素不要"}
</c:if>
${li}
</ c:foreach>
注意：varStatus 表示当前集合的状态（其实是不是，我也不太清楚，只知道这样用，会的人指点下），count为循环一个计算器。
4、循环遍历，输出第一个或最后一个元素。
<c:foreach items="${list}" var ="li" varStatus="status">
<c:if text="${status.first}">我是第一个元素</c:if>
<c:if text="${status.last}">我是最后一个元素</c:if>
</c:foreach>
注意：first表示如果是一个元素，则返回ture,反之则返回false
last 表示如果是最后一个元素，则返回ture,反之则返回false。
5、循环遍历，按指定步长输出。
<c:foreach items="list" var ="li" step="2">
${li}
</c:foreach>
注意：step为循环的步长。每次隔两个单位输出一个。如：1、3、5、==
```

# 7.fmt标签库常用标签
```
fmt标签库是用来格式化输出的，通常需要格式化的有时间和数字。
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %>  
......  
<%  
    Date date = new Date();  
    pageContext.setAttribute("d", date);  
%>  
<fmt:formatDate value="${d }" pattern="yyyy-MM-dd HH:mm:ss"/>  
```
