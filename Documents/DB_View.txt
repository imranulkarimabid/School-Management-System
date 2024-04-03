--1

create or replace view emp_dept_report_lov_view
as
select e.department_id, department_name||'('||count(employee_id)||')' department_name
from   employee e, department d
where  e.department_id = d.department_id 
group  by e.department_id, department_name
order  by department_name ;

select department_id, department_name 
from   emp_dept_report_lov_view ;


--2

create or replace view admission_view
as
select admission_id, admission_date, first_name||' '||last_name Student_Name, 
       class_name, BIRTH_REG_NUMBER, STUDENT_IMAGE, PRESENT_ADDRESS, 
       FATHERS_CELL_NUMBER, gender, date_of_birth, FATHERS_NAME,MOTHERS_NAME, 
       GUARDIANS_NAME,RELATION_WITH_GUARDIAN, a.class_id
from   admission a, class c
where  a.class_id = c.class_id
order  by admission_id ;

select admission_id, Student_Name, class_name, admission_date
from   admission_view ;


--3

create or replace view user_view
as
select username, user_type_name, ui.action_user created_by, ui.action_date_time creation_date
from   user_info ui, user_type ut
where  ui.user_type_id = ut.user_type_id 
order  by username ;


select username, user_type_name, created_by, creation_date
from   user_view ;


--4

create or replace view employee_view 
as 
select         DEPARTMENT_NAME, DESIGNATION_NAME, EMPLOYEE_ID , e.DEPARTMENT_ID, e.DESIGNATION_ID , 
               FIRST_NAME, LAST_NAME, FATHER_NAME, MOTHER_NAME ,PRESENT_ADDRESS,PERMANENT_ADDRESS, 
               SALARY, JOIN_DATE, NID, EMAIL, CELL_NUMBER, DATE_OF_BIRTH, GENDER, RELIGION, NATIONALITY, 
               BLOOD_GROUP, EMPLOYEE_IMAGE, e.ACTION_USER, e.ACTION_DATE_TIME
from           DEPARTMENT d, DESIGNATION de, EMPLOYEE e
where          d.department_id = e.department_id 
and            de.designation_id = e.designation_id  ; 

select      DEPARTMENT_NAME, DESIGNATION_NAME, EMPLOYEE_ID, DATE_OF_BIRTH, DEPARTMENT_ID
from        employee_view ;


--5

create or replace view class_view
as
select ci.class_id, class_name, ci.subject_id, subject_name
from   class_info ci, class c, subject s
where  ci.class_id = c.class_id
and    ci.subject_id = s.subject_id 
order  by class_name ;

select  class_name, subject_name
from    class_view ;


--6

create or replace view attendance_view
as
select ATTENDANCE_DATE, am.SHIFT_ID, shift_name, am.CLASS_ID, am.SECTION_ID, 
       class_name, section_name, ad.student_id, first_name||' '||last_name student_name, status
from   attendance_d ad, attendance_m am, shift sh, class c, section se, student st
where  ad.attendance_m_id = am.attendance_m_id
and    ad.student_id = st.student_id
and    am.class_id = c.class_id
and    am.shift_id = sh.shift_id
and    am.section_id = se.section_id
order  by class_name ;

select ATTENDANCE_DATE, shift_name, SHIFT_ID, CLASS_ID,SECTION_ID, 
       class_name, section_name, student_id, student_name, status
from   attendance_view ;


--7

create or replace view result_view
as
select to_char(ed.exam_date,'RRRR') year, rd.student_id, st.section_id, F_SECTION_NAME(st.section_id) section, 
       F_SHIFT_NAME(st.shift_id) shift, st.shift_id, st.class_id, F_CLASS_NAME(st.class_id) class, 
       st.first_name||' '||st.last_name st_name, st.roll_number, 
       em.exam_category_id, exam_category_name, 
       em.exam_type_id, exam_type_name,
       rm.subject_id, subject_name, 
       (CASE WHEN obtained_marks is null then 'Absent' 
                  ELSE to_char(obtained_marks)
             END) show_marks, obtained_marks
from   result_m rm, result_d rd, student st, subject sb, exam_m em, exam_category ec, exam_type et, exam_d ed
where  rd.student_id = st.student_id
and    rd.result_m_id = rm.result_m_id
and    rm.subject_id = sb.subject_id
and    em.exam_category_id = ec.exam_category_id
and    em.exam_type_id = et.exam_type_id
and    rm.exam_m_id = em.exam_m_id 
and    ed.exam_m_id = em.exam_m_id
and    ed.subject_id = rm.subject_id;

select   year, student_id, section_id, section, shift, shift_id, class_id, class, st_name, roll_number,
         exam_category_id, exam_category_name,
         exam_type_id, exam_type_name,
         subject_id, subject_name, show_marks, obtained_marks
from     result_view ;


--8

create or replace view  student_ATTENDANCE_view
as
select ATTENDANCE_D.student_id, first_name||' '||last_name student_name,
       to_char(ATTENDANCE_m.ATTENDANCE_DATE, 'DD-MM-RRRR') dates, status, to_char(ATTENDANCE_m.ATTENDANCE_DATE, 'Month') months
from  student,ATTENDANCE_M,ATTENDANCE_D
where  ATTENDANCE_D.student_id = student.student_id 
and    ATTENDANCE_D.ATTENDANCE_m_id = ATTENDANCE_m.ATTENDANCE_m_id ;


--9

--Class_Routine_view

CREATE OR REPLACE VIEW CLASS_ROUTINE_VIEW 
as
 select class_name, shift_name, section_name, subject_name, class_d.subject_id, detailed_class_name, day_of_week, first_name||' '||last_name teacher_name, 
        ROUTINE_D.start_time, ROUTINE_D.end_time, class_d.class_id,
        class_d.shift_id, class_d.section_id, routine_m.employee_id
 from   class, class_d, shift, section, routine_m, routine_d, employee, subject
 where  class_d.class_id = class.class_id
 and    class_d.shift_id = shift.shift_id
 and    class_d.section_id = section.section_id
 and    routine_d.class_d_id = class_d.class_d_id
 and    routine_d.routine_m_id = routine_m.routine_m_id
 and    routine_m.employee_id = employee.employee_id
 and    class_d.subject_id = subject.subject_id
order by class_d.class_d_id;


--10

create or replace view Teacher_Routine_view
as
select rm.employee_id, first_name||' '||last_name teacher_name,rm.routine_m_id, DETAILED_CLASS_NAME,Day_OF_Week,
        start_time, end_time
from class_d cd, employee e, routine_m rm, routine_d rd
where rd.class_d_id = cd.class_d_id
and rd.routine_m_id = rm.routine_m_id
and rm.employee_id = e.employee_id
order by rm.employee_id ;

--11

create or replace view Re_Admission_view
as
select re_admission.student_id, first_name||' '|| last_name student_name, f_shift_name(CURRENT_shift_ID) current_shift_name, f_shift_name(new_shift_id) new_shift_name,new_class_id,
       f_class_name(current_class_id) current_class_name, f_class_name(new_class_id) new_class_name,
      f_section_name(CURRENT_SECTION_ID) current_section_name, f_section_name(NEW_SECTION_ID) new_section_name, current_roll_number, new_roll_number, RE_ADMISSION_DATE
from   re_admission, student 
where  re_admission.student_id = student.student_id
order by re_admission.student_id  ;


--12

create or replace view class_wise_student_view
as
select s.student_id, cl.class_id, class_name,sh.shift_id, shift_name, sec.section_id, section_name, first_name ||' '|| last_name        student_name, gender, date_of_birth, birth_reg_number, roll_number,   fathers_name, present_address
from  student s, shift sh, section sec, class cl
where s.class_id = cl.class_id
and   s.shift_id = sh.shift_id
and   s.section_id = sec.section_id
order by cl.class_id ;


--13

create or replace view monthly_attendance_count
as
select atm.class_id, f_class_name(atm.class_id) class,atm.shift_id, f_shift_name(atm.shift_id) shift,atm.section_id, 
       f_section_name(atm.section_id) section, attendance_date, atd.student_id,
       roll_number, first_name||' '||last_name student_name, (CASE WHEN Status = 'Absent' THEN 1
                  ELSE 0
             END) Absent, (CASE WHEN Status = 'Present' THEN 1
                  ELSE 0
             END) present
from    attendance_d atd, attendance_m atm, student s
where   atd.attendance_m_id = atm.attendance_m_id 
and     atd.student_id = s.student_id 
order   by atd.student_id, attendance_date ;


select class, section, shift, to_char(attendance_date, 'fmMonth-RRRR'),
       roll_number, student_name, present, absent
from   monthly_attendance_count ;


-----
query_attedance_daily

select f_class_name(atm.class_id) class_name, f_shift_name(atm.shift_id) shift_name, 
       f_section_name(atm.section_id) section_name, attendance_date, roll_number, first_name||' '||last_name, status, ad.student_id
from   attendance_m atm, student s, attendance_d ad
where  atm.attendance_m_id = ad.attendance_m_id
and    ad.student_id = s.student_id
order  by roll_number ;


--14

create or replace view fee_view
as 
select distinct fm.fee_m_id, fm.student_id, fm.admission_id, f_st_std_name(fm.student_id) st_student_name, 
       f_ad_std_name(fm.admission_id) ad_student_name, f_class_name(fm.class_id) class_name, collection_date, 
       paid_amount, due_amount, fee_name, fd.fee_amount, fee_type_name, quantity, 
       fd.fee_amount * quantity sub_total, sessions
from   student s, fee_type ft, fee_amount fa, fee_m fm, fee_d fd, admission a
where  fm.fee_m_id = fd.fee_m_id
and    fa.fee_type_id = ft.fee_type_id 
and    fd.fee_amount_id = fa.fee_amount_id 
and    
       (fm.student_id like nvl(s.student_id, '%')
or      fm.admission_id like nvl(a.admission_id, '%'));


select fee_m_id, st_student_name||ad_student_name, class_name, collection_date, paid_amount, due_amount,
       fee_name, fee_amount, fee_type_name, quantity, sub_total
from   fee_view ;


--15

create or replace view exam_view
as
select em.exam_m_id, em.exam_category_id, exam_type_name, exam_category_name,  
       em.exam_type_id, em.class_id, f_class_name(em.class_id) class_name, em.section_id, 
       f_section_name(em.section_id) section_name, em.shift_id, em.action_date_time, 
       f_shift_name(em.shift_id) shift_name, ed.subject_id, subject_name, exam_date, exam_time, total_marks
from   exam_m em, exam_d ed, subject su, exam_category ec, exam_type et
where  ed.exam_m_id = em.exam_m_id
and    ed.subject_id = su.subject_id 
and    em.exam_type_id = et.exam_type_id
and    em.exam_category_id = ec.exam_category_id
order  by em.exam_m_id ;

select exam_m_id, exam_category_name, exam_type_name, class_name, section_name, shift_name, subject_name, 
       exam_date, exam_time, total_marks
from   exam_view ;


--16

create or replace view student_details_view
as
select STUDENT_ID, FIRST_NAME||' '||LAST_NAME student_name, DATE_OF_BIRTH,  GENDER, RELIGION, BIRTH_REG_NUMBER, FATHERS_NAME,FATHERS_CELL_NUMBER,  MOTHERS_NAME, GUARDIANS_NAME,
GUARDIANS_CELL_NUMBER, SHIFT_name, CLASS_name, SECTION_name,ROLL_NUMBER, PRESENT_ADDRESS,PERMANENT_ADDRESS,STUDENT_IMAGE, ADMISSION_DATE
from student s, shift sh, section sec, class cl
where  s.shift_id = sh.shift_id
and    s.class_id = cl.class_id
and    s.section_id = sec.section_id
order by student_id ;


select  STUDENT_ID, student_name, DATE_OF_BIRTH,  GENDER, RELIGION, BIRTH_REG_NUMBER, FATHERS_NAME,FATHERS_CELL_NUMBER,  MOTHERS_NAME, GUARDIANS_NAME,
GUARDIANS_CELL_NUMBER, SHIFT_name, CLASS_name, SECTION_name,ROLL_NUMBER, PRESENT_ADDRESS,PERMANENT_ADDRESS,STUDENT_IMAGE, ADMISSION_DATE
from  student_details_view 
where  student_id like nvl(:p_student_id, '%') ;




