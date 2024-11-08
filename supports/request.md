// DAX Query
DEFINE
	VAR __DS0FilterTable = 
		TREATAS({"2018-11"}, 'Date'[Month])

	VAR __DS0Core = 
		SUMMARIZECOLUMNS(
			ROLLUPADDISSUBTOTAL(
				ROLLUPGROUP('Date'[Date], 'Reseller Sales'[Order Number], 'Product'[Product]), "IsGrandTotalRowTotal"
			),
			__DS0FilterTable,
			"Sales", 'Reseller Sales'[Sales]
		)

	VAR __DS0PrimaryWindowed = 
		TOPN(
			502,
			__DS0Core,
			[IsGrandTotalRowTotal],
			0,
			'Reseller Sales'[Order Number],
			1,
			'Date'[Date],
			1,
			'Product'[Product],
			1
		)

EVALUATE
	__DS0PrimaryWindowed

ORDER BY
	[IsGrandTotalRowTotal] DESC,
	'Reseller Sales'[Order Number],
	'Date'[Date],
	'Product'[Product]


// Direct Query

SELECT 
TOP (1000001) *
FROM 
(

SELECT [t0].[Date] AS [c1],[t1].[Product] AS [c7],[t2].[Order Number] AS [c15],SUM([t2].[SalesAmount])
 AS [a0]
FROM 
(
((
select [SalesOrderNumber] as [Order Number],
    [SalesOrderLineNumber] as [Order Line],
    [OrderDate] as [OrderDate],
    [ProductKey] as [ProductKey],
    [SalesAmount] as [SalesAmount]
from [dbo].[FactResellerSales] as [$Table]
) AS [t2]

 INNER JOIN 

(
select [_].[FullDateAlternateKey] as [Date],
    [_].[t0_0] as [Fiscal Year],
    convert(nvarchar(max), [_].[Fiscal Quarter]) as [Fiscal Quarter],
    [_].[t2_0] as [Month]
from 
(
    select [_].[FullDateAlternateKey] as [FullDateAlternateKey],
        [_].[MonthNumberOfYear] as [MonthNumberOfYear],
        [_].[CalendarYear] as [CalendarYear],
        [_].[FiscalQuarter] as [FiscalQuarter],
        [_].[FiscalYear] as [FiscalYear],
        [_].[Fiscal Year] as [Fiscal Year],
        [_].[Month] as [Month],
        ([_].[Fiscal Year] + ' Q') + convert(nvarchar(max), [_].[FiscalQuarter]) as [Fiscal Quarter],
        convert(nvarchar(max), [_].[Fiscal Year]) as [t0_0],
        convert(nvarchar(max), [_].[Month]) as [t2_0]
    from 
    (
        select [_].[FullDateAlternateKey] as [FullDateAlternateKey],
            [_].[MonthNumberOfYear] as [MonthNumberOfYear],
            [_].[CalendarYear] as [CalendarYear],
            [_].[FiscalQuarter] as [FiscalQuarter],
            [_].[FiscalYear] as [FiscalYear],
            'FY' + convert(nvarchar(max), [_].[FiscalYear]) as [Fiscal Year],
            ((convert(nvarchar(max), [_].[CalendarYear]) + '-') + (case
                when [_].[MonthNumberOfYear] < 10
                then '0'
                else ''
            end)) + convert(nvarchar(max), [_].[MonthNumberOfYear]) as [Month]
        from 
        (
            select [FullDateAlternateKey],
                [MonthNumberOfYear],
                [CalendarYear],
                [FiscalQuarter],
                [FiscalYear]
            from [dbo].[DimDate] as [$Table]
        ) as [_]
    ) as [_]
) as [_]
) AS [t0] on 
(
[t2].[OrderDate] = [t0].[Date]
)
)


 INNER JOIN 

(
select [$Outer].[ProductKey] as [ProductKey],
    [$Outer].[EnglishProductName] as [Product],
    [$Outer].[Color] as [Color],
    [$Outer].[EnglishProductSubcategoryName] as [Subcategory],
    [$Inner].[EnglishProductCategoryName] as [Category]
from 
(
    select [$Outer].[ProductKey] as [ProductKey],
        [$Outer].[ProductSubcategoryKey2] as [ProductSubcategoryKey2],
        [$Outer].[EnglishProductName] as [EnglishProductName],
        [$Outer].[Color] as [Color],
        [$Inner].[EnglishProductSubcategoryName] as [EnglishProductSubcategoryName],
        [$Inner].[ProductCategoryKey] as [ProductCategoryKey2]
    from 
    (
        select [_].[ProductKey] as [ProductKey],
            [_].[ProductSubcategoryKey] as [ProductSubcategoryKey2],
            [_].[EnglishProductName] as [EnglishProductName],
            [_].[Color] as [Color]
        from [dbo].[DimProduct] as [_]
        where [_].[FinishedGoodsFlag] = 1
    ) as [$Outer]
    left outer join [dbo].[DimProductSubcategory] as [$Inner] on ([$Outer].[ProductSubcategoryKey2] = [$Inner].[ProductSubcategoryKey])
) as [$Outer]
left outer join [dbo].[DimProductCategory] as [$Inner] on ([$Outer].[ProductCategoryKey2] = [$Inner].[ProductCategoryKey])
) AS [t1] on 
(
[t2].[ProductKey] = [t1].[ProductKey]
)
)

WHERE 
(
[t0].[Month] = N'2018-11'
)

GROUP BY [t0].[Date],[t1].[Product],[t2].[Order Number]
)
 AS [MainTable]
WHERE 
(

NOT(
(
[a0] IS NULL 
)
)

)
 
