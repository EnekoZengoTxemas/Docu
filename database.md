---
layout: page
title: Database
---
# Create 2 databases:
First, we created two databases. On the one hand, non-relational MongoDB and on the other hand relational, in this case, we have used MariaDB.

## Non-relational database data(MongoDB):
### Identification and Time
_id: Single document identifier in the database. This succession of letters and numbers distinguishes this record from all the others.

timestamp: Shows the exact time of measurement: February 12, 2026, at 10:50 a.m.

### Location and Device:
siteId ("PLANT-EIBAR-01" or "PLANT-EIBAR-02"): Installation where data has been collected. In this case, it looks like Eibar's 01 factory.

SensorId ("FLOW-METER-78" or "FLOW-METER-77"): The exact device that made the measurement; it is a flow meter (number 78).

Status: Indicates that the sensor or system is in good condition at the time, without any problems.

### Technical Measurements:
FlowRate_Lpm: Shows how many liters per minute are passing

Pressure_bar:  Shows how much pressure there is in the system.

Ph_Level: Shows the acidity/alkalinity of the liquid.


![](images/DataBase_MongoDB.png)



## Relational database data(MariaDB):
The water_plants database is a relational system exported as a JSON structure, designed to manage industrial water monitoring infrastructure and telemetry. It is organized into three primary tables that maintain data integrity through specific relational rules and hierarchical constraints.

The foundation of the database is the sites table, which acts as a master registry for physical locations, uniquely identifying facilities like PLANT-EIBAR-01. Linked to this is the sensors table, which assigns specific hardware models to those sites, ensuring that every active sensor is tied to a valid plant location. Finally, the site_hourly_stats table serves as the primary data log, storing aggregated measurements for flow rate, pH levels, and pressure. This table follows a strict internal logic where the recorded minimum, average, and maximum values for each hour must maintain a consistent mathematical relationship to ensure statistical accuracy.

![](images/MySql_DataBase.png)


#Data abstraction from a non-relational database to a relational database:

##Query for MongoDB:
db.data.aggregate([
  {
    //1. Filter the whole last hour.
    $match: {
      timestamp: {
        $gte: new Date(new Date().setHours(new Date().getHours() - 1, 0, 0, 0)),
        $lte: new Date(new Date().setHours(new Date().getHours() - 1, 59, 59, 999))
      }
    }
  },
  {
    //2. Grouping and calculating statistics
    $group: {
      _id: {
        siteId: "$siteId",
        rango_horario: { $dateTrunc: { date: "$timestamp", unit: "hour" } }
      },
      flow_avg: { $avg: "$flowRate_Lpm" },
      flow_min: { $min: "$flowRate_Lpm" },
      flow_max: { $max: "$flowRate_Lpm" },
      ph_avg: { $avg: "$phLevel" },
      ph_min: { $min: "$phLevel" },
      ph_max: { $max: "$phLevel" },
      pressure_avg: { $avg: "$pressure_bar" },
      pressure_min: { $min: "$pressure_bar" },
      pressure_max: { $max: "$pressure_bar" }
    }
  },
  {
  //3. Project and round areas (equivalent to ToFix (2))
    $project: {
      _id: 0,
      site_id: "$_id.siteId",
      rango_horario: "$_id.rango_horario",
      flow_avg: { $round: ["$flow_avg", 2] },
      flow_min: 1,
      flow_max: 1,
      ph_avg: { $round: ["$ph_avg", 2] },
      ph_min: 1,
      ph_max: 1,
      pressure_avg: { $round: ["$pressure_avg", 2] },
      pressure_min: 1,
      pressure_max: 1
    }
  }
])

