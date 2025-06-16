# Putting it All Together

## Progress Diagram

![Final progress diagram](images/final-progress-diagram.jpg)

## Happy Path

* Change feed + Functions to forward to a new Event Hub, or modify CreateRating function with a new second output binding to Event Hub
* Create Stream Analytics solution with original POS Event Hubs & new new Event Hub as input
* Write one or more Stream Insight queries then output to Cosmos or to PowerBI. Example:

```sql
WITH
Products AS (
    Select *
    from testdata as t
    CROSS APPLY GetArrayElements(t.items) AS flat
)

SELECT System.TimeStamp AS WindowEnd,
        T.header.locationname,
        flat.ArrayValue.productname,
        sum(flat.ArrayValue.totalcost) as totalCost,
        count(1) as countUnits
INTO prodPowerBi
FROM Products
GROUP BY flat.ArrayValue.productname, T.header.locationname, TumblingWindow(minute, 5)
```
