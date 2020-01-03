# ReserveMe
### >https://ReserveMe.in

## Features
  ### >users can be able to view all trains.
## Feature 1: list of all trains

```sql
   create table train_lists(
   train_num number ,
   train_name varchar2(50) not null unique,
   source_station varchar2(50) ,
   destination_station varchar2(50),
   constraint train_num_pk primary key(train_num),
   constraint source_dest_ck check(source_station<>destination_station));
   
   insert into  train_lists(train_num,train_name,source_station,destination_station,class)values
   (123,'indian express','chennai','covai');
   insert into  train_lists(train_num,train_name,source_station,destination_station,class)values
   (321,'sahapthi express','covai','madurai');
   insert into  train_lists(train_num,train_name,source_station,destination_station,class)value
   (467,'dindugal express','chengalpattu','chennai');
   insert into  train_lists(train_num,train_name,source_station,destination_station,class)value
   (426,'covai express','chennai','covai');   
```   
| s.no | train_num | train_name       | source_station | destination_station |
|------|-----------|------------------|----------------|---------------------|
| 1    | 123       | indian express   | chennai        | covai               |
| 2    | 321       | sahapthi express | covai          | madurai             |
| 3    | 467       | dindugal express | chengalpattu   | chennai             |
| 4    | 426       | covai express    | chennai        | covai               |

## Feature 2: Passanger information
```sql
   create table passenger_details(
   train_num number,
   p_name varchar2(50) not null,
   p_id number,
   no_of_tickets number not null,
   p_age number not null,
   p_gender char(1) not null,
   p_contact number(10) not null,
   constraints train_num_fk foreign key(train_num) references train_lists(train_num),
   constraints p_id primary key(p_id),
   constraints p_age_ck check(p_age>=1),
   constraints p_gender_ck check(p_gender in('M','F','O')),
   constraints no_of_tickets check(no_of_tickets>=1),
   constraints p_contact_ck check(p_contact>999999999));
   create sequence p_id
   start with 1000
   increment by 1
   insert into passenger_details(train_num,p_name,p_id,no_of_tickets,p_age,p_gender,p_contact) values (123,'Aravinth',p_id.nextval,5,33,'M',8531946805);
   insert into passenger_details(train_num,p_name,p_id,no_of_tickets,p_age,p_gender,p_contact) values (321,'sahana',p_id.nextval,6,19,'F',9876543210);
   insert into passenger_details(train_num,p_name,p_id,no_of_tickets,p_age,p_gender,p_contact) values (123,'praveen',p_id.nextval,7,60,'M',8765432190);
   insert into passenger_details(train_num,p_name,p_id,no_of_tickets,p_age,p_gender,p_contact) values (426,'amrish',p_id.nextval,34,45,'M',7890654673);
   select * from passenger_details where train_num = 123;
```   
| s.no | train_num | p_nmae   | p_id | n0.of.tickets  | p_age | p_gender | p_contact  |
|------|-----------|----------|------|----------------|-------|----------|------------|
| 1    | 123       | Aravinth | 1000 | 5              | 33    | M        | 8531946805 |
| 2    | 321       | sahana   | 1001 | 6              | 19    | F        | 9876543210 |
| 3    | 123       | praveen  | 1002 | 7              | 60    | M        | 8765432190 |
| 4    | 426       | amrish   | 1003 | 34             | 45    | M        | 7890654673 |

## Feature 3: Seat Availabilities
```sql
 create table seat_availabilities(
   train_num number,
   tot_no_of_seats number not null,
   no_of_seats_available number not null,
   constraints train_num_fk1 foreign key(train_num) references train_lists (train_num));
   insert into seat_availabilities(train_num,tot_no_of_seats,no_of_seats_available) values(123,200,50);
   insert into seat_availabilities(train_num, tot_no_of_seats, no_of_seats_available) values(123,500,10);
   insert into seat_availabilities( train_num, tot_no_of_seats, no_of_seats_available) values( 467,450,50);
   insert into seat_availabilities( train_num, tot_no_of_seats, no_of_seats_available) values( 426,250,25);
```   
| s.no | train.num | tot.no.of.seats | available.seats |
|------|-----------|-----------------|-----------------|
| 1    | 123       | 200             | 50              |
| 2    | 321       | 500             | 10              |
| 3    | 467       | 450             | 40              |
| 4    | 426       | 250             | 25              |
## Feature 4: Train timings
```sql
   create table train_timings(
   p_id number,
   departure_time timestamp not null,
   arrival_time timestamp not null,
   constraints p_id_fk foreign key(p_id) references passenger_details(p_id));
   insert into train_timings(p_id,departure_time,arrival_time) values(1020,to_date('05-01-2020 10:00:00AM','dd-mm-yyyy hh:mi:ssPM'),
   to_date('06-01-2020 12:00:00PM','dd-mm-yyyy hh:mi:ssAM'));
   insert into train_timings(p_id,departure_time,arrival_time) values(1021,to_date('05-01-2020 12:00:00AM','dd-mm-yyyy hh:mi:ssAM'),
   to_date('07-01-2020 11:00:00AM','dd-mm-yyyy hh:mi:ssPM'));
   insert into train_timings(p_id,departure_time,arrival_time) values(1022,to_date('06-01-2020 11:00:00PM','dd-mm-yyyy hh:mi:ssPM'),
   to_date('06-01-2020 06:00:00AM','dd-mm-yyyy hh:mi:ssAM'));
   insert into train_timings(p_id,departure_time,arrival_time) values(1023,to_date('05-01-2020 03:00:00AM','dd-mm-yyyy hh:mi:ssAM'),
   to_date('06-01-2020 05:00:00PM','dd-mm-yyyy hh:mi:ssPM'));
   alter table train_timings add booked varchar2(10);
   update train_timings set booked = 'reserved' where p_id = 1020;
   update train_timings set booked = 'reserved' where p_id = 1021;
   update train_timings set booked = 'reserved' where p_id = 1022;
   update train_timings set booked ='cancelled' where p_id = 1023;
   select *from train_timings;
```
| s.no | p_id | departure time         | arrival time           | booked      |
|------|------|------------------------|------------------------|-------------|
| 1    | 1020 | 05-01-2020 10:00:00 AM | 06-01-2020 12:00:00PM  | reserved    |
| 2    | 1021 | 05-01-2020 12:00:00 AM | 07-01-2020 11:00:00AM  | reserved    |
| 3    | 1022 | 06-01-2020 11:00:00 PM | 06-01-2020 06:00:00 AM | reserved    |
| 4    | 1023 | 05-01-2020 03:00:00 AM | 06-01-2020 05:00:00 PM | cancelled   |


 ---scenerioo---
   ### Admin update---
   ### train_lists--
   ```sql
    select* from train_lists;
    
    select* from train_lists where source_station='chennai' and destination_station = 'covai'; 
   ```
    ### Passenger_details----
    ```sql
     select * from passenger_details p,train_lists t where p.train_num = p.train_num and source_station='chennai' and     destination_station = 'covai';
     
    ### male passenger----
```sql
select * from passenger_details where p_gender='M';
### Female passenger----
select * from passenger_details where p_gender='F';
```
------------------------------------------------------------------------------

### inner join query
```sql
select p.p_name,p.p_id,l.train_name,source_station,destination_station,p_gender from train_lists l,passenger_details p where l.train_num=p.train_num;
```
### outer join query
```sql
select * from train_lists l left outer join passenger_details p on l.train_num=p.train_num;
select * from train_lists l right outer join passenger_details p on l.train_num=p.train_num;
```
### update train_lists
```sql
 insert into  train_lists(train_num,train_name,source_station,destination_station,class)values
   (146,'andhara express','vaishak','delhi');
```   

   ### to check the remaining tickets----  
   ```sql
  CREATE OR REPLACE FUNCTION SEATS_AVAILABILITY(i_train_num IN number)
RETURN NUMBER AS 
remaining_seats number;
booked_seats number;
maximum_seats number;
BEGIN
select no_of_seats_available into maximum_seats from seat_availabilities where train_num=i_train_num;
select sum(no_of_tickets) into booked_seats from passenger_details where train_num=i_train_num;
remaining_seats := maximum_seats - booked_seats;
  RETURN remaining_seats;
END SEATS_AVAILABILITY;
select SEATS_AVAILABILITY(323)from dual;
```
-----------------------------------------------------------------------------
### male passenger----
```sql
select * from passenger_details where p_gender='M';
### Female passenger----
select * from passenger_details where p_gender='F';
```
------------------------------------------------------------------------------

### inner join query
```sql
select p.p_name,p.p_id,l.train_name,source_station,destination_station,p_gender from train_lists l,passenger_details p where l.train_num=p.train_num;
```
### outer join query
```sql
select * from train_lists l left outer join passenger_details p on l.train_num=p.train_num;
select * from train_lists l right outer join passenger_details p on l.train_num=p.train_num;
```
### update train_lists
```sql
 insert into  train_lists(train_num,train_name,source_station,destination_station,class)values
   (146,'andhara express','vaishak','delhi');
```   
