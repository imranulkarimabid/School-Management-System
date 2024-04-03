sys as sysdba

drop user sc_ddd56 cascade ;

create      user sc_ddd56
identified  by   123
quota       unlimited on users ;

grant dba
to    sc_ddd56 ;

conn sc_ddd56/123

--===============
--user_type Table
--===============

drop table user_type cascade constraint ;

create table user_type
(
user_type_ID             number,
user_type_name           varchar2(100) constraint user_type_user_type_name_nn not null
                                       constraint user_type_user_type_name_uk unique  ,
user_type_description    varchar2(250),
action_user              varchar2(100) default user,
action_date_time         date          default sysdate
) ;

alter table user_type
add         constraint user_type_user_type_id_pk primary key(user_type_id) ;

insert into user_type (user_type_id, user_type_name) 
values (1, 'Admin') ;

insert into user_type (user_type_id, user_type_name)
values (2, 'Moderator') ;

insert into user_type (user_type_id, user_type_name)
values (3, 'Student') ;

insert into user_type (user_type_id, user_type_name)
values (4, 'Writer') ;

insert into user_type (user_type_id, user_type_name)
values (5, 'Reader') ;

insert into user_type (user_type_id, user_type_name)
values (6, 'Subscriber') ;

insert into user_type (user_type_id, user_type_name)
values (7, 'Guest') ;

insert into user_type (user_type_id, user_type_name)
values (8, 'Teacher') ;

insert into user_type (user_type_id, user_type_name)
values (9, 'Contributor') ;

insert into user_type (user_type_id, user_type_name)
values (10, 'Curator') ;

insert into user_type (user_type_id, user_type_name)
values (11, 'Mentor') ;

insert into user_type (user_type_id, user_type_name)
values (12, 'Learner') ;

commit ;


--=================
--user_status Table
--=================

drop table user_status cascade constraint ;

create table user_status
(
user_status_ID             number,
user_status_name           varchar2(100) constraint user_status_user_status_name_nn not null
                                         constraint user_status_user_status_name_uk unique  ,
user_status_description    varchar2(250),
action_user                varchar2(100) default user,
action_date_time           date          default sysdate
) ;

alter table user_status
add         constraint user_status_user_status_id_pk primary key(user_status_id) ;

insert into user_status (user_status_id, user_status_name)
values ( 1, 'Registered');

insert into user_status (user_status_id, user_status_name)
values ( 2, 'Active');  

insert into user_status (user_status_id, user_status_name)
values ( 3, 'Inactive'); 

insert into user_status (user_status_id, user_status_name)
values ( 4, 'Pending'); 

insert into user_status (user_status_id, user_status_name)
values ( 5, 'Approved'); 

insert into user_status (user_status_id, user_status_name)
values ( 6, 'Blocked'); 

insert into user_status (user_status_id, user_status_name)
values ( 7, 'Rejected'); 

insert into user_status (user_status_id, user_status_name)
values ( 8, 'Verified'); 

insert into user_status (user_status_id, user_status_name)
values ( 9, 'Unverified'); 

insert into user_status (user_status_id, user_status_name)
values ( 10, 'Suspended'); 

insert into user_status (user_status_id, user_status_name)
values ( 11, 'Deleted'); 

insert into user_status (user_status_id, user_status_name)
values ( 12, 'Invited'); 

commit ;

--==================
--branch table
--==================

drop table branch cascade constraint ;

create table branch
(
branch_id            number,
branch_name          varchar2(100)  constraint branch_branch_name_nn not null
                                    constraint branch_branch_name_uk unique,
cell_number          varchar2(100)  constraint branch_cell_number_uk unique,
branch_address       varchar2(250),
email                varchar2(150) constraint branch_email_uk unique,
branch_description   varchar2(250),
action_user          varchar2(100) default user,
action_date_time     date          default sysdate
) ;

alter table branch
add         constraint branch_branch_id_pk primary key(branch_id) ;

insert into branch (branch_id, branch_name, cell_number, branch_address, email) 
values (1, 'Dhaka Branch', '12345674890', 'Dhaka, Bangladesh', 'dhaka@abc.com');

insert into branch (branch_id, branch_name, cell_number, branch_address, email) 
values (2, 'Chittagong Branch', '09787654321', 'Chittagong, Bangladesh', 'chittagong@abc.com');

insert into branch (branch_id, branch_name, cell_number, branch_address, email) 
values (3, 'Sylhet Branch', '123456890', 'Sylhet, Bangladesh', 'sylhet@abc.com');

insert into branch (branch_id, branch_name, cell_number, branch_address, email) 
values (4, 'Rajshahi Branch', '097654321', 'Rajshahi, Bangladesh', 'rajshahi@abc.com');

insert into branch (branch_id, branch_name, cell_number, branch_address, email) 
values (5, 'Khulna Branch', '1245674890', 'Khulna,Bangladesh', 'khulna@abc.com');

insert into branch (branch_id, branch_name, cell_number, branch_address, email) 
values (6, 'Barisal Branch', '0978764321', 'Barisal Bangladesh', 'barisal@abc.com');

insert into branch (branch_id, branch_name, cell_number, branch_address,email)
values (7, 'Rangpur Branch', '1345674890', 'Rangpur Bangladesh', 'rangpur@abc.com');

insert into branch(branch_id, branch_name, cell_number, branch_address, email)
values (8, 'Mymensingh Branch', '0978754321', 'Mymensingh Bangladesh', 'mymensingh@abc.com');

insert into branch(branch_id, branch_name, cell_number, branch_address, email)
values (9, 'Comilla Branch', '1234567490', 'Comilla Bangladesh', 'comilla@abc.com');

insert into branch(branch_id, branch_name, cell_number, branch_address, email)
values (10, 'Narayanganj Branch', '0977654321', 'Narayanganj Bangladesh', 'narayanganj@abc.com');

insert into branch(branch_id, branch_name, cell_number, branch_address, email)
values (11, 'Gazipur Branch', '1234574890', 'Gazipur Bangladesh', 'gazipur@abc.com');

insert into branch(branch_id, branch_name, cell_number, branch_address, email)
values (12, 'Jessore Branch', '0978654321', 'Jessore Bangladesh', 'jessore@abc.com');

commit ;


--==================
--department table
--==================

drop table department cascade constraint ;

create table department
(
department_id          number,
department_name        varchar2(100) constraint department_department_name_nn not null
                                     constraint department_department_name_uk unique,
department_location    varchar2(100),
department_country     varchar2(100),
department_description varchar2(250),
action_user            varchar2(100) default user,
action_date_time       date default sysdate
) ;

alter table department 
add         constraint department_department_id_pk primary key(department_id) ;

insert into department (department_id, department_name, department_location, department_country) 
values (1, 'Marketing', 'Dhaka', 'Bangladesh');

insert into department (department_id, department_name, department_location, department_country) 
values (2, 'Finance', 'Chittagong', 'Bangladesh');

insert into department (department_id, department_name, department_location, department_country) 
values (3, 'Human Resources', 'Sylhet', 'Bangladesh');

insert into department (department_id, department_name, department_location, department_country) 
values (4, 'Sales', 'Rajshahi', 'Bangladesh');

insert into department (department_id, department_name, department_location, department_country) 
values (5, 'Customer Service', 'Khulna', 'Bangladesh');

insert into department (department_id ,department_name ,department_location ,department_country)
values (6 ,'IT' ,'Barisal' ,'Bangladesh');

insert into department(department_id ,department_name ,department_location ,department_country)
values(7 ,'Research and Development' ,'Rangpur' ,'Bangladesh');

insert into department(department_id ,department_name ,department_location ,department_country)
values(8 ,'Quality Assurance' ,'Mymensingh' ,'Bangladesh');

insert into department(department_id ,department_name ,department_location ,department_country)
values(9 ,'Public Relations' ,'Comilla' ,'Bangladesh');

insert into department(department_id ,department_name ,department_location ,department_country)
values(10 ,'Legal' ,'Narayanganj' ,'Bangladesh');

insert into department(department_id ,department_name ,department_location ,department_country)
values(11 ,'Administration' ,'Gazipur' ,'Bangladesh');

insert into department(department_id ,department_name ,department_location ,department_country)
values(12 ,'Logistics' ,'Jessore' ,'Bangladesh');


--=================
--designation table
--=================

drop table designation cascade constraint ;

create table designation
(
designation_id            number,
designation_name          varchar2(100) constraint designation_designation_name_nn not null
                                        constraint desigantion_designation_name_uk unique,
designation_description   varchar2(250),
action_user               varchar2(100) default user,
action_date_time          date          default sysdate
) ;

alter table designation
add         constraint designation_designation_id_pk primary key(designation_id) ;

insert into designation (designation_id, designation_name) 
values (1, 'Marketing Manager') ;

insert into designation (designation_id, designation_name) 
values (2, 'Finance Officer') ;

insert into designation (designation_id, designation_name) 
values (3, 'Human Resources Specialist') ;

insert into designation (designation_id, designation_name) 
values (4, 'Sales Representative') ;

insert into designation (designation_id, designation_name) 
values (5, 'Research and Development Director') ;

insert into designation (designation_id, designation_name) 
values (6, 'Operations Analyst') ;

insert into designation (designation_id, designation_name) 
values (7, 'Customer Service Associate') ;

insert into designation (designation_id, designation_name) 
values (8, 'Legal Counsel') ;

insert into designation (designation_id, designation_name) 
values (9, 'Production Supervisor') ;

insert into designation (designation_id, designation_name) 
values (10, 'Design Lead') ;

insert into designation (designation_id, designation_name) 
values (11, 'Engineering Manager') ;

insert into designation (designation_id, designation_name) 
values (12, 'Quality Assurance Engineer') ;

commit ;

--==================
--expense_type table
--==================

drop table expense_type cascade constraint ;

create table expense_type
(
expense_type_id             number,
expense_type_name           varchar2(100) constraint expense_type_expense_type_name_nn not null
                                          constraint expense_type_expense_type_name_uk unique  ,
expense_type_description    varchar2(250),
action_user                 varchar2(100) default user,
action_date_time            date          default sysdate
) ;

alter table expense_type
add         constraint expense_type_expense_type_id_pk primary key(expense_type_id) ;

Insert into Expense_Type ( Expense_Type_ID, Expense_Type_Name )
Values                    (1, 'Operating Expenses');

Insert into Expense_Type ( Expense_Type_ID, Expense_Type_Name )
Values                    (2, 'Cost of Goods Sold');

Insert into Expense_Type ( Expense_Type_ID, Expense_Type_Name )
Values                    (3, 'Marketing Expenses');

Insert into Expense_Type ( Expense_Type_ID, Expense_Type_Name )
Values                    (4, 'Travel Expenses');

Insert into Expense_Type ( Expense_Type_ID, Expense_Type_Name )
Values                    (5, 'Office Supplies Expenses');

Insert into Expense_Type ( Expense_Type_ID, Expense_Type_Name )
Values                    (6, 'Rent Expenses');

Insert into Expense_Type ( Expense_Type_ID, Expense_Type_Name )
Values                    (7, 'Utility Expenses');

Insert into Expense_Type ( Expense_Type_ID, Expense_Type_Name )
Values                    (8, 'Insurance Expenses');

Insert into Expense_Type ( Expense_Type_ID, Expense_Type_Name )
Values                    (9, 'Taxes Expenses');

Insert into Expense_Type ( Expense_Type_ID, Expense_Type_Name )
Values                    (10, 'Interest Expenses');

Insert into Expense_Type ( Expense_Type_ID, Expense_Type_Name )
Values                    (11, 'Depreciation Expenses');

Insert into Expense_Type ( Expense_Type_ID, Expense_Type_Name )
Values                    (12, 'Amortization Expenses');

commit ;

--==================
--expense_m table
--==================

drop table expense_m cascade constraint ;

create table expense_m
(
expense_m_id           number,
branch_id              number,
expense_date           date          constraint expense_m_expense_date_nn not null
                                     constraint expense_m_expense_date_uk unique  ,
expense_m_description  varchar2(250),
action_user            varchar2(100) default user,
action_date_time       date          default sysdate
) ;

alter table expense_m
add         constraint expense_m_expense_m_id_pk primary key(expense_m_id) ;

alter table expense_m
add         constraint expense_m_branch_id_fk foreign key(branch_id)
references  branch(branch_id) ;

insert into expense_m (expense_m_id, branch_id, expense_date)
values      (1, 2, '02-May-2020') ;

insert into expense_m (expense_m_id, branch_id, expense_date)
values      (2, 1, '02-Feb-2023') ;

insert into expense_m (expense_m_id, branch_id, expense_date)
values      (3, 5, '03-Mar-2022') ;

insert into expense_m (expense_m_id, branch_id, expense_date)
values      (4, 9, '04-Apr-2021') ;

insert into expense_m (expense_m_id, branch_id, expense_date)
values      (5, 7, '05-May-2020') ;

insert into expense_m (expense_m_id, branch_id, expense_date)
values      (6, 4, '06-Jun-2023') ;

insert into expense_m (expense_m_id, branch_id, expense_date)
values      (7, 8, '07-Jul-2022') ;

insert into expense_m (expense_m_id, branch_id, expense_date)
values      (8, 6, '08-Aug-2021') ;

insert into expense_m (expense_m_id, branch_id, expense_date)
values      (9, 10,'09-Sep-2020') ;

insert into expense_m (expense_m_id, branch_id, expense_date)
values      (10,3,'10-Oct-2023') ;

insert into expense_m (expense_m_id, branch_id, expense_date)
values      (11,1,'11-Nov-2022') ;

insert into expense_m (expense_m_id, branch_id, expense_date)
values      (12,4,'12-Dec-2021') ;

commit ;

--==================
--expense_d table
--==================

drop table expense_d cascade constraint ;

create table expense_d
(
expense_m_id           number,
expense_type_id        number        constraint expense_d_expense_type_id_nn not null ,
expense_amount         number        constraint expense_d_expense_amount_nn not null ,
payment_mode           varchar2(100) constraint expense_d_payment_made_nn not null ,
expense_by             number,
description            varchar2(250),
action_user            varchar2(100) default user,
action_date_time       date          default sysdate
) ;

alter table expense_d
add         constraint expense_d_expense_m_id_fk foreign key(expense_m_id)
references  expense_m(expense_m_id) ;

alter table expense_d
add         constraint expense_d_expense_type_id_fk foreign key(expense_type_id)
references  expense_type(expense_type_id) ;

INSERT INTO expense_d (expense_M_id, expense_type_id, expense_amount, payment_mode, expense_by, description)
VALUES (1, 1, 1000, 'Cash', 1, 'Operating expenses for the month of January');

INSERT INTO expense_d (expense_M_id, expense_type_id, expense_amount, payment_mode, expense_by, description)
VALUES (2, 2, 2000, 'Credit Card', 2, 'Cost of goods sold for the month of February');

INSERT INTO expense_d (expense_M_id, expense_type_id, expense_amount, payment_mode, expense_by, description)
VALUES (3, 3, 3000, 'Debit Card', 3, 'Marketing expenses for the month of March');

INSERT INTO expense_d (expense_M_id, expense_type_id, expense_amount, payment_mode, expense_by, description)
VALUES (4, 4, 4000, 'Cash', 4, 'Travel expenses for the month of April');

INSERT INTO expense_d (expense_M_id, expense_type_id, expense_amount, payment_mode, expense_by, description)
VALUES (5, 5, 5000, 'Credit Card', 5, 'Office supplies expenses for the month of May');

INSERT INTO expense_d (expense_M_id ,expense_type_id, expense_amount, payment_mode, expense_by, description)
VALUES (6, 6, 6000, 'Debit Card', 6, 'Rent expenses for the month of June');

INSERT INTO expense_d (expense_M_id, expense_type_id, expense_amount, payment_mode, expense_by, description)
VALUES (7, 7, 7000, 'Cash', 7, 'Utility expenses for the month of July');

INSERT INTO expense_d (expense_M_id ,expense_type_id ,expense_amount, payment_mode ,expense_by ,description)
VALUES (8, 8, 8000, 'Credit Card', 8, 'Insurance expenses for the month of August');

INSERT INTO expense_d (expense_M_id, expense_type_id, expense_amount, payment_mode, expense_by ,description)
VALUES (9 , 9, 9000, 'Debit Card', 9, 'Taxes expenses for the month of September');

INSERT INTO expense_d (expense_M_id, expense_type_id, expense_amount, payment_mode, expense_by ,description)
VALUES (10, 10, 10000, 'Cash', 10, 'Interest expenses for the month of October');

INSERT INTO expense_d (expense_M_id, expense_type_id, expense_amount, payment_mode, expense_by ,description)
VALUES (11, 11, 11000, 'Credit Card', 11, 'Depreciation expenses for the month of November');

INSERT INTO expense_d (expense_M_id, expense_type_id, expense_amount, payment_mode, expense_by, description)
VALUES (12, 12, 12000, 'Debit Card', 12, 'Amortization expenses for the month of December');

commit ;


--==============
--employee table
--==============

drop table employee cascade constraint ;

create table employee
(
employee_id          number,
department_id        number,
designation_id       number,      
branch_id            number,
first_name           varchar2(100)  constraint employee_first_name_nn not null,
last_name            varchar2(100)  constraint employee_last_name_nn not null,
father_name          varchar2(100),
mother_name          varchar2(100),
present_address      varchar2(350),
permanent_address    varchar2(350),
salary               number         constraint employee_salary_ck check(salary between 1000 and 50000),
join_date            date           default sysdate,
NID                  number         constraint employee_nid_uk unique,
email                varchar2(350)  constraint employee_email_uk unique,
cell_number          varchar2(100)  constraint employee_cell_number_uk unique,
date_of_birth        date,
gender               varchar2(100),
religion             varchar2(100),
nationality          varchar2(100),
blood_group          varchar2(100),
employee_image       blob,
employee_description varchar2(250),
action_user          varchar2(100) default user,
action_date_time     date          default sysdate
) ;

alter table employee
add         constraint employee_employee_id_pk primary key(employee_id) ;

alter table employee
add         constraint employee_designation_id_fk foreign key(designation_id)
references  designation(designation_id) ;

alter table employee
add         constraint employee_department_id_fk foreign key(department_id)
references  department(department_id) ;

alter table employee
add         constraint employee_branch_id_fk foreign key(branch_id)
references  branch(branch_id) ;

insert into employee (Employee_id, Department_id, Designation_id, Branch_id, First_name, Last_name, Father_name, Mother_name, Present_address, Permanent_address, Salary, Join_date, NID, Email, Cell_number, Date_of_birth, Gender, Religion, Nationality, Blood_group)
values                (1, 5, 7, 7, 'Sadia', 'Akter', 'Abdul' ,'Rahima', 'Mirpur Dhaka', 'Mirpur Dhaka', 50000, '20-jan-20', 1990123456789012, 'sadia.akter@gmail.com', '+8801712345678', '19-feb-01', 'Female', 'Islam', 'Bangladeshi', 'B+');

insert into employee (Employee_id, Department_id, Designation_id, Branch_id, First_name, Last_name, Father_name, Mother_name, Present_address, Permanent_address, Salary, Join_date, NID, Email, Cell_number, Date_of_birth, Gender, Religion, Nationality, Blood_group)
values                (2, 4, 6, 2, 'Tasnim', 'Akter', 'Jamil', 'Karima', 'Shyamoli Dhaka', 'Shyamoli Dhaka', 45000, '13-mar-21', 1991123456789012, 'tasnim.akter@gmail.com', '+8801812345678', '11-apr-90', 'Female', 'Islam', 'Bangladeshi', 'O+');

insert into employee (Employee_id, Department_id, Designation_id, Branch_id, First_name, Last_name, Father_name, Mother_name, Present_address, Permanent_address, Salary, Join_date, NID, Email, Cell_number, Date_of_birth, Gender, Religion, Nationality, Blood_group)
values                (3, 3, 5, 1, 'Nurul', 'Amin', 'Abdulla', 'Jaima', 'Jatrabari Dhaka', 'Jatrabari Dhaka', 40000, '23-feb-20', 1992123456789012, 'nurul.amin@gmail.com', '+8801912345678', '12-may-91', 'Male', 'Islam', 'Bangladeshi', 'AB+');

insert into employee (Employee_id, Department_id, Designation_id, Branch_id, First_name, Last_name, Father_name, Mother_name, Present_address, Permanent_address, Salary, Join_date, NID, Email, Cell_number, Date_of_birth, Gender, Religion, Nationality, Blood_group)
values                (4, 2, 4, 3, 'Taslima', 'Akter', 'Arman', 'Shammi', 'Uttara Dhaka', 'Uttara Dhaka', 35000, '20-sep-23', 1993123456789013, 'taslima.akter@gmail.com', '+8801612345678', '19-jun-95', 'Female', 'Islam', 'Bangladeshi', 'A+');

insert into employee (Employee_id, Department_id, Designation_id, Branch_id, First_name, Last_name, Father_name, Mother_name, Present_address, Permanent_address, Salary, Join_date, NID, Email, Cell_number, Date_of_birth, Gender, Religion, Nationality, Blood_group)
values                (5, 11, 12, 1, 'Sakib', 'Hossain', 'Amir', 'Ramisa', 'Mohammadpur Dhaka', 'Mohammadpur Dhaka', 30000, '15-aug-20', 1994123456789012, 'sakib.hossain@gmail.com', '+8801312345678', '01-jan-94', 'Male', 'Islam', 'Bangladeshi', 'B-');

insert into employee (Employee_id, Department_id, Designation_id, Branch_id, First_name, Last_name, Father_name, Mother_name, Present_address, Permanent_address, Salary, Join_date, NID, Email, Cell_number, Date_of_birth, Gender, Religion, Nationality, Blood_group)
values                (6, 9, 11, 4, 'Sadiaa', 'Akter', 'Hamza', 'Kohinur', 'Badda Dhaka', 'Badda Dhaka', 25000, '10-jul-23', 199513456789012, 'sadiaa.akter@gmail.com', '+8801412345678', '28-dec-02', 'Female', 'Islam', 'Bangladeshi', 'O-');

insert into employee (Employee_id, Department_id, Designation_id, Branch_id, First_name, Last_name, Father_name, Mother_name, Present_address, Permanent_address, Salary, Join_date, NID, Email, Cell_number, Date_of_birth, Gender, Religion, Nationality, Blood_group)
values                (7, 8, 10, 3, 'Taasnim', 'Akter', 'Sulaiman', 'Fahmida', 'Khilkhet Dhaka', 'Khilkhet Dhaka', 20000, '12-dec-22', 199613456789012, 'taasnim.akter@gmail.com', '+8801512345678', '30-nov-99', 'Female', 'Islam', 'Bangladeshi', 'AB-');

insert into employee (Employee_id, Department_id, Designation_id, Branch_id, First_name, Last_name, Father_name, Mother_name, Present_address, Permanent_address, Salary, Join_date, NID, Email, Cell_number, Date_of_birth, Gender, Religion, Nationality, Blood_group)
values                (8, 6, 8, 2, 'Taaslima', 'Akter', 'Jakariya', 'Afreen', 'Khilgaon Dhaka', 'Khilgaon Dhaka', 45000, '04-may-20', 200112356789012, 'taaslima.akter@gmail.com', '+880191234578', '05-oct-99', 'Female', 'Islam', 'Bangladeshi', 'A-');

insert into employee (Employee_id, Department_id, Designation_id, Branch_id, First_name, Last_name, Father_name, Mother_name, Present_address, Permanent_address, Salary, Join_date, NID, Email, Cell_number, Date_of_birth, Gender, Religion, Nationality, Blood_group)
values                (9, 2, 3, 4, 'Rakib', 'Hossain', 'Zahid', 'Nurunnahar', 'Shahbagh Dhaka', 'Shahbagh Dhaka', 20000, '07-mar-20', 1997123456789012, 'rakib.hossain@gmail.com', '+8801212345678', '03-sep-91', 'Male', 'Islam', 'Bangladeshi', 'A+');

insert into employee (Employee_id, Department_id, Designation_id, Branch_id, First_name, Last_name, Father_name, Mother_name, Present_address, Permanent_address, Salary, Join_date, NID, Email, Cell_number, Date_of_birth, Gender, Religion, Nationality, Blood_group)
values                (10, 1, 2, 3, 'Saaima', 'Akter', 'Faruk', 'Tahmina', 'Malibagh Dhaka', 'Malibagh Dhaka', 15000, '15-nov-22', 19981456789012, 'saimaa.akter@gmail.com', '+880131245678', '12-aug-96', 'Female', 'Islam', 'Bangladeshi', 'B-');

insert into employee (Employee_id, Department_id, Designation_id, Branch_id, First_name, Last_name, Father_name, Mother_name, Present_address, Permanent_address, Salary, Join_date, NID, Email, Cell_number, Date_of_birth, Gender, Religion, Nationality, Blood_group)
values                (11, 12, 1, 4, 'Nabila', 'Islam', 'Zahir', 'Afroza', 'Dhanmondi Dhaka', 'Dhanmondi Dhaka', 50000, '13-jan-21', 1999123456789012, 'nabila.islam@gmail.com', '+880141234678', '26-feb-98', 'Female', 'Islam', 'Bangladeshi', 'AB+');

insert into employee (Employee_id, Department_id, Designation_id, Branch_id, First_name, Last_name, Father_name, Mother_name, Present_address, Permanent_address, Salary, Join_date, NID, Email, Cell_number, Date_of_birth, Gender, Religion, Nationality, Blood_group)
values                (12, 11, 2, 1, 'Fahim', 'Molla', 'Eyakub', 'Sefali', 'Gulshan Dhaka', 'Gulshan Dhaka', 5000, '23-mar-23', 2000123456789012, 'fahim.mollaa@gmail.com', '+880151234578', '11-nov-92', 'Male', 'Islam', 'Bangladeshi', 'O-');

commit ;

--===============
--user_info table
--===============

drop table user_info cascade constraint ;

create table user_info
(
user_info_id             number,
user_type_id             number,
user_status_id           number,
employee_id              number,
branch_id                number,
username                 varchar2(100) constraint user_info_username_nn not null
                                       constraint user_info_username_uk unique  ,
password                 varchar2(100) constraint user_info_password_nn not null,
user_image               blob,
user_info_description    varchar2(250),
action_user              varchar2(100) default user,
action_date_time         date          default sysdate
) ;

alter table user_info
add         constraint user_info_user_info_id_pk primary key(user_info_id) ;

alter table user_info
add         constraint user_info_user_type_id_fk foreign key(user_type_id)
references  user_type(user_type_id) ;

alter table user_info
add         constraint user_info_user_status_id_fk foreign key(user_status_id)
references  user_status(user_status_id) ;

alter table user_info
add         constraint user_info_employee_id_fk foreign key(employee_id)
references  employee(employee_id) ;

alter table user_info
add         constraint user_info_branch_id_fk foreign key(branch_id)
references  branch(branch_id) ;

insert into user_info (user_info_id, user_type_id, user_status_id, employee_id, branch_id, username, password)
values (1, 1, 1, 3, 4, 'admin', 'admin') ;

insert into user_info (user_info_id, user_type_id, user_status_id, employee_id, branch_id, username, password)
values (2, 2, 1, 4, 1, 'mod', 'mod') ;

insert into user_info (user_info_id, user_type_id, user_status_id, employee_id, branch_id, username, password)
values (3, 3, 4, 2, 5, 'stu', 'stu') ;

insert into user_info (user_info_id, user_type_id, user_status_id, employee_id, branch_id, username, password)
values (4, 4, 3, 1, 4, 'writ', 'writ') ;

insert into user_info (user_info_id, user_type_id, user_status_id, employee_id, branch_id, username, password)
values (5, 5, 8, 4, 5, 'rdr', 'rdr') ;

insert into user_info (user_info_id, user_type_id, user_status_id, employee_id, branch_id, username, password)
values (6, 6, 2, 5, 8, 'sub', 'sub') ;

insert into user_info (user_info_id, user_type_id, user_status_id, employee_id, branch_id, username, password)
values (7, 7, 9, 1, 5, 'gst', 'gst') ;

insert into user_info (user_info_id, user_type_id, user_status_id, employee_id, branch_id, username, password)
values (8, 8, 5, 1, 2, 'rviwr', 'rviwr') ;

insert into user_info (user_info_id, user_type_id, user_status_id, employee_id, branch_id, username, password)
values (9, 9, 6, 5, 3, 'cntrbtr', 'cntrbtr') ;

insert into user_info (user_info_id, user_type_id, user_status_id, employee_id, branch_id, username, password)
values (10, 10, 11, 12, 4, 'crtr', 'crtr') ;

insert into user_info (user_info_id, user_type_id, user_status_id, employee_id, branch_id, username, password)
values (11, 11, 2, 4, 5, 'mntr', 'mntr') ;

insert into user_info (user_info_id, user_type_id, user_status_id, employee_id, branch_id, username, password)
values (12, 12, 7, 9, 2, 'lrnr', 'lrnr') ;

commit ;


--- FORM_INFORMATION ---

drop table FORM_INFORMATION cascade constraints ;

CREATE TABLE FORM_INFORMATION
(
FORM_INFORMATION_ID NUMBER NOT NULL ENABLE,
FORM_NAME VARCHAR2(100 BYTE),
MENU_NAME VARCHAR2(100 BYTE)
) ;

ALTER TABLE FORM_INFORMATION
ADD CONSTRAINT FORM_INFORMATION_ID_PK PRIMARY KEY ( FORM_INFORMATION_ID ) ;


--- USER_FORM_M ---

drop table USER_FORM_M cascade constraints ;

CREATE TABLE USER_FORM_M
(
USER_FORM_M_ID NUMBER NOT NULL ENABLE,
USER_ID VARCHAR2(100 BYTE),
USER_NAME VARCHAR2(100 BYTE)
) ;

ALTER TABLE USER_FORM_M
ADD CONSTRAINT USER_FORM_M_ID_PK PRIMARY KEY ( USER_FORM_M_ID ) ;

--- USER_FORM_D ---

drop table USER_FORM_D cascade constraints ;

CREATE TABLE USER_FORM_D
(
USER_FORM_D_ID NUMBER NOT NULL ENABLE,
USER_FORM_M_ID NUMBER,
FORM_INFORMATION_ID NUMBER,
FORM_NAME VARCHAR2(100 BYTE),
STATUS VARCHAR2(100 BYTE),
INSERT_USER VARCHAR2(100 BYTE),
CONSTRAINT USER_FORM_M_ID_FK FOREIGN KEY ( USER_FORM_M_ID )
REFERENCES USER_FORM_M ( USER_FORM_M_ID ) ENABLE
) ;

ALTER TABLE USER_FORM_D
ADD CONSTRAINT USER_FORM_D_ID_PK PRIMARY KEY ( USER_FORM_D_ID ) ;



