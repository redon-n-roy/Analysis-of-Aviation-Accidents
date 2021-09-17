# Analyzing the aviation accidents dataset using Apache Hive

## Project Description

The project dealt with the analysis of the historical data related to the accidents that has occurred in the aviation sector and tried to obtain valuable insights from the dataset. All of these is done by querying the data within Hive with HQL and also applying the necessary operations and aggregations on the data that is being queried.

## Technologies Used

* HDP 2.6.5
* Hive 2.1.0
* Hadoop 2.7.3
* Sqoop 1.4.6
* MySQL
* Git/GitHub  

## Features

A few of the insights got from the analysis were:-
* What phase of the flight do most of the accidents occur?
* Which make of the aircraft suffered the most accidents?
* What is the influence of weather on these accidents?
* What phase resulted in fatal accidents?

## Getting Started
   
* Make sure that the virtualization is enabled for your system from the BIOS.
* Install VMware Workshation Player.
* Download and insatll Hortonworks HDP 2.6.5.
* Get everything up and runninng.
* Connect to the system either through the webshell/OpenSSH/PuTTY.
* Upload all the required files into the local system or clone this repo using the following command:-
```
git clone https://github.com/redon-n-roy/Analysis-of-Aviation-Accidents.git
```

## Usage

To run the hive queries, use the Hive shell

Use the Sqoop commands to load the data into MySQL
`sqoop export --connect jdbc:mysql://localhost:3306/<DB Name> -username <user> -password <pass> -table <table_name> -m 1 --export-dir /path/to/dir --input-fields-terminated-by ',';`

To run the MySQL queries, use the MySQL shell 
`mysql -u<username> -p<password>`

# License

 This project uses the [MIT](./LICENSE) license.

# References
 [Dataset](https://www.kaggle.com/prathamsharma123/aviation-accidents-and-incidents-ntsb-faa-waas)
