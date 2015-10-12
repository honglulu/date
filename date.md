
```js
在线时间：
<input type="text" class="dc-input" id="starTime" name="begin_time" value="" bind-datepicker> - 
<input type="text" class="dc-input" name="end_time" id="endTime" value="" bind-datepicker>
  <input type="button" id="yesterDayBtn" class="dc-btn dc-btn-blue dc-btn-s" value="昨天"/>
  <input type="button" id="toDayBtn" class="dc-btn dc-btn-blue dc-btn-s" value="今天"/>
  <input type="button" id="preWeekBtn" class="dc-btn dc-btn-blue dc-btn-s" value="上周"/>
  <input type="button" id="thisWeekBtn" class="dc-btn dc-btn-blue dc-btn-s" value="本周"/>
  
//js
//在线时间
 var yesterDayBtn = $("#yesterDayBtn"),
 toDayBtn = $("#toDayBtn"),
 preWeekBtn = $("#preWeekBtn"),
 thisWeekBtn = $("#thisWeekBtn"),
 starTime = $("starTime"),
 endTime = $("endTime");
 
 //提交日期
 function subData(star,end){
 starTime.val(star);
 endTime.val(end);
 }
 
 //今天
 toDayBtn.on('click',function(){
 var star = getNowDate(0);
 var end = getNowDate(1);
 subData(star,end);
 });
 
 //昨天
 yesterDayBtn.on('click',function(){
 var star = getYesDate(0);
 var end = getYesDate(1);
 subData(star,end);
 });
 
 //上周
 preWeekBtn.on('click',function(){
 var star = getPreWeekStarDate();
 var end = getPreWeekStarDate();
 subData(star,end);
 });
 
 //本周
 thisWeekBtn.on('click',function(){
 var star = getWeekStarDate();
 var end = getPrreWeekEndDate();
 subData(star,end);
 });
 
//本月
thisMonthBtn.on('click',function(){
var star = getMonthStartDate();
var end = getMonthEndDate();
});

//上月
preMonthBtn.on('click',function(){
var star = getLastMonthStarDate();
var end = getLastMonthEndDat();
subData(star,end);
});

var now = new Date(); //当前日期
var nowDayOfWeek = now.getDay()-1; // 今天是本周的第几天
var nowDay = now.getDate(); //当前日
var nowMonth = now.getMonth(); //当前年
nowYear += (nowYear < 2000)?1900:0;
var lastMonthDate = new Date(); //上月日期
lastMonthDate.setDate(1);
lastMonthDate.setMonth(lastMonthDate.getMonth()-1);
var lastYear = lastMonthDate.getYear();
var lastMonth = lastMonthDate.getMonth();

//格局化日期：yyyy-mm-dd
function formatDate(date,type){
 var myyear = date.getFullYear();
 var mymonth = date.getMonth()+1;
 var myweekday = date.getDate();
  if(mymonth<10){
    mymonth = "0"+mymonth;
  }
  if(myweekday <10){
  myweekday = "0" +myweekday;
  }
  if(type ==1){
    return (myyear + '-' + mymonth + '-' +myweekday + '' + '23:59:59');
    }else{
    return(myyear + '-' +mymonth + '-' + myweekday + '' + '00:00:00');
    }
}

//获得今天日期
function getNowDate(type){
var nowDate = new Date(nowYear,nowMonth,nowDay)
return fornatDate(nowDate,type);
}

//获得昨日日期
function getYesDate(type){
var yesDate = new Date(nowYear,nowMonth,nowDay-1);
return formatDate(yesDate,type);
}

//获得上周的开端日期
function getPreWeekStarDate(){
var preWeekStartDate = new Date(nowYear,nowMonth,nowDay-(nowDayOfWeek +7));
return fornatDate(preWeekStartDate,0);
}

//获得上周的停止日期
function getPrreWeekEndDate(){
var PreweekEndDate = new Date(nowYear,nowMonth,nowDay-(nowDayOfWeek+1));
return formatDate(PreweekEndDate,1);
}

//获得本周的开端日期 
function getWeekStartDate() {
var weekStartDate = new Date(nowYear, nowMonth, nowDay - nowDayOfWeek);
return formatDate(weekStartDate, 0);
}

//获得本周的停止日期 
function getWeekEndDate() {
var weekEndDate = new Date(nowYear, nowMonth, nowDay + (6 - nowDayOfWeek));
return formatDate(weekEndDate, 1);
}

//获得本月的开端日期 
function getMonthStartDate() {
var monthStartDate = new Date(nowYear, nowMonth, 1);
return formatDate(monthStartDate, 0);
}

//获得本月的停止日期
function getMonthEndDate() {
var monthEndDate = new Date(nowYear, nowMonth, getMonthDays(nowMonth));
return formatDate(monthEndDate, 1);
}

//获得上月开端时候 
function getLastMonthStartDate() {
var lastMonthStartDate = new Date(nowYear, lastMonth, 1);
return formatDate(lastMonthStartDate, 0);
}

//获得上月停止时候 
function getLastMonthEndDate() {
var lastMonthEndDate = new Date(nowYear, lastMonth, getMonthDays(lastMonth));
return formatDate(lastMonthEndDate, 1);
}

//获得某月的天数 
function getMonthDays(myMonth) {
var monthStartDate = new Date(nowYear, myMonth, 1);
var monthEndDate = new Date(nowYear, myMonth + 1, 1);
var days = (monthEndDate - monthStartDate) / (1000 * 60 * 60 * 24);
return days;
}

```
