# Resume-Based Interview Questions

> This file contains interview questions that can be asked directly from my resume.
>
> Detailed technical concepts such as Python, OOP, SQL, DBMS, PySpark, AWS, OS, CN, etc. are covered separately in their respective folders.
>
> The purpose of this file is to prepare for questions about my background, projects, internships, certifications, resume claims, decisions, and possible follow-up questions.

---

# 1. Resume Overview

## Q1. Tell me about yourself.

**Answer:**

Refer to `self-introduction.md`.

---

## Q2. Walk me through your resume.

**Answer:**

I am currently pursuing my B.Tech in Artificial Intelligence and Data Science with a 9.06 CGPA. My main technical interests are Python, SQL and Data Engineering. I have worked on a YouTube Data Engineering pipeline using AWS and PySpark, a Python Full-Stack Finance Tracker using FastAPI, and a SQL-based Pizza Sales Analysis project. I have also gained exposure through a Deloitte Data Analytics Job Simulation and virtual internships in Generative AI and MERN Stack.

---

## Q3. What are your strongest technical skills?

**Answer:**

My strongest areas are Python and SQL. I also have practical project experience with PySpark, AWS, ETL and FastAPI. Among these, I am currently focusing most on strengthening my Data Engineering skills.

---

## Q4. Which technology are you most comfortable with?

**Answer:**

I am most comfortable with Python because I have used it in both my Data Engineering and backend projects. I am also comfortable with SQL because I have used it for data analysis and database-related work.

---

## Q5. What is your career interest?

**Answer:**

My current career interest is Data Engineering because I enjoy working with data, building pipelines and understanding how raw data can be transformed into useful information.

---

## Q6. You have both Data Engineering and Full-Stack experience. Which one do you prefer?

**Answer:**

Currently, I prefer Data Engineering because I particularly enjoyed working with ETL, PySpark and AWS in my YouTube project. At the same time, my Full-Stack project helped me understand APIs, backend development and databases.

---

## Q7. Why should we consider you for a Data Engineering role?

**Answer:**

I have a combination of strong programming and database fundamentals along with practical project experience. I have worked with Python, SQL, PySpark, ETL and AWS, and I am also comfortable learning new technologies. As a fresher, I am willing to learn quickly and apply my knowledge to real-world problems.

---

# 2. Education

## Q8. Why did you choose Artificial Intelligence and Data Science?

**Answer:**

I was interested in understanding how data can be used to solve real-world problems. AI and Data Science gave me exposure to programming, databases, data analysis and AI concepts, which eventually increased my interest in working with data.

---

## Q9. How is AI and Data Science related to Data Engineering?

**Answer:**

Data Engineering focuses on collecting, storing, processing and preparing data, while Data Science and AI use that prepared data for analysis and machine learning. So Data Engineering provides the data foundation required by analytics and AI applications.

---

## Q10. What subjects from your degree are useful for this role?

**Answer:**

Programming, databases, data structures, data analysis and other data-related subjects are particularly useful. They helped me develop the fundamentals that I later applied in my projects.

---

## Q11. You have a 9.06 CGPA. How did you maintain it?

**Answer:**

I try to maintain consistency in my academics rather than depending on last-minute preparation. I also manage my project and technical learning alongside academics by planning my time properly.

---

## Q12. Which subject are you strongest in?

**Answer:**

I am most comfortable with programming and database-related subjects because I have also applied those concepts practically through my projects.

---

## Q13. Which subject did you find difficult?

**Answer:**

Some theoretical subjects were initially challenging for me. I usually handle them by breaking the concepts into smaller parts and connecting them with practical examples.

---

# 3. Technical Skills — Resume-Level Questions

## Q14. Where have you used Python?

**Answer:**

I used Python in my YouTube Data Engineering project for data-related processing and in my Finance Tracker project for backend development using FastAPI.

---

## Q15. Where have you used SQL?

**Answer:**

I used SQL extensively in my Pizza Sales Analysis project and also worked with SQL databases in my Finance Tracker project.

---

## Q16. Where have you used PySpark?

**Answer:**

I used PySpark in my YouTube Data Engineering project for processing and transforming the data as part of the ETL pipeline.

---

## Q17. Where have you used AWS?

**Answer:**

My main AWS experience comes from my YouTube Data Engineering project, where I worked with services including S3, Glue, Athena, Lambda and IAM.

---

## Q18. Where have you used FastAPI?

**Answer:**

I used FastAPI in my Finance Tracker project to develop the backend REST APIs.

---

## Q19. Where have you used Power BI?

**Answer:**

I used Power BI in my YouTube Data Engineering project to create dashboards and visualize insights from the processed data.

---

## Q20. How do your technical skills connect together?

**Answer:**

Python and PySpark are useful for data processing, AWS provides cloud services for storage and ETL, SQL and Athena are useful for querying data, and Power BI helps visualize the processed information. Together they form an end-to-end Data Engineering and analytics workflow.

---

## Q21. Which technologies did you learn through projects?

**Answer:**

I gained practical experience with Python, SQL, PySpark, AWS, ETL, FastAPI and Power BI through my projects. My internships and courses also helped me explore additional technologies and concepts.

---

# 4. YouTube Data Engineering Project

## Q22. Explain your YouTube Data Engineering project.

**Answer:**

The project is an end-to-end ETL pipeline for YouTube Trending Data. I worked with raw YouTube data, stored it in AWS S3, processed and transformed it using AWS Glue and PySpark, queried the processed data using Athena, and created Power BI dashboards for analysis.

---

## Q23. Why did you choose YouTube Trending Data?

**Answer:**

I wanted to work with a dataset containing information across different regions and categories. It was a good use case for understanding data ingestion, storage, transformation, querying and visualization as a complete pipeline.

---

## Q24. What was the main objective of the project?

**Answer:**

The main objective was to build an automated pipeline that could take raw YouTube data, process and transform it, and make it available for analysis and visualization.

---

## Q25. What was the complete architecture?

**Answer:**

The high-level flow was:

Raw Data → AWS S3 → AWS Glue/PySpark → Processed Data → Athena → Power BI.

Each component had a specific role in storing, processing, querying or visualizing the data.

---

## Q26. What exactly was your contribution?

**Answer:**

I worked on organizing the raw data, storing it in S3, building the processing and transformation workflow using PySpark and AWS Glue, querying the processed data through Athena, and creating Power BI dashboards.

---

## Q27. Why did you use S3?

**Answer:**

S3 provides scalable cloud object storage and is well suited for storing raw and processed datasets. It also integrates well with other AWS data services.

---

## Q28. Why did you use AWS Glue?

**Answer:**

I used AWS Glue because it provides managed ETL capabilities and integrates with AWS data services. It allowed me to build the data processing workflow without managing the underlying infrastructure myself.

---

## Q29. Why did you use PySpark?

**Answer:**

I used PySpark because it is suitable for processing large datasets and provides distributed data processing capabilities. It also gives me a practical way to perform transformations efficiently.

---

## Q30. Why did you use Athena?

**Answer:**

Athena allows SQL-based querying directly on data stored in S3. It was useful for analyzing the processed data without setting up a separate database server.

---

## Q31. Why did you use Power BI?

**Answer:**

Power BI made it easier to convert the processed data into interactive dashboards and visualize trends and comparisons.

---

## Q32. Where exactly did ETL happen?

**Answer:**

The ETL process involved taking the raw data from storage, transforming and cleaning it using the processing workflow, and making the processed data available for querying and analysis.

---

## Q33. What transformations did you perform?

**Answer:**

The transformations involved preparing the raw data into a cleaner and more consistent structure suitable for analysis. This included data cleaning, selecting relevant fields and performing the required transformations before querying and visualization.

---

## Q34. How did you handle data from multiple regions?

**Answer:**

I organized the data according to its source/region and processed it in a consistent structure so that the datasets could be analyzed together.

---

# 5. Resume Numbers and Project Claims

## Q35. You mentioned 100,000+ records. How did you calculate that?

**Answer:**

The project used YouTube trending datasets from multiple regions and time periods. After bringing the datasets together for processing, the total number of records exceeded 100,000. The record count can be verified by checking the number of rows in the datasets during processing.

---

## Q36. Why is processing 100,000+ records important?

**Answer:**

It demonstrates that the pipeline was designed to handle more than a small sample dataset. It also gave me an opportunity to work with a larger volume of data and understand data-processing performance.

---

## Q37. You mentioned an approximately 80% reduction in manual preprocessing. How did you calculate it?

**Answer:**

I compared the repetitive preprocessing work required in a manual approach with the amount of that work automated through the ETL pipeline. Since tasks such as preparing, cleaning and transforming the data were automated, the manual effort was significantly reduced. Based on that comparison, I estimated an approximately 80% reduction.

---

## Q38. Was the 80% reduction an exact benchmark?

**Answer:**

It was an approximate project-level estimate of manual effort rather than a formal production benchmark. The main purpose of the metric was to represent the reduction in repetitive manual preprocessing after automation.

---

## Q39. What exactly did you automate?

**Answer:**

I automated repetitive data preparation and transformation steps so that the raw data could pass through a consistent processing workflow rather than requiring those steps to be performed manually each time.

---

## Q40. How would you improve this project?

**Answer:**

I would improve monitoring, error handling and data-quality checks. I would also optimize partitioning and transformations for larger datasets and consider adding more robust orchestration and scheduling.

---

## Q41. What happens if the data becomes 10 times larger?

**Answer:**

I would focus on optimizing the Spark transformations, partitioning the data properly, reducing unnecessary shuffles and making sure the storage and processing architecture can scale with the increased volume.

---

## Q42. What happens if one part of the pipeline fails?

**Answer:**

I would use proper error handling and monitoring to identify the failed stage. The pipeline should also be designed so that failures can be retried without unnecessarily processing everything again.

---

# 6. Power BI / Analytics Questions from Resume

## Q43. What did your Power BI dashboards show?

**Answer:**

The dashboards presented insights from the processed YouTube data. They helped visualize trends, comparisons and other relevant aspects of the dataset in an interactive way.

---

## Q44. What KPIs did you use?

**Answer:**

The KPIs were based on the YouTube trending data and focused on measures useful for comparing video performance and trends.

---

## Q45. Why did you use Power BI instead of only SQL queries?

**Answer:**

SQL is useful for querying and analyzing data, while Power BI makes the results easier to communicate through interactive visualizations and dashboards. I used both for different purposes.

---

# 7. Finance Tracker Project

## Q46. Explain your Finance Tracker project.

**Answer:**

The Finance Tracker is a full-stack application where React is used for the frontend and FastAPI is used for the backend. SQLAlchemy handles database interaction and SQLite is used as the database. The application supports transaction management, CRUD operations, search and filtering.

---

## Q47. Why did you choose FastAPI?

**Answer:**

FastAPI is a modern Python framework that makes it straightforward to build REST APIs. It also provides automatic API documentation and data validation, which made it suitable for my project.

---

## Q48. Why did you choose React?

**Answer:**

React provides a component-based approach for building interactive user interfaces. It was suitable for creating the frontend of the Finance Tracker and communicating with the backend APIs.

---

## Q49. Why did you use SQLAlchemy?

**Answer:**

SQLAlchemy provides a structured way to interact with the database from Python. It helped me manage database operations without writing every interaction as raw SQL.

---

## Q50. Why did you use SQLite?

**Answer:**

SQLite is lightweight and easy to set up because it doesn't require a separate database server. For a personal project and development environment, it was sufficient.

---

## Q51. How does React communicate with FastAPI?

**Answer:**

The React frontend sends HTTP requests to the FastAPI REST endpoints. FastAPI processes those requests, interacts with the database when required, and sends the response back to the frontend.

---

## Q52. What CRUD operations did you implement?

**Answer:**

I implemented Create, Read, Update and Delete operations for financial transactions. Users can add, view, modify and delete transaction records.

---

## Q53. What were your REST API endpoints?

**Answer:**

The endpoints were mainly related to transaction management, including creating, retrieving, updating and deleting transactions, along with functionality for searching and filtering records.

---

## Q54. You mentioned 8+ REST APIs. How did you count them?

**Answer:**

I counted the separate API routes implemented for different transaction operations and supporting functionality such as retrieval, creation, updating, deletion, search and filtering.

---

## Q55. You mentioned 1,000+ transaction records. How did you get them?

**Answer:**

I worked with a dataset containing more than 1,000 transaction records for testing the application's transaction management, search and filtering functionality.

---

## Q56. How did you test your APIs?

**Answer:**

I tested the APIs by sending requests for the different operations and checking whether the expected responses and database changes were produced.

---

## Q57. You mentioned reducing data retrieval time. How did you measure it?

**Answer:**

I compared the retrieval behavior before and after improving the backend processing and query handling. The improvement refers to the reduction observed during project testing rather than a production-level performance benchmark.

---

## Q58. What was the biggest challenge in the Finance Tracker?

**Answer:**

One challenge was making sure the frontend, backend and database worked together correctly. I had to handle API communication, database operations and the application's transaction logic consistently.

---

# 8. Pizza Sales SQL Project

## Q59. Explain your Pizza Sales SQL project.

**Answer:**

It was a SQL-based data analysis project using pizza sales data containing more than 10,000 transactions. I used joins, CTEs, aggregations and window functions to analyze sales patterns, product performance and ordering trends.

---

## Q60. Why did you choose this project?

**Answer:**

I wanted to practice SQL using a realistic transactional dataset rather than only solving isolated SQL questions. The project allowed me to apply multiple SQL concepts together for analysis.

---

## Q61. What were the major insights?

**Answer:**

The analysis helped identify sales patterns across different pizza varieties, ordering trends and peak periods. It also helped compare the performance of different products.

---

## Q62. Why did you use JOINs?

**Answer:**

JOINs were useful when information required for the analysis was distributed across multiple related tables. They allowed me to combine that information into a single result.

---

## Q63. Why did you use CTEs?

**Answer:**

CTEs helped me divide complex queries into logical steps. This made the queries easier to read, understand and maintain.

---

## Q64. Why did you use window functions?

**Answer:**

Window functions were useful when I needed calculations across related rows while still retaining individual records. They were useful for ranking and comparative analysis.

---

## Q65. How did you identify peak ordering hours?

**Answer:**

I extracted the relevant time information from the transaction data, grouped the orders by hour and calculated the number of orders for each hour. I then compared the results to identify the periods with the highest order volume.

---

## Q66. What was the most difficult SQL query?

**Answer:**

The more challenging queries were those requiring multiple analytical steps, where I had to combine data, calculate aggregates and then compare or rank the results. CTEs and window functions helped structure these queries.

---

# 9. Deloitte Data Analytics Job Simulation

## Q67. What exactly did you do in the Deloitte Data Analytics Job Simulation?

**Answer:**

It was a virtual job simulation based on business data analytics scenarios. I worked with the provided datasets using Excel and Tableau, performed the required analysis and created dashboards to communicate the findings. I also worked on a pay equity analysis task.

---

## Q68. Was this a real Deloitte internship?

**Answer:**

It was a Deloitte Data Analytics Job Simulation through Forage rather than a traditional employment internship. It gave me exposure to the type of data analytics tasks that could be performed in a business environment.

---

## Q69. What was the manufacturing telemetry task?

**Answer:**

It involved analyzing manufacturing-related telemetry data to identify useful operational patterns and findings. I worked with the provided data and used visualization to communicate the results.

---

## Q70. What did you do in Excel?

**Answer:**

I used Excel to work with and prepare the provided data for analysis, including organizing the data and performing the required analysis based on the business scenario.

---

## Q71. What did you do in Tableau?

**Answer:**

I used Tableau to create visualizations and dashboards from the analyzed data so that important trends and findings could be communicated more clearly.

---

## Q72. What were your dashboards about?

**Answer:**

The dashboards were based on the business requirements of the simulation and focused on presenting relevant patterns and findings from the available datasets.

---

## Q73. What was the pay equity analysis?

**Answer:**

The task involved analyzing employee-related data to understand compensation patterns and identify differences in pay across the available groups.

---

## Q74. What did you learn from the Deloitte simulation?

**Answer:**

I learned how data analysis can be approached from a business perspective. I also gained practical exposure to Excel, Tableau, data visualization and communicating findings from data.

---

## Q75. Did you use ChatGPT or other resources during the simulation?

**Answer:**

Yes, I used online learning resources and AI tools such as ChatGPT when I needed help understanding certain concepts or tasks. I also used the requirements and datasets provided by the simulation to complete and understand the work.

---

# 10. Generative AI Virtual Internship — SmartBridge

## Q76. What did you do during your Generative AI internship?

**Answer:**

During the internship, I worked on an Emotion Tracker project. The objective was to develop an AI-based application that could identify or track emotions based on the given input. The internship gave me practical exposure to working on an AI-related application.

---

## Q77. What was the Emotion Tracker project?

**Answer:**

The Emotion Tracker was an AI-based project designed to identify the emotion associated with a given input and provide an emotion-related output.

---

## Q78. What was the main objective of the project?

**Answer:**

The objective was to use an AI-based approach to understand the emotional information in the input and present the identified emotion to the user.

---

## Q79. What did you learn from the internship?

**Answer:**

I learned the basic workflow involved in developing an AI-based application, from understanding the problem and input to working with an AI model and producing a useful output.

---

## Q80. Was this your strongest technical project?

**Answer:**

It gave me useful introductory exposure to AI-based development, but my stronger practical project experience currently comes from my Data Engineering and Python Full-Stack projects.

---

# 11. MERN Stack Virtual Internship — SmartInternz

## Q81. What did you do during your MERN Stack internship?

**Answer:**

The internship was mainly based on development scenarios. I worked through the given scenarios and prepared documentation related to a Flight Ticket Booking system.

---

## Q82. What was the Flight Ticket Booking system?

**Answer:**

It was a scenario-based web application concept where the requirements and development aspects of a flight ticket booking system were studied and documented.

---

## Q83. What exactly was your contribution?

**Answer:**

My main contribution was documentation. I worked on understanding the flight ticket booking scenario and documenting the requirements and development-related aspects of the system.

---

## Q84. Did you develop the complete MERN application yourself?

**Answer:**

No. The internship was scenario-based, and my contribution was mainly focused on understanding the development requirements and preparing documentation rather than building a complete production-level MERN application.

---

## Q85. What did you learn from the MERN internship?

**Answer:**

I gained an overall understanding of how the MERN stack components work together and how requirements can be converted into a structured development approach.

---

## Q86. Why did you learn MERN if you are interested in Data Engineering?

**Answer:**

I wanted to explore full-stack development and understand how web applications work end to end. Later, through my own projects, I became more interested in Python, SQL and Data Engineering.

---

# 12. NPTEL — Social Networks

## Q87. Why did you choose the Social Networks course?

**Answer:**

I was interested in understanding how entities and relationships can be represented and analyzed as networks. The course gave me exposure to the fundamentals of network structures and their analysis.

---

## Q88. What did you learn from the course?

**Answer:**

I learned the fundamentals of social network analysis and how relationships between different entities can be represented and studied as network structures.

---

## Q89. How is Social Networks related to your technical background?

**Answer:**

It helped me understand another way of working with structured relationships between data points. It also gave me exposure to concepts involving networks and analyzing connections.

---

## Q90. What does NPTEL Elite certification mean?

**Answer:**

Elite is a performance category associated with the NPTEL certification based on the candidate's performance in the course and examination.

---

# 13. Why Questions

## Q91. Why Data Engineering?

**Answer:**

I enjoy working with data and understanding how raw data can be collected, processed and transformed into useful information. My YouTube project increased my interest in ETL, PySpark and AWS, so I decided to focus more on Data Engineering.

---

## Q92. Why Python?

**Answer:**

Python has simple syntax and a large ecosystem for data processing, automation, backend development and analytics. I also found it comfortable to use across different types of projects.

---

## Q93. Why SQL?

**Answer:**

SQL is fundamental for working with structured data and databases. I enjoy using it to retrieve, transform and analyze data, and I have applied it in my Pizza Sales project and other work.

---

## Q94. Why AWS?

**Answer:**

AWS provides a wide range of cloud services that can be combined to build scalable data solutions. Working with AWS in my project helped me understand how cloud services can be used in a real data pipeline.

---

## Q95. Why did you build two different types of projects?

**Answer:**

I wanted to develop both specialization and versatility. The Data Engineering project helped me focus on data pipelines and cloud technologies, while the Full-Stack project helped me understand APIs, backend development and databases.

---

## Q96. Why did you choose FastAPI instead of another backend framework?

**Answer:**

I wanted to work with a Python-based backend framework, and FastAPI was suitable because it makes REST API development straightforward and provides useful features such as automatic documentation and validation.

---

## Q97. Why did you choose SQLite instead of MySQL?

**Answer:**

For my personal project, SQLite was sufficient because it is lightweight and doesn't require a separate database server. If the application needed a larger multi-user production database, I would consider a database such as MySQL or PostgreSQL.

---

# 14. Project Cross-Questions

## Q98. Which project are you most proud of?

**Answer:**

I'm most proud of my YouTube Data Engineering project because it helped me understand an end-to-end data pipeline and allowed me to work with Python, PySpark and multiple AWS services together.

---

## Q99. Which project taught you the most?

**Answer:**

The YouTube Data Engineering project taught me the most because it required me to understand how different technologies work together instead of using only one technology.

---

## Q100. What was the biggest challenge across your projects?

**Answer:**

The biggest challenge was connecting different components correctly and debugging issues when the expected result was not produced. Working through those problems helped me improve my understanding of the technologies rather than just following tutorials.

---

## Q101. Did you build these projects completely by yourself?

**Answer:**

I worked on the projects myself while also using documentation, tutorials and online resources whenever I needed help. I consider the projects my own practical work, but I also believe using learning resources is part of the development process.

---

## Q102. What did you do when you got stuck?

**Answer:**

First, I tried to understand the error and debug it myself. If I couldn't resolve it, I referred to official documentation, tutorials or other learning resources. After finding a solution, I tried to understand why it worked rather than simply copying it.

---

## Q103. Did you use ChatGPT while building your projects?

**Answer:**

Yes, I used ChatGPT as a learning and debugging resource when I was stuck or needed clarification. I used it to understand concepts, troubleshoot issues and improve my implementation, but I also made sure to understand the code and workflow I used.

---

## Q104. What would you improve if you rebuilt your YouTube project?

**Answer:**

I would improve monitoring, error handling, data-quality validation and pipeline orchestration. I would also make the pipeline more scalable and production-oriented by adding better logging and failure recovery.

---

## Q105. What would you improve in your Finance Tracker?

**Answer:**

I would improve authentication and authorization, make the database more suitable for production, add stronger validation and error handling, and improve the application's deployment and scalability.

---

## Q106. What would you improve in your Pizza Sales project?

**Answer:**

I would extend the analysis with more advanced business metrics and create a visualization layer so that the SQL results could be presented more interactively.

---

# 15. Strengths, Weaknesses and Career Questions

## Q107. What are your strengths?

**Answer:**

My main strengths are that I am willing to learn, I enjoy understanding how things work, and I like applying concepts through practical projects. I also try to be consistent in improving my technical skills.

---

## Q108. What is your weakness?

**Answer:**

Sometimes I spend more time than necessary trying to understand a problem in depth. I'm working on improving this by setting time limits for initial investigation and then using documentation or asking for help when necessary.

---

## Q109. How do you learn a new technology?

**Answer:**

I first understand the purpose and basic concepts, then I follow a small practical example and finally try to use the technology in a project. Working on a real problem helps me remember the concepts better.

---

## Q110. Where do you see yourself in the next few years?

**Answer:**

I want to become a strong Data Engineer with solid knowledge of Python, SQL, cloud technologies and distributed data processing. I also want to gain experience working on real-world data systems and gradually take more responsibility.

---

## Q111. Are you willing to learn technologies other than those on your resume?

**Answer:**

Yes. My projects and internships have already required me to learn different technologies, and I'm comfortable learning new tools based on the requirements of the role.

---

## Q112. Are you comfortable working in a team?

**Answer:**

Yes. I am comfortable working with others, discussing problems and learning from teammates. I also understand that professional projects require communication and coordination in addition to technical skills.

---

# 16. Final Resume Cross-Questions

## Q113. What is the strongest point in your resume?

**Answer:**

I would say my strongest point is the combination of academic performance and practical projects. My Data Engineering project gave me hands-on exposure to Python, PySpark, AWS and ETL, while my other projects gave me experience with SQL and backend development.

---

## Q114. What is one area missing from your resume that you want to improve?

**Answer:**

I want to gain more experience with production-level Data Engineering practices such as advanced orchestration, monitoring, testing, optimization and working with larger real-world datasets.

---

## Q115. If we remove your projects, what technical skill can you demonstrate?

**Answer:**

I can demonstrate my fundamentals in Python and SQL and explain the concepts I have learned through academics and practice. My projects are where I have applied those fundamentals practically.

---

## Q116. Which project should we discuss first?

**Answer:**

I would prefer to discuss my YouTube Data Engineering project because it is closely related to the Data Engineering role and covers Python, PySpark, AWS, ETL, SQL and data visualization.

---

## Q117. If we ask you something you don't know, what will you do?

**Answer:**

I would be honest that I don't know the answer rather than guessing. If possible, I would explain what I know about the related concept and make sure I learn the missing part afterward.

---

## Q118. Why should we hire you instead of another fresher?

**Answer:**

I have built a good foundation in Python, SQL and Data Engineering and have applied those skills in practical projects. I am also comfortable learning new technologies and solving problems when I don't initially know the solution. I believe my willingness to learn and my practical exposure will help me adapt quickly to the role.

---

# Quick Revision — Most Important Questions

Before an interview, prioritize these questions:

1. Tell me about yourself.
2. Walk me through your resume.
3. Why Data Engineering?
4. Explain your YouTube Data Engineering project.
5. Explain the complete architecture.
6. Why S3?
7. Why Glue?
8. Why PySpark?
9. Why Athena?
10. How did you process 100,000+ records?
11. How did you calculate the 80% reduction?
12. What exactly did you automate?
13. What happens if data becomes 10× larger?
14. Explain your Finance Tracker.
15. Why FastAPI?
16. Why SQLAlchemy?
17. Why SQLite?
18. What were your APIs?
19. Explain your Pizza Sales project.
20. Explain your Deloitte simulation.
21. What did you do in Excel?
22. What did you do in Tableau?
23. What was the pay equity task?
24. What did you do in the SmartBridge internship?
25. What was the Emotion Tracker?
26. What did you do in the MERN internship?
27. What was your role in the Flight Ticket Booking scenario?
28. Why did you choose Social Networks in NPTEL?
29. What are your strengths?
30. What is your weakness?
31. Why should we hire you?
32. What would you improve in your projects?
33. What did you do when you got stuck?
34. Did you use ChatGPT?
35. Which project are you most proud of?

---

# Important Rule

I should be able to explain every technology, project claim and certification mentioned in my resume.

If an interviewer asks something outside this file, I should move to the corresponding technical preparation folder.

Examples:

Python question → `Python/`

OOP question → `OOP/`

SQL question → `SQL/`

Database question → `DBMS/`

PySpark question → `PySpark/`

AWS question → `AWS/`

Operating System question → `OS/`

Computer Networks question → `CN/`

Power BI question → `PowerBI/`

FastAPI question → `FastAPI/`

The purpose of this file is **not to replace those folders**. It prepares me for questions that start from my resume and then branch into those technical concepts.