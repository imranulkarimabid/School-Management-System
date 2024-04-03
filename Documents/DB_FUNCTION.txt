--1

create or replace function f_section_name
(
 P_section_id in section.section_id%type
)
return section.section_name%type
is
 v_section_name section.section_name%type ;
 begin
SELECT section_name
into   v_section_name
from   section
where  section_id = P_section_id ;
return v_section_name ;
end  f_section_name ;
/


select f_shift_name(CURRENT_shift_ID) current_shift_name, f_shift_name(new_shift_id) new_shift_name,
       f_class_name(current_class_id) current_class_name, f_shift_name(new_class_id) new_class_name,
      f_section_name(CURRENT_SECTION_ID) current_section_name, f_section_name(NEW_SECTION_ID) new_section_name
from   re_admission ;



--2

create or replace function f_shift_name
(
 P_shift_id in shift.shift_id%type
)
return shift.shift_name%type
is
 v_shift_name shift.shift_name%type ;
 begin
SELECT shift_name
into   v_shift_name
from   shift
where  shift_id = P_shift_id ;
return v_shift_name ;
end  f_shift_name ;
/


select f_shift_name(CURRENT_shift_ID) current_shift_name, f_shift_name(NEW_shift_ID) new_shift_name
from   re_admission ;


--3

create or replace function f_class_name
(
 P_class_id in class.class_id%type
)
return class.class_name%type
is
 v_class_name class.class_name%type ;
 begin
SELECT class_name
into   v_class_name
from   class
where  class_id = P_class_id ;
return v_class_name ;
end  f_class_name ;
/


select f_class_name(CURRENT_class_ID) current_class_name, f_class_name(NEW_class_ID) new_class_name
from   re_admission ;


select f_shift_name(CURRENT_shift_ID) current_shift_name, f_shift_name(new_shift_id) new_shift_name,
       f_class_name(current_class_id) current_class_name, f_shift_name(new_class_id) new_class_name,
      f_section_name(CURRENT_SECTION_ID) current_section_name, f_section_name(NEW_SECTION_ID) new_section_name
from   re_admission ;


--4

--to show name from student table

create or replace function f_st_std_name
 (p_student_id   student.student_id%type)
return varchar2
is
 v_student_name   varchar2(200) ;
begin
 select first_name||' '||last_name student_name
 into   v_student_name
 from   student 
 where  student_id = p_student_id ;
return v_student_name ;
end  f_st_std_name ;
/


--5

--to show name from admission table

create or replace function f_ad_std_name
 (p_admission_id   admission.admission_id%type)
return varchar2
is
 v_student_name   varchar2(200) ;
begin
 select first_name||' '||last_name student_name
 into   v_student_name 
 from   admission
 where  admission_id = p_admission_id ;
return v_student_name  ;
end  f_ad_std_name ;
/


--6

create or replace function f_letter_grade
 (p_obtained_marks result_d.obtained_marks%type)
return varchar2
is
 v_letter_grade varchar2(100) ;
begin
 if p_obtained_marks between 80 and 100 then 
  v_letter_grade := 'A+' ;
 elsif p_obtained_marks between 70 and 79 then 
  v_letter_grade := 'A' ;
 elsif p_obtained_marks between 60 and 69 then 
  v_letter_grade := 'A-' ;
 elsif p_obtained_marks between 50 and 59 then 
  v_letter_grade := 'B-' ;
 elsif p_obtained_marks between 40 and 49 then 
  v_letter_grade := 'C' ;
 elsif p_obtained_marks between 33 and 39 then 
  v_letter_grade := 'D' ;
 elsif p_obtained_marks between 0 and 32 then 
  v_letter_grade := 'F' ;
  else  v_letter_grade := 'F' ;
 end if ;
return v_letter_grade ;
end f_letter_grade ;
/

--7

create or replace function f_grade_point
 (p_obtained_marks result_d.obtained_marks%type)
return number
is
 v_grade_point number ;
begin
 if p_obtained_marks between 80 and 100 then 
  v_grade_point := 5.00 ;
 elsif p_obtained_marks between 70 and 79 then 
  v_grade_point := 4.00 ;
 elsif p_obtained_marks between 60 and 69 then 
  v_grade_point := 3.50 ;
 elsif p_obtained_marks between 50 and 59 then 
  v_grade_point := 3.00 ;
 elsif p_obtained_marks between 40 and 49 then 
  v_grade_point := 2.00 ;
 elsif p_obtained_marks between 33 and 39 then 
  v_grade_point := 1.00 ;
 elsif p_obtained_marks between 0 and 32 then 
  v_grade_point := 0.00 ;
 else  v_grade_point := 0.00 ;
 end if ;
return V_grade_point;
end f_grade_point;
/






















