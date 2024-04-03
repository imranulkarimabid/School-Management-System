-- exam_Category table

drop table exam_Category cascade constraints ;

create table exam_Category
(
 exam_Category_ID             number,
 exam_Category_name           varchar2(100)  constraint exam_Category_exam_Category_name_uk unique
                                             constraint exam_Category_exam_Category_name_nn not null,
 exam_category_description    varchar2(250),
 action_user                  varchar2(100)    default user,
 action_date_time             date            default sysdate
) ;
alter table exam_Category
add   constraint exam_Category_exam_Category_id_pk primary key (exam_Category_id) ;

-- exam_type table

drop table exam_type cascade constraints ;

create table Exam_Type
(
 Exam_Type_ID          number,
 Exam_Type_name        varchar2(100) constraint exam_type_exam_type_name_uk unique
                                     constraint exam_type_exam_type_name_nn not null,
 exam_type_description varchar2(250),
 action_user           varchar2(100)    default user,
 action_date_time      date            default sysdate  
) ;

alter table Exam_Type
add   constraint Exam_Type_Exam_Type_id_pk primary key (Exam_Type_id) ;

--Shift_Table

drop table shift cascade constraints ;

create table shift
(
shift_id            number,
shift_name          varchar2(100)  constraint  shift_shift_name_uk unique,
start_time          varchar2(100),
end_time            varchar2(100),
action_user         varchar2(100) default user,
action_date_time    date          default sysdate
) ;


alter table shift
add   constraint shift_shift_id_pk primary key(shift_id) ; 


--result_category Table

drop table result_category cascade constraints ;

create table Result_Category
(
 Result_Category_ID          number,
 Result_Category_name        varchar2(100)  constraint Result_Category_Result_Category_name_uk unique,
 result_category_description varchar2(250),
 action_user                 varchar2(100)    default user,
 action_date_time            date            default sysdate
) ;

alter table Result_Category
add   constraint Result_Category_Result_Category_id_pk primary key (Result_Category_id) ;

--result_type table

drop table result_type cascade constraints ;

create table Result_Type
(
 Result_Type_ID          number,
 Result_Category_ID      number,
 Result_Type_name        varchar2(100),
 result_type_description varchar2(250),
 action_user             varchar2(100)    default user,
 action_date_time        date            default sysdate  
) ;

alter table Result_Type
add   constraint Result_Type_Result_Type_id_pk primary key (Result_Type_id) ;

alter      table Result_Type
add        constraint Result_Type_Result_category_id_fk foreign key (Result_category_id) 
references result_category (result_category_id) ;

--class table

drop table class cascade constraints ;

create table class
(
 Class_ID          number,
 Class_Name        varchar2(100) constraint class_class_name_nn not null
                                 constraint class_class_name_uk unique,
 class_description varchar2(250),
 action_user       varchar2(100)    default user,
 action_date_time date            default sysdate
) ;

alter table class
add   constraint class_class_id_pk primary key(class_id) ;

--class_info table

drop table class_info cascade constraint ;

create table class_info
(
class_info_id      number,
class_id           number,
subject_id           number,
action_user          varchar2(100) default user,
action_date_time     date default sysdate
) ;
    
alter table class_info
add constraints  class_info_class_info_id_pk primary key(class_info_id) ;

alter table class_info
add constraints  class_info_class_id_fk foreign key(class_id)
references class(class_id) ;

alter table class_info
add constraints  class_info_subject_id_fk foreign key(subject_id)
references subject(subject_id) ;


--fee_type table

drop table fee_type cascade constraints ;

create table Fee_Type
(
 Fee_Type_ID          number,
 Fee_type_name        varchar2(100)   constraint fee_type_fee_type_name_nn not null,
 fee_type_description varchar2(250),
 action_user          varchar2(100)    default user,
 action_date_time     date            default sysdate
) ;

alter table fee_type
add   constraint fee_type_fee_type_id_pk primary key(fee_type_id) ;

insert into fee_type(fee_type_id, fee_type_name)
values(1, 'Weekly') ;

insert into fee_type(fee_type_id, fee_type_name)
values(2, 'Monthly') ;

insert into fee_type(fee_type_id, fee_type_name)
values(3, 'Annual') ;

insert into fee_type(fee_type_id, fee_type_name)
values(4, 'One Time') ;

commit ;

drop table subject cascade constraints ;

create table subject
(
 subject_ID          number,
 subject_Name        varchar2(100)   constraint subject_subject_name_nn not null,
 subject_description varchar2(250),
 action_user         varchar2(100)    default user,
 action_date_time    date            default sysdate
);


alter table subject
add   constraint subject_subject_id_pk primary key(subject_id) ;

drop table section cascade constraints ;

create table section
(
 section_ID          number,
 section_Name        varchar2(100)   constraint section_section_name_nn not null,
 section_description varchar2(250),
 action_user         varchar2(100)    default user,
 action_date_time    date            default sysdate
);


alter table section
add   constraint section_section_id_pk primary key(section_id) ;

--fee_amount Table

drop table fee_amount cascade constraint ;

create table fee_amount 
(
 Fee_Amount_Id    Number,
 Fee_Type_ID      Number,
 Class_ID         Number,
 fee_name         varchar2(100),
 Fee_Amount       Number,
 Action_User      Varchar2(100) Default User,
 Action_Date_Time Date          Default Sysdate
) ;

alter table fee_amount
add   constraint fee_amount_fee_amount_id_pk primary key(fee_amount_id) ;

alter table fee_amount
add   constraint fee_amount_fee_type_id_fk foreign key (fee_type_id)
references fee_type(fee_type_id) ;

alter table fee_amount
add   constraint fee_amount_class_id_fk foreign key (class_id)
references class(class_id) ;



drop table subject_d cascade constraints ;

create table Subject_d
(
 Subject_d_ID          number,
 Subject_m_ID          number,
 class_id              number,
 subject_d_description varchar2(250),
 action_user           varchar2(100)    default user,
 action_date_time      date            default sysdate
);


alter table subject_d
add   constraint subject_d_subject_d_id_pk primary key(subject_d_id) ;

alter      table subject_d
add        constraint subject_d_subject_m_id_fk foreign key (subject_m_id) 
references subject_m (subject_m_id) ;


alter      table subject_d
add        constraint subject_d_class_id_fk foreign key (class_id) 
references class (class_id) ;


--Student Table

drop table student cascade constraint ;

create table student
(
student_id             number,
first_name             varchar2(100)  constraint student_first_name_nn not null,
last_name              varchar2(100),
date_of_birth          date,
gender                 varchar2(100),
religion               varchar2(100),
blood_group            varchar2(5),
Birth_reg_number       number         constraint student_Birth_reg_number_uk unique,
fathers_name           varchar2(100),
Fathers_Signature      blob,
Fathers_Cell_Number    varchar2(100),
mothers_name           varchar2(100),
mothers_Signature      blob,
mothers_Cell_Number    varchar2(100),
Guardians_Name         Varchar2(100),
Guardians_Signature    BLOB,
Guardians_Cell_Number  varchar2(100),
Relation_with_Guardian Varchar2(100),
shift_id                number,
class_id                number,
section_id              number,
roll_number             number,
previous_class          number,
previous_school         varchar2(250),
present_address         varchar2(350),
permanent_address       varchar2(350),
student_image           blob,
admission_date          date default sysdate,
action_user          varchar2(100) default user,
action_date_time     date          default sysdate
) ;


alter table student
add constraint student_student_id_pk primary key(student_id) ;

alter table student 
add  constraint student_class_id_fk foreign key(class_id)
references  class(class_id) ; 

alter table student 
add  constraint student_section_id_fk foreign key(section_id)
references  section(section_id) ; 

alter table student 
add  constraint student_shift_id_fk foreign key(shift_id)
references  shift(shift_id) ; 

--Admission Table

drop table Admission cascade constraint ;

create table Admission
(
Admission_id             number,
first_name             varchar2(100)  constraint Admission_first_name_nn not null,
last_name              varchar2(100),
date_of_birth          date,
gender                 varchar2(100),
religion               varchar2(100),
blood_group            varchar2(5),
Birth_reg_number       number         constraint Admission_Birth_reg_number_uk unique,
fathers_name           varchar2(100),
Fathers_Signature      blob,
Fathers_Cell_Number    varchar2(100),
mothers_name           varchar2(100),
mothers_Signature      blob,
mothers_Cell_Number    varchar2(100),
Guardians_Name         Varchar2(100),
Guardians_Signature    BLOB,
Guardians_Cell_Number  varchar2(100),
Relation_with_Guardian Varchar2(100),
class_id                number,
previous_class          number,
previous_school         varchar2(250),
present_address         varchar2(350),
permanent_address       varchar2(350),
student_image           blob,
admission_date          date default sysdate,
action_user          varchar2(100) default user,
action_date_time     date          default sysdate
) ;


alter table Admission
add constraint Admission_Admission_id_pk primary key(Admission_id) ;

alter table Admission
add  constraint Admission_class_id_fk foreign key(class_id)
references  class(class_id) ; 


--re_Admission Table

drop table Re_Admission cascade constraint ;

create table Re_Admission 
(
 Re_Admission_id     number, 
 student_id          number, 
 Re_Admission_date   date,
 current_shift_id    number,
 current_class_id    number, 
 current_section_id  number,
 current_roll_number number,
 new_shift_id        number,
 new_class_id        number, 
 new_section_id      number,
 new_roll_number     number,
 action_user         varchar2(100) default user,
 action_date_time    date default sysdate
) ;


alter table Re_Admission 
add constraint Re_Admission_Re_Admission_id_pk primary key(Re_Admission_id) ;

alter table Re_Admission
add  constraint Re_Admission_student_id_fk foreign key(student_id)
references  student(student_id) ; 

alter table Re_Admission
add  constraint Re_Admission_new_class_id_fk foreign key(new_class_id)
references  class(class_id) ; 

alter table Re_Admission
add  constraint Re_Admission_new_section_id_fk foreign key(new_section_id)
references  section(section_id) ; 

alter table Re_Admission
add  constraint Re_Admission_new_shift_id_fk foreign key(new_shift_id)
references  shift(shift_id) ; 



--class_d_Table

drop table class_D cascade constraints ;

create table Class_D
(
 Class_d_ID          Number,
 Detailed_Class_Name varchar2(100) constraint class_d_Detailed_Class_Name_uk unique,
 shift_id            number,
 Class_ID            Number,
 Section_id          Number,
 Subject_id          Number,
 Action_User         Varchar2(100) Default User,
 Action_Date_Time    Date Default Sysdate
) ;

alter table class_d
add constraint class_d_class_d_id_pk primary key(class_d_id) ;

alter table class_d
add  constraint class_d_shift_id_fk foreign key(shift_id)
references  shift(shift_id) ; 

alter table class_d
add  constraint class_d_class_id_fk foreign key(class_id)
references  class(class_id) ; 

alter table class_d
add  constraint class_d_section_id_fk foreign key(section_id)
references  section(section_id) ; 

alter table class_d
add  constraint class_d_subject_id_fk foreign key(subject_id)
references  subject(subject_id) ; 


--exam table

drop table exam cascade constraints ;

create table Exam
(
 Exam_ID          Number,
 Exam_Category_ID Number,
 Exam_Type_ID     Number,
 Student_ID       Number,
 class_d_ID       Number,
 exam_date        date,
 Action_User      Varchar2(100) Default User,
 Action_Date_Time Date Default Sysdate
) ;

alter table Exam
add   constraint Exam_Exam_id_pk primary key (Exam_id) ;

alter      table Exam
add        constraint Exam_Exam_category_id_fk foreign key (Exam_category_id) 
references Exam_category (Exam_category_id) ;

alter      table Exam
add        constraint Exam_Exam_type_id_fk foreign key (Exam_type_id) 
references Exam_type (Exam_type_id) ;

alter      table Exam
add        constraint Exam_student_id_fk foreign key (student_id) 
references student (student_id) ;

alter      table Exam
add        constraint Exam_class_d_id_fk foreign key (class_d_id) 
references class_d (class_d_id) ;

--attendance_e
 
drop table Attendance_E  cascade constraint ;

create table Attendance_e
(
Attendance_E_ID        Number,
Attendance_date        date default sysdate,
employee_id            number,
login	               Date,
logoff	               Date,
status                 varchar2(100),
Action_User	       Varchar2(100) default user,
Action_Date_Time       Date default sysdate
) ;

alter table Attendance_e
add constraint Attendance_E_Attendance_E_id_pk primary key(Attendance_E_id) ;

alter table Attendance_E
add   constraint Attendance_e_employee_id_fk foreign key(employee_id)
references employee(employee_id) ;


--Routine_M_Table


drop table routine_M cascade constraint ;

create table routine_M
(
routine_m_id          number,
employee_id           number,
day_of_week           varchar2(100),
action_user           varchar2(100) default user,
action_date_time      date          default sysdate
) ;

alter table routine_m
add constraint routine_M_routine_M_id_pk primary key(routine_M_id) ;

alter table routine_M
add constraint routine_M_employee_id_fk foreign key(employee_id) 
references employee (employee_id) ;

--Routine_d_Table


drop table routine_d cascade constraint ;

create table routine_d
(
routine_d_id          number,
routine_m_id          number,
class_d_id            number,
start_time            varchar2(100),
end_time              varchar2(100),
action_user           varchar2(100) default user,
action_date_time      date          default sysdate
) ;


alter table routine_d
add constraint routine_d_routine_d_id_pk primary key(routine_d_id) ;

alter table routine_d
add constraint routine_D_routine_m_id_fk foreign key(routine_m_id) 
references routine_m(routine_m_id) ;

alter table routine_d
add constraint routine_D_class_d_id_fk foreign key(class_d_id) 
references class_d(class_d_id) ;


--attendance_m
 
drop table Attendance_m cascade constraint ;

create table Attendance_m
(
Attendance_m_ID        Number,
Attendance_date        date default sysdate,
shift_id               Number,
class_id               number,
section_id	       Number,
Action_User	       Varchar2(100) default user,
Action_Date_Time       Date default sysdate
) ;

alter table Attendance_M
add constraint Attendance_m_Attendance_m_id_pk primary key(Attendance_m_id) ;

alter table Attendance_M
add   constraint Attendance_m_shift_id_fk foreign key(shift_id)
references shift(shift_id) ;

alter table Attendance_M
add   constraint Attendance_m_class_id_fk foreign key(class_id)
references class(class_id) ;

alter table Attendance_M
add   constraint Attendance_m_section_id_fk foreign key(section_id)
references section(section_id) ;

--table attendance_d

drop table Attendance_d cascade constraints ;

create table Attendance_d
(
Attendance_d_ID        Number,
Attendance_m_ID        Number,
student_id             number,
status                 varchar2(100),
Action_User	       Varchar2(100) default user,
Action_Date_Time       Date default sysdate
);

alter table Attendance_d
add constraint Attendance_d_Attendance_d_id_pk primary key(Attendance_d_id) ;

alter table Attendance_D
add   constraint Attendance_d_Attendance_m_fk foreign key(Attendance_m_id)
references Attendance_m(Attendance_m_id) ;

alter table Attendance_D
add   constraint Attendance_d_student_id_fk foreign key(student_id)
references student(student_id) ;



--exam_m table

drop table exam_m cascade constraint ;

create table exam_m
(
exam_m_id         number,
exam_category_id  number,
exam_type_id      number,
shift_id            number,
Class_ID            Number,
Section_id          Number,
action_user       varchar2(100) default user,
action_date_time  date  default sysdate
) ;

alter table exam_m
add constraint exam_m_exam_m_id_pk primary key(exam_m_id) ;

alter table exam_m
add constraint exam_m_exam_category_id_fk foreign key(exam_category_id) 
references exam_category(exam_category_id) ;

alter table exam_m
add constraint exam_m_exam_type_id_fk foreign key(exam_type_id) 
references exam_type(exam_type_id) ;

alter table exam_m
add constraint exam_m_class_id_fk foreign key(class_id) 
references class(class_id) ;

alter table exam_m
add constraint exam_m_shift_id_fk foreign key(shift_id) 
references shift(shift_id) ;

alter table exam_m
add constraint exam_m_section_id_fk foreign key(section_id) 
references section(section_id) ;



--exam_d table

drop table exam_d cascade constraint ;

create table exam_d
(
exam_d_id         number,
exam_m_id         number,
subject_id        number,
exam_date         date,
exam_time         varchar2(100),
Total_marks       number,
action_user       varchar2(100) default user,
action_date_time  date  default sysdate
) ;

alter table exam_d
add constraint exam_d_exam_d_id_pk primary key(exam_d_id) ;

alter table exam_d
add constraint exam_d_exam_m_id_fk foreign key(exam_m_id) 
references exam_m(exam_m_id) ;

alter table exam_d
add constraint exam_d_subject_id_fk foreign key(subject_id) 
references subject(subject_id) ;



--result_m

drop table result_m cascade constraint ;

create table result_m
(
result_m_id        number,
exam_m_id          number,
subject_id        number,
action_user       varchar2(100) default user,
action_date_time  date default sysdate
) ;

alter table result_m
add constraint result_m_result_m_id_pk primary key(result_m_id) ;

alter table result_m
add constraint result_m_exam_m_id_fk foreign key(exam_m_id)
references  exam_m (exam_m_id) ;

alter table result_m
add constraint result_m_subject_id_fk foreign key(subject_id)
references  subject (subject_id) ;


--result_d table

drop table result_d cascade constraint ;

create table result_d
(
result_d_id      number,
result_m_id      number,
student_id       number,
obtained_marks   number,
Absent           varchar2(100),
action_user      varchar2(100) default user,
action_date_time  date default sysdate
) ;

alter table result_d
add constraint result_d_result_d_id_pk primary key(result_d_id) ;

alter table result_d
add constraint result_d_result_m_id_fk foreign key(result_m_id)
references  result_m (result_m_id) ;

alter table result_d
add constraint result_d_student_id_fk foreign key(student_id)
references  student (student_id) ;


--fee_m table

drop table fee_m cascade constraints ;

create table fee_m
(
fee_m_id       number,
student_id       number,
admission_id    number,
class_id          number,
collection_date     date default sysdate,
paid_amount         number,
due_amount         number,
sessions           number,
action_user         varchar2(100) default user,
action_date_time    date  default sysdate
) ;

alter table fee_m
add   constraint fee_m_fee_m_id_pk primary key(fee_m_id) ;

alter table fee_m
add   constraint fee_m_student_id_fk foreign key (student_id)
references student(student_id) ;

alter table fee_m
add   constraint fee_m_admission_id_fk foreign key (admission_id)
references admission(admission_id) ;

alter table fee_m
add   constraint fee_m_class_id_fk foreign key (class_id)
references class(class_id) ;


--table fee_d 

drop table fee_d cascade constraints ;

create table fee_d
(
fee_d_id       number,
fee_m_id       number,
fee_amount_id       number,
fee_amount          number,
quantity            number,
action_user         varchar2(100) default user,
action_date_time    date  default sysdate
) ;

alter table fee_d
add   constraint fee_d_fee_d_id_pk primary key(fee_d_id) ;

alter table fee_d
add   constraint fee_d_fee_m_id_fk foreign key (fee_m_id)
references fee_m(fee_m_id) ;

alter table fee_d
add   constraint fee_m_fee_amount_id_fk foreign key (fee_amount_id)
references fee_amount(fee_amount_id) ;

