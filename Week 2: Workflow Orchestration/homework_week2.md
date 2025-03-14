Quiz Questions

Within the execution for Yellow Taxi data for the year 2020 and month 12: what is the uncompressed file size (i.e. the output file yellow_tripdata_2020-12.csv of the extract task)?  

**128.3 MB**  
~~134.5 MB~~  
~~364.7 MB~~  
~~692.6 MB~~  

What is the value of the variable file when the inputs taxi is set to green, year is set to 2020, and month is set to 04 during execution?  

~~{{inputs.taxi}}_tripdata_{{inputs.year}}-{{inputs.month}}.csv~~  
**green_tripdata_2020-04.csv**  
~~green_tripdata_04_2020.csv~~  
~~green_tripdata_2020.csv~~  

How many rows are there for the Yellow Taxi data for the year 2020?  

~~13,537.299~~  
24,648,499  
~~18,324,219~~  
~~29,430,127~~

```
select count(*)
FROM yellow_tripdata
where tpep_pickup_datetime > '2019-12-31' AND tpep_pickup_datetime < '2021-01-01';
```

How many rows are there for the Green Taxi data for the year 2020?  

~~5,327,301~~  
~~936,199~~  
1,734,051  
~~1,342,034~~  

```
select count(*)
FROM green_tripdata
where lpep_pickup_datetime > '2019-12-31' AND lpep_pickup_datetime < '2021-01-01';
```
*********************************************************************************
This question was removed  
Using dbt on the Green and Yellow Taxi data for the year 2020, how many rows are there in the fact_trips table?  

198  
~~165~~  
~~151~~  
~~203~~

```
SELECT COUNT(*)
FROM fact_trips;
```
**********************************************************************************

Question 5. Number of rows (yellow, March 2021) (1 point)  

~~1,428,092~~  
~~706,911~~    
1,925,152  
~~2,561,031~~   

```
select count(*)
FROM yellow_tripdata
Where tpep_pickup_datetime > '2021-03-01' AND tpep_pickup_datetime < '2021-03-31';
```

returns:  
1857586

How would you configure the timezone to New York in a Schedule trigger?  

~~Add a timezone property set to EST in the Schedule trigger configuration~~  
Add a timezone property set to America/New_York in the Schedule trigger configuration  
~~Add a timezone property set to UTC-5 in the Schedule trigger configuration~~  
~~Add a location property set to New_York in the Schedule trigger configuration~~

```
Timezone
By default, Kestra will handle all dates using your system's timezone. You can change the timezone using the user.timezone JVM option.

Changing the timezone will mostly affect:

scheduler: by default, all schedule dates are UTC; changing the Java timezone will allow scheduling the flow in your timezone.
logs display: in your configured timezone.
```


