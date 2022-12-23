CREATE TABLE if not exists mentors (
  id                 SERIAL PRIMARY KEY,
  name               VARCHAR(30) NOT NULL,
  years_glasgow      INT NOT NULL,
  address            VARCHAR(120),
  favourite_language VARCHAR(30)
);

insert into 
	mentors 
(name, years_glasgow, address, favourite_language) values ('Lucia', 1, 'street1, 1', 'HTML');
insert into 
	mentors 
(name, years_glasgow, address, favourite_language) values ('Giorgio', 2, 'street 2, 2', 'CSS');
-- insert many values at the same time on mentor's table:
insert into 
	mentors 
(name, years_glasgow, address, favourite_language) values ('Marco', 3, 'street 3, 3', 'JavScript'), ('Camila', 4, 'street 4, 4', 'NodeJs');

create table if not exists students (
	id              SERIAL primary key,
	name            VARCHAR(30) NOT NULL,
	address         VARCHAR(120),
	graduated       boolean
);


insert into 
	students 
(name, address, graduated) values 
('Amanda', 'street 5, 5', true), 
('Danielle', 'street 6, 6', true), 
('Nuno', 'street 7, 7', true),
('Jorge', 'street 8, 8', false),
('Carlos', 'street 9, 9', false),
('Joaquina', 'street 10, 10', false), 
('Mabel', 'street 11, 11', true), 
('Jaci', 'street 12, 12', true),
('Patel', 'street 13, 13', false),
('Jadi', 'street 14, 14', false);

select * from mentors m;
select  * from students s;

select name from mentors m ;
select address from students s ;

select * from students s where 
	graduated = true ;

create table if not exists classes (
	id SERIAL primary key,
	mentor    INT references mentors(id),
	topic     VARCHAR(30) NOT NULL,
	taught_date date not null,
	class_location VARCHAR(60) not NULL
);


delete from classes 
where mentor = 1;

insert into 
	classes 
(mentor, topic, taught_date, class_location) values 
(1, 'HTML', '2022-02-19', 'Barcelona'),
(7, 'HTML', '2022-06-25', 'Barcelona'),
(6, 'HTML', '2022-09-30', 'Barcelona'),
(5, 'CSS' ,'2022-12-24', 'Barcelona');

select mentor from classes c ;

create table if not exists class_attendance (
	id SERIAL     primary key,
	student_id    INT references students(id),
	class_id      INT references classes(id)
);

insert into class_attendance(student_id, class_id)
values
	(1, 11),
	(2, 12),
	(3, 13),
	(4, 14),
	(5, 11),
	(6, 12),
	(7, 13),
	(8, 14),
	(9, 11),
	(10, 12)
;

update class_attendance 
set class_id = 11
where student_id = 10;

select * from class_attendance ca 
where class_id = 15

delete from mentors 
where id > 7;

select * from mentors m 
where years_glasgow > 2;

update mentors 
set favourite_language = 'Javascript'
where id = 6;

select * from mentors m 
where favourite_language = 'Javascript';


delete from students 
where id > 10;

select * from students s 
where graduated = true;

select * from classes c 
where taught_date 

--Retrieve all the classes taught before June this year

select * from classes c 
where taught_date < '2022-06-01';

--Retrieve all the students (retrieving student ids only is fine) who attended the Javascript class (or any other class that you have in the classes table).
select s.id, name from students s 
	left join class_attendance ca on ca.student_id = s.id 
	where class_id = 14;

