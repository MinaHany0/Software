
# mySQL some orders and practise
```mysql
create table avengar(
  id int,first_name varchar(255), last_name varchar(255), origin varchar(255), age int, alias varchar(255));
  
describe avengar;

insert into avengar values
(1,"thor", "odinson", "asgard", 12500, "strongest avengar");
 insert into avengar values (2, "clint", "barlon", "earth", 55, "hawkeye");
  
insert into avengar values(3, "tony", "stark", "earth", 34, "ironman");
insert into avengar values(4 , "peter", "parker", "earth", 52, "sppiderman");
insert into avengar values(5 , "groot", "groot", "planet x", 232323, "tree");

select * from avengar where not origin = "earth";

insert into avengar values (6, "jeff", "smith", "earth", 23, "jeff the man");

select * from avengar ;
delete from avengar where first_name = "jeff";
select * from avengar ;

update avengar set last_name = null where first_name = "groot";
select * from avengar order by age asc;
select * from avengar order by age desc;

alter table avengar add beard boolean;
select * from avengar;
update  avengar set beard = false where not first_name = "thor";
update  avengar set beard = true where first_name = "thor";
select * from avengar;
```

