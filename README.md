# Nonsmokers

Evaluating an HR dataset about absenteeism and health. You will use your skills to provide a data-driven approach to determine how to provide a bonus and incentive to healthy employees. You will also develop a database, and SQL queries to answer questions and build a dashboard that meets a wireframe specification.

#HR Request to Data Analytics Team 
- Provide a list of Healthy Individuals and low Absenteeism for our healthy bonus program - Total Budget $1000 USD
- Calculate a Wage Increase or annual compensation for Non-smokers for an Insurance budget of $983,221 for all Non-Smokers
- Create a Dashboard for HR to understand Absenteeism at work based on the approved wireframe.

  #SQL Queries
  Join Table:
   --create a join table
select * from Absenteeism_at_work a
left join compensation b
on a.ID = b.ID
left join Reasons r on
a.Reason_for_absence = r.Number;

--find the healthiest employee for the bonus 
select * from Absenteeism_at_work
where Social_drinker = 0 and Social_smoker = 0
and Body_mass_index < 25 and 
Absenteeism_time_in_hours < (select AVG(Absenteeism_time_in_hours) from Absenteeism_at_work)

--compensation rate increase for non-smokers/ budget 983,221 so 0.68 increase per hour/$1,414 per year
select count(*) as nonsmokers from Absenteeism_at_work
where Social_smoker = 0

--Optimizations
select
a.ID,
r.Reason,
Month_of_absence,
Body_mass_index,
CASE when Body_mass_index < 18.5 then 'Underweight'
	 when Body_mass_index is between 18.5 and 24.9 then 'Healthy weight'
	 when Body_mass_index is between 25 and 30  then 'Overweight'
	 when Body_mass_index > 18.5 then 'FAT'
	 ELSE 'UNKNOWN'end as BMI_Category,
CASE when Month_of_absence IN (12,1,2) Then 'Winter'
when Month_of_absence IN (3,4,5) Then 'Springr'
when Month_of_absence IN (6,7,8) Then 'Summer'
when Month_of_absence IN (9,10,11) Then 'Fall'
Else 'UNKNOWN' END as Seasons_name,
Seasons, 
Month_of_absence,
Day_of_the_week,
Transportation_expense,
Education,
Son,
Social_drinker,
Social_smoker,
Pet,
Disciplinary_failure,
Age,
Work_load_Average_day,
Absenteeism_time_in_hours
from Absenteeism_at_work a
left join compensation b
on a.ID = b.ID
left join Reasons r on
a.Reason_for_absence = r.Number;


#PowerBI Tool 
Filters
Line Graphs 
Employee Categories 
HR Analytics: Absenteeism
Trends and Times
Reasons and Comparisons
