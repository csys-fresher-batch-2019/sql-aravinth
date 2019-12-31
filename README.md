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
   class varchar2(50),
   constraint train_num_pk primary key(train_num),
   constraint class_ck check(class in ('non-ac-sleeper','non-ac-seater','ac-sleeper','ac-seater')),
   constraint source_dest_ck check(source_station<>destination_station));
   
   insert into  train_lists(train_num,train_name,source_station,destination_station,class)values
   (123,'indian express','chennai','covai','sleeper');
   insert into  train_lists(train_num,train_name,source_station,destination_station,class)values
   (321,'sahapthi express','covai','madurai','non-ac-sleeper');
   insert into  train_lists(train_num,train_name,source_station,destination_station,class)value
   (467,'dindugal express','chengalpattu','chennai','ac-seater');
   insert into  train_lists(train_num,train_name,source_station,destination_station,class)value
   (426,'covai express','chennai','covai','ac-seater');   
   
| s.no | train_num | train_name       | source_station | destination_station | class          |
|------|-----------|------------------|----------------|---------------------|----------------|
| 1    | 123       | indian express   | chennai        | covai               | ac-sleeper     |
| 2    | 321       | sahapthi express | covai          | madurai             | non-ac-sleeper |
| 3    | 467       | dindugal express | chengalpattu   | chennai             | ac-sleeper     |
| 4    | 426       | covai express    | chennai        | covai               | ac-sleeper     |
```
