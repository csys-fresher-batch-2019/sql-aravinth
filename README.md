# ReserveMe
### >https://ReserveMe.in

## Features
  ### >users can be able to view all trains.
## Feature 1: list of all trains
```sql
   create table train_lists(
   train_num number ,
   train_name varchar2(50) not null,
   source_station varchar2(50) unique,
   destination_station varchar2(50) unique,
   class varchar2(50),
   constraints train_num_pk primary key(train_num),
   constraints class_ck check(class in ('non-ac-sleeper','non-ac-seater','ac-sleeper','ac-seater')));
   ```
   ## Feature 2:necessary details of passenger
   ```sql
   create table passanger_details(
   passenger_name varchar2(50) not null,
   passenger_age number not null,
   passenger_gender char(1) not null,
   constraints gender_ck check (passenger_gender in ('M','F','O')));
   ```
