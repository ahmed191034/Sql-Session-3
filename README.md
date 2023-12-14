# Sql-Session-3
In this SQL class, we covered data aggregation, grouping, and conditional statements. Explored averaging, identifying top data users, and filtering feedback. Demonstrated conditional expressions, data categorization, and data cleaning, showcasing comprehensive SQL skills for effective data analysis.
# Aggregating Data & group by
select service_type,avg(monthly_rate) as Avg_Monthly_Rate
from service_packages
group by service_type;

# Just using round function
select service_type,round(avg(monthly_rate),2) as Avg_Monthly_Rate
from service_packages group by service_type;

select customer_id ,max(data_used) as MAX_data_Usage from service_usage
group by customer_id order by max_data_usage desc limit 1;

select sum(minutes_used) as Total_Minutes from service_usage
where service_type="Mobile"; 

select rating,count(rating) as Overall_Rating from feedback
group by rating order by rating asc;

# Having clause
select customer_id,sum(rating) as Rating_Individual from feedback
group by customer_id having rating_individual<10  order by customer_id asc;

select customer_id,service_type,round(sum(data_used),2) as Total_Data_Used,
round(Sum(Minutes_used),2) as Total_Minutes_Used from service_usage
group by service_type, customer_id order by customer_id desc;

# Case Statements
select customer_id ,
case 
when subscription_date >"2023-01-01" then "New"
else "old"
end as customer_type from customer;

select * from feedback
where customer_id =337;

select customer_id,feedback_id,service_impacted,
case when service_impacted ="Mobile" then "Voice"
else "Digital"
end as Service_Categories from feedback;


select customer_id,data_used,minutes_used,
case when data_used>(select avg(data_used) from  service_usage) then "High"
else "Low"
end as Data_Usage from service_usage;

set sql_safe_updates=0;
update billing
set discounts_applied=
case when payment_date>due_date then amount_due*0.1
else amount_due*0.05
end ;

