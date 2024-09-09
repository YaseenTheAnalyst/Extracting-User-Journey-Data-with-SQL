# User Journey and Purchase Analysis

## **Introduction**

### **Project Overview**

- *The goal of this project is to analyze the user journey of paying customers on a company's website.*
- *We aim to understand the sequence of pages visited by users leading up to their first purchase.*
- *By identifying the most common paths taken by users before making a purchase, we can gain insights into the effectiveness of the website's design, marketing strategies, and content placement.*

**To achieve this, we will extract and process data from three key tables in the database:**
- *1. **`front_interactions`**: Contains all visitor interactions with the website.*
- *2. **`student_purchases`**: Records of user payments and the type of subscription purchased.*
- *3. **`front_visitors`**: Connects visitors to users who created an account.*

**The final output will be a CSV file with the following information:**
 - *`user_id`: The unique ID of the user.*
 - *`session_id`: The session during which the interactions occurred.*
 - *`subscription_type`: The type of subscription purchased.*
 - *`user_journey`: A concatenated string representing the sequence of pages visited by the user before the purchase.*

### Database Tables Overview

#### 1. **`front_interactions` Table**
- This table contains data on all interactions by visitors to the website. 
- Each row represents a single interaction by a visitor during a specific session.

> Columns:
 >- *`interaction_id`: (INT) A unique identifier for each interaction.*
 >- *`visitor_id`: (VARCHAR) A unique identifier for each visitor. This ID is not linked directly to the user ID until a visitor creates an account.*
 >- *`event_date`: (DATETIME) The date and time when the interaction occurred.*
 >- *`session_id`: (VARCHAR) A unique identifier for the session during which the interaction took place.*
 >- *`event_source_url`: (VARCHAR) The URL of the page where the interaction started.*
 >- *`event_destination_url`: (VARCHAR) The URL of the page where the interaction ended.*

#### 2. **`student_purchases` Table**
- This table records information about all purchases made by users, including subscription details.

> Columns:
>- *`user_id`: (INT) A unique identifier for each user who made a purchase.*
>- *`date_purchased`: (DATETIME) The date and time when the purchase was made.*
>- *`purchase_type`: (INT) An indicator of the type of subscription purchased.* 
     >>- *`0` represents a Monthly subscription.*
     >>- *`1` represents a Quarterly subscription.*
     >>- *`2` represents an Annual subscription.*
     >>- *Any other value represents other types of subscriptions.*
>- *`purchase_price`: (DECIMAL) The amount paid by the user for the purchase.* 
>>- *A value of `0` indicates a test or a free purchase.*

#### 3. **`front_visitors` Table**
- This table links visitors (who may or may not have created an account) to users who have registered an account.

> Columns:
>- *`visitor_id`: (VARCHAR) A unique identifier for each visitor. Matches the `visitor_id` in the `front_interactions` table.*
>- *`user_id`: (INT) A unique identifier for each registered user. Matches the `user_id` in the `student_purchases` table.*

### **Analysis Goals**

**The primary goal of this analysis is to generate a comprehensive report showing the journey of users from their first interaction with the website to the point of their first purchase.**
> This report will help in:
- Identifying the most common paths that lead to a purchase.
- Understanding user behavior and preferences.
- Optimizing the website design and content layout for better conversion rates.

> The report will consist of the following columns:
>- *`user_id`: To identify each unique user.*
>- *`session_id`: To differentiate multiple sessions of a user.*
>- *`subscription_type`: The type of subscription purchased by the user.*
>- *`user_journey`: A sequence of pages visited by the user before the purchase, represented as a concatenated string.*

### **Step-by-Step Approach**

> The notebook will follow these steps:
>
>1. **Increase Maximum String Length**: Configure the SQL environment to handle long concatenated strings for user journeys.
>2. **Extract Relevant User Data**: Identify users who made a purchase within a specified date range and exclude test purchases.
>3. **Link Users with Interactions**: Extract and filter user interactions data before their first purchase.
>4. **Assign Aliases to URLs**: Replace raw URLs with more readable aliases for clarity in the final output.
>5. **Combine Page Interactions**: Concatenate the source and destination URLs to form a page-to-page journey string.
>6. **Aggregate the User Journey**: Group the page interactions by user and session to form a complete journey.
>7. **Output the Result**: Format and export the final output to a CSV file for further analysis.

**The following sections of the notebook will detail the SQL code and provide explanations for each step to achieve the desired output.**

### **Summary**
*This project involved a comprehensive analysis of user interactions and purchase behaviors to gain insights into user engagement and subscription patterns. The analysis was conducted using two primary datasets: `user_purchases` and `user_interactions`, which were processed and joined to reveal meaningful patterns and trends.*

### **Key Findings**
1. **Subscription Patterns:**
   - *The `user_purchases` dataset provided valuable information on subscription types and purchase dates. By categorizing subscriptions into types such as Monthly, Quarterly, and Annual, we could analyze user preferences and trends over time.*
   - *Filtering out test or free purchases ensured that the analysis focused on genuine customer behavior.*

2. **Interaction Analysis:**
   - *The `user_interactions` dataset was analyzed to track user engagement before their first purchase. This involved identifying interactions that occurred before the user's first recorded purchase.*
   - *By mapping URLs to user-friendly labels (e.g., Homepage, Sign up, Courses), we were able to categorize and understand user navigation patterns more effectively.*

3. **Efficiency Improvements:**
   - *Optimizations were made to the SQL queries to enhance performance, including the use of `WITH` clauses for intermediate results and avoiding redundant subqueries.*
   - *The revised queries efficiently joined datasets and applied filters to produce accurate and actionable insights.*

### **Implications**
1. **Customer Engagement:**
   - *The insights gained from analyzing user interactions before their first purchase can inform strategies to enhance customer engagement. Understanding common navigation paths and behaviors can help tailor marketing efforts and improve user experience.*

2. **Marketing Strategies:**
   - *By identifying key pages and interactions that lead up to purchases, businesses can optimize their marketing strategies to focus on high-impact areas. This can involve targeted promotions, improved website navigation, and personalized content.*

3. **Future Work:**
   - *Further analysis could explore additional factors influencing purchase decisions, such as time spent on different pages or interaction frequency. Integrating data from other sources (e.g., customer feedback) could provide a more comprehensive view of user behavior.*

### **Conclusion**
*This project successfully demonstrated the use of SQL queries to analyze user purchase and interaction data, leading to actionable insights. The optimization of queries and the clear mapping of interaction data have set the stage for further analysis and improvements in user engagement and marketing strategies.*
