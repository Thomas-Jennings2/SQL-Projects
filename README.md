# SQL-Projects
Examples of SQL querys I have used
# Find the number of unique companies and their total carbon footprint PCF for each industry group, filtering for the most recent year in the database. The query should return three columns: industry_group, num_companies, and total_industry_footprint, with the last column being rounded to one decimal place. The results should be sorted by total_industry_footprint from highest to lowest values.

SELECT industry_group,

COUNT(DISTINCT company) AS num_companies,

ROUND(SUM(carbon_footprint_pcf),1) AS total_industry_footprint
FROM public.product_emissions

	WHERE year IN (SELECT MAX (year) FROM product_emissions)
	
GROUP BY industry_group

ORDER BY total_industry_footprint DESC;


# Aggregation
To first approach this task, I split the question into smaller tasks. I began with aggregating the columns necessary. I counted the unique companies with the alias "num_companies" and calculated the sum of the carbon footprints making sure to round to 1 decimal place as requested.





<img width="1127" height="303" alt="image" src="https://github.com/user-attachments/assets/a37e6544-cfab-4e23-87f5-c697e9600834" />



# Grouping
Next, I combined the current query with a group clause to group the results by the industry group.



<img width="1119" height="487" alt="image" src="https://github.com/user-attachments/assets/2533ec7a-a8f2-4804-9c3f-a933566f02fb" />

# Conditions
The next step was to add the condition clause to only show results from the most recent year in the database. At first I inspected the data to find the most recent year was 2017 and used the condition: WHERE year = 2017. However, I realised it would be more practical if I could write the query as to find the most recent year and use that instead. This makes sense if more recent data is to be added as the query will not return outdated results.To make the query find the most recent year, I used WHERE year IN (SELECT MAX (year) FROM product_emissions). This ensures the query will remain up to date.

<img width="1128" height="438" alt="image" src="https://github.com/user-attachments/assets/b8b23c39-7d48-4003-8e29-15bd896aec30" />

# Organising the results
The last thing to add to this query before it was complete was to order the results from highest to lowest total carbon footprint. This was done simply using the ORDER BY DESC function: Order by descending order of a given parameter. 

# Result
Here are the results when all these queries are combined. 

<img width="1124" height="460" alt="Image" src="https://github.com/user-attachments/assets/3358e3cf-d857-466b-955d-c3d7a3322fe7" />

# Insights
From the results table, as you might expect, the industries with only one company contribute to the least amount of total carbon footprint. Interestingly, the industry with the most companies which is Technology Hardware and Equipment, does not contribute to the most total carbon footprint. This shows that this indusrty is cleaner than both the Capital goods and Materials industries.
