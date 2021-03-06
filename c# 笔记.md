Get the Calendar of your ZonedDateTime and then call the GetDaysInMonth(year, month) method:

```
ZonedDateTime mstNow = now.InZone(mst);
CalendarSystem calendar = mstNow.Calendar;
LocalDate mstLastDayOfCurrentMonth = new LocalDate(
    mstNow.Year, mstNow.Month, calendar.GetDaysInMonth(mstNow.Year, mstNow.Month));
```

You can use the .NET DateTime functionality to achieve this. I think you can plug this into your NodaTime code to get the last day of current month and last day of following month:

```
 DateTime today = DateTime.Today;
    DateTime currentYearMonth = new DateTime(today.Year, today.Month, 1);
    DateTime lastDayCurrentMonth = currentYearMonth.AddMonths(1).AddDays(-1);
    DateTime lastDayNextMonth = currentYearMonth.AddMonths(2).AddDays(-1);

    // This is just to illustrate end of year compatibility
    DateTime december = new DateTime(2014, 12, 1);
    DateTime lastDayDecember = december.AddMonths(1).AddDays(-1);
    DateTime lastDayJanuary = december.AddMonths(2).AddDays(-1);
```

Hi you could also use the function "DaysInMonth" of "DateTime" object, like this.
```
DateTime today = DateTime.Today;
int lastDayOfCurrMonth = DateTime.DaysInMonth(today.Year, today.Month); // which return from 1 to 31, according to the month

DateTime nextMonth = today.AddMonths(1);
int lastDayOfNextMonth = DateTime.DaysInMonth(nextMonth.Year, nextMonth.Month); // which return from 1 to 31, according to the month
```

```
int theMonth = ((System.DateTime)periodStartDate).AddMonths(1).Month;
```



[jqGrid使用记录](http://www.cnblogs.com/kissdodog/p/3875992.html)


[手机安装google play应用](http://www.zhihu.com/question/20232626)

```
SELECT 
DATE(begin_time) AS `Date`,
CASE 
WHEN TIME(begin_time) >= '00:00:00' AND TIME(begin_time) < '01:00:00' THEN '00:00:00 - 01:00:00' 
WHEN TIME(begin_time) >= '01:00:00' AND TIME(begin_time) < '02:00:00' THEN '01:00:00 - 02:00:00' 
/*...and so on...*/
END AS `TimeSlot`,
COUNT(id) as reservations
FROM reservation
WHERE begin_time > '" . $from . "'
AND end_time < '" . $until . "'
GROUP BY `Date`, `TimeSlot`
```


```
SELECT A.TIME1,B.YU_JIAN_CHE_LIANG_SHU FROM 
(SELECT DATE_FORMAT(DATE_FORMAT(now(),'%Y-%m-%d') - INTERVAL numlist.id HOUR,'%Y-%m-%d %H') as TIME1 from (SELECT n1.i*8 + n2.i*80 as id from num n1 cross join num as n2) as numlist) A
LEFT JOIN (SELECT CONCAT(date_format(YU_JIAN_JIAN_CE_SHI_JIAN,'%Y-%m-%d'),case when date_format(YU_JIAN_JIAN_CE_SHI_JIAN,'%H') < 8 then ' 00' when date_format(YU_JIAN_JIAN_CE_SHI_JIAN,'%H') < 16 then ' 08' else ' 16' end) as TIME1,
COUNT(*) as YU_JIAN_CHE_LIANG_SHU FROM ZCJL_R_YJSJB B WHERE YU_JIAN_JIAN_CE_SHI_JIAN > '2016-05-01' AND YU_JIAN_JIAN_CE_SHI_JIAN < '2016-05-30'
GROUP BY TIME1 ORDER BY YU_JIAN_JIAN_CE_SHI_JIAN) B on A.TIME1 = B.TIME1
```

http://www.cnblogs.com/s021368/articles/1738372.html


explain SELECT A.YU_JIAN_SHU_JU_BIAO_ID,A.CHE_PAI_HAO,A.YU_JIAN_JIAN_CE_SHI_JIAN,A.YU_JIAN_ZONG_ZHONG,A.YU_JIAN_CHAO_XIAN_LV,A.YU_JIAN_ZHOU_SHU,
A.YU_JIAN_CHE_SU,C.TAO_YI_SHI_JIAN,C.TAO_YI_BIAO_ID   
FROM ZCJL_R_YJSJB A  
INNER JOIN ZCJL_R_FTY C ON  A.CHE_PAI_HAO = C.CHE_PAI_HAO 


WHERE A.CHE_PAI_HAO <>'未识别' AND A.YU_JIAN_CHAO_XIAN_LV > 0   
AND A.YU_JIAN_JIAN_CE_SHI_JIAN< C.TAO_YI_SHI_JIAN AND date_add(A.YU_JIAN_JIAN_CE_SHI_JIAN, interval 2 hour) > C.TAO_YI_SHI_JIAN   

AND  NOT exists (SELECT 1 FROM ZCJL_R_JJSJB B WHERE a.CHE_PAI_HAO=b.CHE_PAI_HAO and A.YU_JIAN_JIAN_CE_SHI_JIAN < B.JING_JIAN_SHI_JIAN 
AND date_add(A.YU_JIAN_JIAN_CE_SHI_JIAN, interval 2 hour) > B.JING_JIAN_SHI_JIAN)   

AND  NOT exists (SELECT 1 FROM ZCJL_R_TYCLJL E WHERE A.CHE_PAI_HAO=E.CHE_PAI_HAO AND DATA_SOURCE = 3 
AND A.YU_JIAN_JIAN_CE_SHI_JIAN = E.JIAN_CE_SHI_JIAN)  

and A.YU_JIAN_JIAN_CE_SHI_JIAN >= '2016-05-25'  AND A.YU_JIAN_JIAN_CE_SHI_JIAN <= '2016-05-28'   
ORDER BY A.YU_JIAN_JIAN_CE_SHI_JIAN DESC  LIMIT 0,15; 
