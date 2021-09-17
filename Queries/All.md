## Creating the database

```
create database aviation;
```

```
use aviation;
```

## Creating and Loading the Hive table

```
create table accidents(investigation_type string, event_date date, injury_severity string, aircraft_damage string, aircraft_category string, make string, model string, purpose_of_flight string, fatal_injuries int, serious_injuries int, minor_injuriesries int, uninjured int, weather_condition string, phase_of_flight string) row format delimited fields terminated by '\t';
```

```
load data local inpath '/root/Aviation.txt' into table accidents;
```

## Finding Phase having most accidents 

```
select phase_of_flight, count(phase_of_flight) as total_count from accidents group by phase_of_flight order by total_count desc;
```

## Finding Phase having most Fatal accidents

```
select phase_of_flight,count(phase_of_flight) as TC from accidents where injury_severity='Fatal' group by phase_of_flight order by TC desc;
```

## Finding Make of Airplane having most accidents

```
select make,count(injury_severity) as injury_count from accidents where aircraft_category='Airplane' group by make order by injury_count desc limit 10;
```

## Finding number of fatalities for each phase

```
select sum(fatal_injuries) as SoI,phase_of_flight from accidents group by phase_of_flight order by SoI desc;
```

## Finding the make that was destroyed the most in accidents

```
select make, count(make) as mk from accidents where aircraft_damage='Destroyed' group by make order by mk desc limit 10;
```

## Finding the effect of weather conditions in accidents

```
select weather_condition,count(weather_condition) as wc from accidents where injury_severity='Fatal'group by weather_condition order by wc desc;
```

## Creating a table for dynamic partitioning

```
create table accidents_pt(investigation_type string, event_date date, aircraft_damage string, aircraft_category string, make string, model string, purpose_of_flight string, fatal_injuries int, serious_injuries int, minor_injuriesries int, uninjured int, weather_condition string) partitioned by(injury_severity string, phase_of_flight string);
```

```
set hive.exec.dynamic.partition.mode=nonstrict;
```

## Inserting data into partition table

```
insert into table accidents_pt partition(injury_severity,phase_of_flight) select investigation_type, event_date, aircraft_damage, aircraft_category, make, model, purpose_of_flight, fatal_injuries, serious_injuries, minor_injuriesries, uninjured, weather_condition,injury_severity, phase_of_flight from accidents;
```

## Displaying the partitions

```
show  partitions accidents_pt;
```

## Running same query on partition table and normal table

```
select count(*) from accidents_pt where injury_severity='Fatal' and phase_of_flight='Approach';
```

```
select count(*) from accidents where injury_severity='Fatal' and phase_of_flight='Approach';
```

## Exporting query result into HDFS

```
insert overwrite directory '/accident_data' row format delimited fields terminated by ',' stored as textfile select phase_of_flight, count(phase_of_flight) as total_count from accidents group by phase_of_flight order by total_count desc;
```

## Writing the query result into MySQL with Sqoop

```
sqoop export --connect jdbc:mysql://localhost:3306/aviation_accidents -username root -password hortonworks1 -table accident_phase -m 1 --export-dir /accident_data/000000_0 --input-fields-terminated-by ',';
```

##  Displaying the query result written into MySQL

```
select * from accident_phase;
```
