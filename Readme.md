# MySQL Installation Steps

```sh
$ sudo apt update
$ sudo apt upgrade
$ sudo apt install mysql-server
$ mysql --version
$ sudo mysql_secure_installation
$ sudo mysql -u root
```
You may Face Challanges In this command execution :

```sh 
$ sudo mysql_secure_installation 
```
Selet Password Number 0 = low , 1 = medium, 2 = strong 
You just Press 0 then type y y y y (given below images explain more easier)


Step # 1:

![](https://github.com/SUDOARSDEV/MySQL/blob/main/install_step_1.png)


Step # 2:

![](https://github.com/SUDOARSDEV/MySQL/blob/main/install_step_2.png)


Step # 3:

![](https://github.com/SUDOARSDEV/MySQL/blob/main/install_step_3.png)


Step # 4:

![](https://github.com/SUDOARSDEV/MySQL/blob/main/install_step_4.png)



### List of MySQL Concept:

* Database Creation
* Table Creation
* Keys Concept
* Basic Queries (Insert, Update, Delete, Select)
* Important Queries
* Aggregate Functions
* Procedures Using Delimiters
* Functions Using Delimiters
* Triggers Using Delimiters


#### Database Creation
```sh
$ Create Database Admin;
$ Use Admin;
```

#### Table Creation 
```sh
$ Create Table users(Uid int NOT NULL,Name Varchar(45) NOT NULL,Password Varchar(35) NOT NULL);
$ Create Table dashboards(Did int Not Null,Panel Varchar(45) Not Null);
$ Create table user_dashboard(Uid int NOT NULL,Did int NOT NULL);
```
![](https://github.com/SUDOARSDEV/MySQL/blob/main/1.png)



#### Keys (Primary, Foreign, Composite)
```sh
$ alter table Users add constraint pk Primary key(Uid);
$ alter table Dashboards add constraint pk1 Primary key(Did);
$ alter table User_Dashboard add constraint fk foreign key(Uid) references Users(Uid);
$ alter table User_Dashboard add constraint fk1 foreign key(Did) references Dashboards(Did);
$ alter table User_Dashboard add constraint pk2 Primary key(Uid,Did);
```
![](https://github.com/SUDOARSDEV/MySQL/blob/main/2.png)

#### Basic Queries (Insert, Update, Delete, Select)
```sh
$ Insert INTO users(Uid,Name,Password) Values(1001,'Barry','admin');
$ Insert INTO dashboards(Did,Panel) Values(1,'dashboard_1');
$ Insert INTO user_dashboard(Uid,Did) Values(1001,1);
$ Select * From users;
$ Select * From dashboards;
$ Select * From user_dashboard;
$ Update users Set Name='Alex' Where Uid='1001';
$ Delete from user_dashboard where Uid = 1001;
```

#### Important Queries
![](https://github.com/SUDOARSDEV/MySQL/blob/main/3.png)
```sh
$ Select Name,Uid from users where users.Uid = 1001 And users.Name = 'Dashborad_1';
$ Select Name from users where users.Uid = 1001 OR users.Uid = 1002;
$ Select Name from users where Uid Between 1001 and 1003;
$ Select users.Uid from users where users.Name Like 'B%' or '___';
$ select Uid from users union select Did from dashboards;
$ Select * From users,dashboards,user_dashboard; 
$ Select users.Name,dashboards.Panel from users,dashboards,user_dashboard where user_dashboard.Uid=users.Uid and user_dashboard.Did=dashboards.Did;
$ Select u.Name,d.Panel from users u inner join user_dashboard ud on ud.Uid = u.Uid inner join dashboards d on d.Did=ud.Did;
$ Select u.Name,d.Panel from users u left join user_dashboard ud on ud.Uid = u.Uid left join dashboards d on d.Did=ud.Did;
$ Select u.Name,d.Panel from users u right join user_dashboard ud on ud.Uid = u.Uid right join dashboards d on d.Did=ud.Did;
```

####  Aggregate Functions
![](https://github.com/SUDOARSDEV/MySQL/blob/main/4.png)
```sh
$ Select count(*) from users;
$ Select max(Uid) from users;
$ Select min(Uid) from users;
$ Select avg(Uid) from users;
$ Select sum(Uid) from users;
```

####  Procedures Using Delimiters
![](https://github.com/SUDOARSDEV/MySQL/blob/main/5.png)
![](https://github.com/SUDOARSDEV/MySQL/blob/main/6.png)
![](https://github.com/SUDOARSDEV/MySQL/blob/main/7.png)
```sh
$ $ Delimiter ??
$ create procedure p1()
$ Begin
$ select * from users;
$ End ??
$ Delimiter ;
$ call p1();
```
* Syntax  ‘in’ parameter:
```sh
$ Delimiter @@
$ create procedure p2(in myId int)
$ Begin
$ select Name from users where Uid=myId;
$ End @@
$ Delimiter ;
$ call p2(1001);
```
* Using ‘out’ parameter:
```sh
$ Delimiter !!
$ create procedure p3(in myId int, out myName varchar(50))
$ Begin
$ select Name into myName from users where Uid=myId;
$ End !!
$ Delimiter ;
$ call p3(1001,@m);
4 select @m;
```

####  Functions Using Delimiters

![](https://github.com/SUDOARSDEV/MySQL/blob/main/8.png)
```sh
$ Delimiter !!
$ Create Function MyQueries()
$ Returns varchar(50)
$ Begin
$ Declare var varchar(50);
$ Set var = “Select * From users”;
$ Return var;
$ End !!
$ Delimiter;
$ Select MyQueries();
```

####  Triggers Using Delimiters

![](https://github.com/SUDOARSDEV/MySQL/blob/main/9.png)
```sh
$ delimiter @#@
$ create trigger bins
$ before insert on users for each row
$ begin
$ if new.Password != 'admin' Then set new.Password = 'admin';
$ end if;
$ end @#@
$ insert INTO users(Name,Password) Values('Eliza','nice');
```
