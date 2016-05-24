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


