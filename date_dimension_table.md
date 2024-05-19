
https://corporatefinanceinstitute.com/resources/data-science/creating-a-date-dimension-table/

Date | Year | Quarter | QuarterId | MonthNum | MonthName | DayOfMonth | ...

DayOfWeek | DayName ... 


Basic Date Information
DateKey (Primary key, typically in YYYYMMDD format)
Date (Full date in YYYY-MM-DD format)
Year
Quarter
QuarterName (e.g., "Q1", "Q2", etc.)
Month
MonthName (e.g., "January", "February", etc.)
MonthShortName (e.g., "Jan", "Feb", etc.)
Day
DayName (e.g., "Monday", "Tuesday", etc.)
DayShortName (e.g., "Mon", "Tue", etc.)
DayOfYear
DayOfQuarter
WeekOfYear
WeekOfMonth
WeekEndingDate (The last date of the week)
DayOfWeek (1 for Sunday, 2 for Monday, etc., or vice versa depending on your week's start day)
Fiscal Information
FiscalYear
FiscalQuarter
FiscalQuarterName (e.g., "Q1", "Q2", etc., for the fiscal year)
FiscalMonth
FiscalMonthName (e.g., "Fiscal January", "Fiscal February", etc.)
FiscalWeek
FiscalWeekOfYear
FiscalWeekOfMonth
Additional Attributes
IsWeekend (Boolean or 1 for yes, 0 for no)
IsHoliday (Boolean or 1 for yes, 0 for no)
HolidayName (Name of the holiday, if applicable)
IsBusinessDay (Boolean or 1 for yes, 0 for no)
ISO Standard Dates
ISOYear
ISOWeek
ISOYearWeek (Combination of ISO Year and Week, e.g., 2023-W01)
Hierarchical and Relative Dates
YearMonth (e.g., 2023-01)
YearQuarter (e.g., 2023-Q1)
YearWeek (e.g., 2023-W01)
PreviousDay (Date of the previous day)
NextDay (Date of the next day)
PreviousYear (Year of the previous year)
NextYear (Year of the next year)
PreviousMonth (Month of the previous month)
NextMonth (Month of the next month)
Seasonal and Miscellaneous
Season (e.g., "Winter", "Spring", etc.)
DayType (e.g., "Weekday", "Weekend", "Holiday")
WeekdayOrWeekend (e.g., "Weekday", "Weekend")
Time Zone Information (if applicable)
TimeZone (Time zone information, if relevant)
UTCOffset (Offset from UTC, if relevant)
Formatting Variations
DateString (Date in string format, e.g., "January 1, 2023")
ShortDate (Date in short format, e.g., "1/1/23")
Special Flags and Indicators
IsCurrentDay (Boolean or 1 for yes, 0 for no, indicating if the date is the current date)
IsCurrentMonth (Boolean or 1 for yes, 0 for no, indicating if the date is in the current month)
IsCurrentYear (Boolean or 1 for yes, 0 for no, indicating if the date is in the current year)
