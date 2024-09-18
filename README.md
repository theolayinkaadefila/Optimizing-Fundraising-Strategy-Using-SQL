# Optimizing-Fundraising-Strategy-Using-SQL

### How much is the total donation?
`Select sum(donation) as "Total Donation" 
from donation_data;`

### What is the total donation by gender?
```
Select gender, Sum(donation) as "Total Donation"
From donation_data
Group by gender; 
```

### Show the total donation and number of donations by gender
```
Select gender, count ( gender) as "No.Of_Donation", sum(donation) as "Total Donation"
From donation_data
Group by gender
order by "Total Donation" desc;
```

### Total donation made by frequency of donation
```
Select sum(d.donation) as "Total Donation", dd.donation_frequency
From donation_data d
Join donor_data dd on dd.id = d.id
Group by dd.donation_frequency
Order by "Total Donation" desc
```

### Total donation and number of donation by Job field
```
Select job_field, Sum(donation) as "Total Donation", count (job_field) as "No Of Donation"
From donation_data
Group by job_field
Order By "Total Donation" Desc;
```

### Total donation and number of donations above $200
```
Select Sum(donation) as "Total Donation",
	Count(Case 
	when donation > 200 
	then 1 
	end) as "No.Of Donation_>_200"
From donation_data;		
```
	
### Total donation and number of donations below $200	
``` 
Select sum(donation) as "Total Donation",
	Count(case 
		 when donation < 200 
		  then 1 
		  end) as "No_Of_Donation_Below_200"
From donation_data;


Select Sum(donation) as "Total Donation", count(id) as "Number Of Donation"
From donation_data
Where donation < 200;
```

### Which top 10 states contributes the highest donations
```
Select Distinct State, sum(donation) as "Total Donation"
from donation_data
Group by state
Order By "Total Donation" desc
Limit 10;
```

### Which top 10 states contributes the least donations
```
Select Distinct State, Sum(donation) as "Total Donation"
From donation_data
Group by state
Order By "Total Donation"
Limit 10;
```

### What are the top 10 cars driven by the highest donors
```
Select d.first_name, d.last_name, sum(d.donation) as total_donation, dd.car
From donation_data d
Join donor_data dd on dd.id = d.id
Group by d.first_name, d.last_name, dd.car
Order By total_donation desc
Limit 10;
```

### Donation amount to Avg, Min, Max Amount donated
```
Select gender,Sum(donation) as total_donation, Round(Avg(donation),2) as Avg_Amount_donated, 
max(donation) as Max_Amount_donated, min(donation) as Min_Amount_donated
from donation_data
Group by gender
```

### Analyze gender by favorite colors and favorite movie genres with amount donated to tailor fundraising campaigns or events.
```
Select  d.gender, sum(d.donation) as total_donation,  dd.movie_genre, dd.favourite_colour
From donor_data dd
Join donation_data d on dd.id = d.id
Group by d.gender, dd.movie_genre, dd.favourite_colour
Order by total_donation desc
Limit 10
```
