# Advanced Prompting

---

## **What is Prompt Engineering?**

Prompt engineering is not about "hacking" AI. It's about _clearly communicating your intent_ to an LLM. Just as a precise database query leads to relevant results, a well-crafted prompt ensures useful answers from the model. Previously, we saw how vague prompts lead to generic and unhelpful outputs.

## **Why Focus on Advanced Techniques?**

While we've learned to write _reasonable_ prompts, we often hit limitations. LLMs struggle with complex tasks requiring deeper reasoning, multiple steps, or integration of external knowledge. Today, we'll cover advanced techniques that enable us to:

- Guide LLMs to deeper reasoning: Learn techniques like **Chain of Thought (CoT)**, **Tree of Thoughts (ToT)**, and **Self-Consistency** to break down complex problems into smaller steps and solve them systematically.
- Improve answer reliability: Explore **Meta Prompting**—how to optimize prompts for better results, and **Prompt Chaining**—how to combine multiple prompts into complex workflows.
- Integrate external knowledge: Introduce techniques like **Retrieval-Augmented Generation (RAG)** and **Cache Augmented Generation (CAG)**, allowing LLMs to use external databases and knowledge graphs for more accurate and contextually relevant answers.
- Leverage multimodality: Explore **Multimodal Prompting**, combining text prompts with images, videos, or other data types.
- Program Assisted LLMs: See how to use programming languages (like Python) to extend LLM capabilities and automate more complex tasks.

---

## Chain of Thought

Chain-of-Thought (CoT) prompting is a technique that improves the ability of large language models (LLMs) to solve complex problems by guiding them to express their reasoning process step by step before providing a final answer. This method mimics human reasoning and increases the accuracy and transparency of results.

**Prompt Example:**

> "I have 3 apples, receive 2 more, and eat 1. How many apples do I have left? Explain your process step by step."

**Expected Output:**

1. "I start with 3 apples."
2. "I add 2 apples: 3 + 2 = 5."
3. "I eat 1 apple: 5 - 1 = 4."
4. "Final result: I have 4 apples left."

This approach helps the model better understand and solve tasks that require logical reasoning or multiple steps. It's especially useful for math, logic, and symbolic reasoning tasks.

### Practical Example

```
You are a senior data analyst and will help me with the following task.

Explain step by step how you would:
1. Identify outliers in this sales dataset,
2. Justify each decision step,
3. Propose how to handle outliers (remove, replace, transform).

The dataset is attached below. Also state which metrics and visualizations you would use.

<data>
| Date | Product | Region | Units_Sold | Unit_Price | Total_Revenue | Discount_Applied |
| --- | --- | --- | --- | --- | --- | --- |
| 2024-01-03 | Notebook | A | Prague | 120 | 25.50 | 3060.00 | 0.00 |
| 2024-01-04 | Smartphone | B | Brno | 350 | 15.20 | 5320.00 | 1.50 |
| 2024-01-05 | Tablet | C | Ostrava | 80 | 18.00 | 1440.00 | 0.00 |
| 2024-01-06 | Notebook | A | Prague | 115 | 25.50 | 2932.50 | 0.00 |
| 2024-01-07 | Smartphone | B | Brno | 360 | 15.20 | 5472.00 | 1.50 |
| 2024-01-08 | Tablet | C | Ostrava | 78 | 18.00 | 1404.00 | 0.00 |
| 2024-01-09 | Notebook | A | Plzen | 130 | 25.50 | 3315.00 | 2.00 |
| 2024-01-10 | Smartphone | B | Liberec | 200 | 15.20 | 3040.00 | 0.00 |
| 2024-01-11 | Tablet | C | Brno | 90 | 18.00 | 1620.00 | 0.00 |
| 2024-01-12 | Notebook | A | Ostrava | 5000* | 25.50 | 127500.00* | 0.00 |
| 2024-01-13 | Smartphone | B | Prague | 340 | 15.20 | 5168.00 | 1.00 |
| 2024-01-14 | Tablet | C | Plzen | 85 | 18.00 | 1530.00 | 0.00 |
| 2024-01-15 | Notebook | A | Brno | 125 | 25.50 | 3187.50 | 0.00 |
| 2024-01-16 | Smartphone | B | Ostrava | 355 | 15.20 | 5396.00 | 1.50 |
| 2024-01-17 | Tablet | C | Liberec | 82 | 18.00 | 1476.00 | 0.00 |
</data>
```

---

> Note: Rows marked with \* are intentionally extreme values (outliers) for model testing.

---

## Meta-Prompting

**Meta-prompting** allows LLMs to optimize another prompt for a specific task. In this example, we focus on data cleaning and error minimization.

1. **Problem:** We have "dirty" CSV data with errors (missing values, invalid formats, duplicates, inconsistencies in names).
2. **Original Prompt:** A simple prompt for data cleaning may not be optimal (e.g., "Clean the following CSV data...").
3. **Meta-Prompt:** Instruct the LLM to propose an _improved_ prompt for data cleaning. Example: "You are a data cleaning expert… Propose a detailed and robust prompt that effectively cleans CSV data with missing values, invalid formats, duplicates, and name inconsistencies."
4. **Meta-Prompt Output:** The LLM generates an improved prompt (e.g., with steps for handling missing values, date formatting, removing duplicates, and fuzzy name matching).
5. **Use the Improved Prompt:** Use the generated improved prompt to clean the original data.

### Practical Example

```
You are a senior data analyst and will help me with the following task.

1. First, reflect on the most common pitfalls when prompting for data cleaning (e.g., ignoring duplicates, mishandling missing values, inconsistent data formats).
2. Based on these pitfalls, create a final prompt that:
   a. Describes specific pre-cleaning steps (format validation, duplicate detection),
   b. Specifies methods for imputing missing values,
   c. Includes consistency checks between related columns,
   d. Proposes a report on performed modifications.

<data>
| Order_ID | Date | Customer_Email | Units | Unit_Price | Total | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| 1001 | 2024-03-01 | jan.novak@company.com | 10 | 15.00 | 150.00 |  |
| 1002 | 03/02/2024 | petra.svobodova@fs.com |  | 20.00 |  | check |
| 1003 | 2024-03-03 | pavel@ | 5 | 18.00 | 90.00 |  |
| 1004 | 2024-03-03 | lucie.kralova@cs.com | 8 | 18.00 | 144.00 | duplicate |
| 1004 | 2024-03-03 | lucie.kralova@cs.com | 8 | 18.00 | 144.00 |  |
| 1005 | 2024-3-05 | jiri.hrdlicka@cs.com | 12 | 17.50 | 210.00 |  |
| 1006 | 2024-03-06 | eva.kovarikova@cs | 7 | 16.00 | 112.00 |  |
| 1007 | 2024-03-07 | martin.novak@cs.com | 15 | 15.00 | 225.00 |  |
</data>
```

> Note: Intentional issues included—non-uniform date formats, missing Units and Total, various price formats, duplicate rows, and invalid emails.

---

## Self-Consistency

LLMs (like GPT) sometimes give random or inconsistent answers. **Self-Consistency is a technique to address this.** It works as follows:

1. **Submit the same prompt multiple times:** Send the same question to the LLM repeatedly (e.g., 3x).
2. **Compare and combine answers:** See which parts of the answers are similar or appear in multiple responses.
3. **Select the most consistent result:** Combine similar parts from different answers to create a final, more robust answer.

**Self-Consistency is like voting—the more generations agree, the more likely the result is correct.**

### Practical Example

```
You are a senior data analyst and will help me with the following task.

1. Choose three different clustering techniques (e.g., K-means, DBSCAN, hierarchical clustering).
2. For each:
   a. Describe the basic principle of the algorithm and key hyperparameters,
   b. Explain how you would select the number of clusters or other parameters,
   c. Show an example output (e.g., centroids, silhouette score).
3. Compare the results of the three methods:
   a. Calculate and compare quality metrics (silhouette, Davies–Bouldin),
   b. Assess differences in cluster size and shape.
4. Based on the comparison, select the "most consistent" method:
   a. Briefly justify your choice,
   b. Suggest further validation (visual inspection, stability test).

<data>
| Customer_ID | Age | Annual_Income | Spending_Score | Tenure_Years |
| --- | --- | --- | --- | --- |
| 1001 | 25 | 35,000 | 62 | 1.2 |
| 1002 | 45 | 58,000 | 48 | 3.5 |
| 1003 | 33 | 72,000 | 77 | 2.1 |
| 1004 | 23 | 25,000 | 81 | 0.8 |
| 1005 | 52 | 90,000 | 29 | 5.0 |
| 1006 | 39 | 61,000 | 68 | 4.3 |
| 1007 | 28 | 40,000 | 55 | 1.7 |
| 1008 | 47 | 85,000 | 31 | 6.2 |
| 1009 | 31 | 55,000 | 73 | 2.5 |
| 1010 | 54 | 95,000 | 27 | 7.1 |
</data>
```

---

## Generate Knowledge Prompting

LLMs (like GPT) have vast knowledge, but sometimes you need to extract and organize it for a specific task. **Generate Knowledge Prompting is a technique for this.** It works as follows:

1. **Break the problem into smaller steps:** Instead of having the LLM solve the whole problem at once, break it into a series of smaller questions or tasks.
2. **Generate knowledge step by step:** Each step generates specific information or facts relevant to the overall problem. These are stored and used in subsequent steps.
3. **Use generated knowledge for the final solution:** The last step uses all accumulated information to solve the original problem.

### Practical Example

```bash
You are a senior data analyst and will help me with the following task.

1. First, describe the domain context of customer segmentation:
   a. Goals (targeted marketing, increased retention),
   b. Key types of segmentation (demographic, behavioral, psychographic),
   c. Advanced methods (RFM, clustering).
2. Then generate SQL queries to extract three cohorts:
   a. RFM cohort:
      <sql>
      WITH rfm AS (
        SELECT
          customer_id,
          DATEDIFF(day, MAX(order_date), GETDATE()) AS recency,
          COUNT(order_id) AS frequency,
          SUM(total_amount) AS monetary
        FROM orders
        GROUP BY customer_id
      )
      SELECT * FROM rfm
      WHERE recency <= 30 AND frequency >= 5 AND monetary >= 1000;
      </sql>
   b. Demographic cohort (25–34 years, Prague):
      <sql>
      SELECT customer_id, age, city
      FROM customers
      WHERE age BETWEEN 25 AND 34
        AND city = 'Prague';
      </sql>
   c. Behavioral cohort (more than 1 purchase in the last year):
      <sql>
      SELECT DISTINCT customer_id
      FROM orders
      WHERE order_date >= DATEADD(year, -1, GETDATE())
      GROUP BY customer_id
      HAVING COUNT(order_id) > 1;
      </sql>

<data>
| customer_id | order_date | total_amount | age | city |
| --- | --- | --- | --- | --- |
| 1001 | 2024-04-10 | 1,200 | 28 | Prague |
| 1002 | 2024-03-15 | 800 | 35 | Brno |
| 1003 | 2024-05-01 | 1,500 | 32 | Prague |
| 1004 | 2023-12-20 | 200 | 45 | Ostrava |
| 1005 | 2024-02-28 | 3,000 | 27 | Prague |
| 1006 | 2024-01-05 | 950 | 29 | Plzen |
| 1007 | 2023-11-30 | 400 | 31 | Prague |
| 1008 | 2024-04-22 | 2,200 | 26 | Liberec |
| 1009 | 2024-03-03 | 1,100 | 34 | Prague |
| 1010 | 2024-05-05 | 700 | 40 | Brno |
</data>
```

---

## Prompt Chaining

LLMs (like GPT) are great at solving simple tasks, but more complex problems often require multiple steps. **Prompt Chaining is a technique that enables this.** It works as follows:

1. **Break the problem into smaller steps:** Identify a sequence of logical steps needed to solve the overall problem.
2. **Create a series of prompts:** Each step corresponds to a separate prompt sent to the LLM.
3. **Link the prompts:** The output from one prompt becomes the input for the next prompt in the chain.

### Practical Example

- Prompt 1 (clean data and prepare for analysis):

```bash
You are an experienced data analyst.

You have a CSV file with product sales information from an e-shop (see below).
Check the data for missing values, inconsistent formats, and duplicate records.
Remove duplicates. Convert the 'Date' column to the correct date format.
Create a new column 'Total_Revenue' that calculates total revenue for each row (Units_Sold * Unit_Price).

Return the cleaned and prepared dataset in CSV format.

<data>
Date,Product,Category,Units_Sold,Unit_Price,Origin
2023-10-26,Microphone,Electronics,50,499.99,China
2023-10-26,Book "Python for Beginners",Books,120,299.99,USA
2023-10-27,Headphones,Electronics,80,799.99,Vietnam
2023-10-27,T-shirt with print,Clothing,250,399.99,Bangladesh
2023-10-28,Microphone,Electronics,65,499.99,China
2023-10-28,Book "Data Science for Advanced",Books,75,599.99,USA
2023-10-29,Headphones,Electronics,90,799.99,Vietnam
2023-10-29,Jeans,Clothing,180,699.99,Bangladesh
2023-10-30,Microphone,Electronics,70,499.99,China
2023-10-30,Book "Machine Learning",Books,100,449.99,USA
</data>
```

- Prompt 2 (identify key sales elements and trends):

```bash
You are a data analyst specializing in sales analysis.

You have the cleaned dataset from the previous prompt.
Identify the 5 best-selling products by units sold.
Calculate total revenue for each product category.
Determine monthly sales trends (e.g., how sales differ by month).

Return the results as a bulleted list with:
1) Top 5 best-selling products
2) Total revenue by category
3) Monthly sales trends.
```

- Prompt 3 (bulleted summary):

```bash
You are an experienced data analyst and machine learning specialist.

You have historical sales data (see below).
Create a simple predictive model (e.g., linear regression) to forecast total revenue for the next month.
Use only the 'Date' and 'Total_Revenue' columns.
Evaluate model performance using metrics such as RMSE (Root Mean Squared Error).

Return:
1) Predicted total revenue for next month,
2) RMSE value
3) A brief explanation of how the model works and its potential limitations.
```

---

## Tree of Thoughts

LLMs are often good at generating a single answer, but more complex problems may have multiple possible solutions. **Tree of Thoughts is a technique that allows LLMs to explore different solution paths.** It works as follows:

1. **Generate "thoughts":** For each step of the problem, the LLM generates several different ideas or possible actions.
2. **Build a tree:** These ideas are organized into a tree structure, where each branch represents a different solution path.
3. **Evaluate thoughts:** The LLM evaluates each idea based on its relevance and potential to lead to a good solution.
4. **Explore the best branches:** The LLM focuses on exploring the branches of the tree with the highest ratings.
5. **Repeat steps 3-4:** This process continues until a satisfactory solution is found or the maximum tree depth is reached.

### Practical Example

```
You are a senior data analyst and will help me with the following task.

1. Create a tree of possible data preprocessing strategies, where each branch represents a different approach (e.g., imputing missing values, scaling, encoding categories).
2. For each branch:
   a. Describe the process,
   b. List pros and cons,
   c. Estimate the impact on the output model.
3. Select the optimal branch:
   a. Define criteria (e.g., preserving variability, computation speed),
   b. Choose the best path and justify your choice.

<data>
| Record_ID | Age | Income | Gender | Purchased | Feedback_Score | Region |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | 25 | 35,000 | M | Yes | 4 | Prague |
| 2 | 40 |  | F | No | 3 | Brno |
| 3 | 31 | 58,000 |  | Yes |  | Ostrava |
| 4 |  | 72,000 | M | No | 5 | Prague |
| 5 | 22 | 24,000 | F | Yes | 2 | Plzen |
| 6 | 29 | 41,000 | M |  | 4 | Brno |
| 7 | 35 | 66,000 | F | No | 3 | Liberec |
| 8 | 28 | 49,000 | M | Yes |  | Ostrava |
| 9 | 47 | 85,000 | F | No | 5 | Prague |
| 10 | 30 | 54,000 |  | Yes | 4 | Plzen |
</data>
```

---

## Program-Aided Language Models

LLMs are great at generating text, but have limitations when it comes to precise calculations and data manipulation. **Program-Aided Language Models (PALM) solve this by allowing LLMs to generate code (e.g., Python), which is then executed and the results are used to complete the task.**

**How does it work?**

1. **Identify the need for programming:** When the LLM encounters a task requiring calculations or data manipulation, it identifies the need for code.
2. **Generate code:** The LLM generates code (e.g., Python) to solve the specific problem.
3. **Run the code:** The generated code is executed in a safe environment (sandbox).
4. **Use the results:** The results of the executed code are returned to the LLM, which uses them to complete the original task and generate the answer.

### Practical Example

- "Write a Python function to clean missing values, then ask the model to use it and explain the output."

```bash
You are a data analyst specializing in text analysis.

You have CSV data with customer comments (see below).
Write a Python function using the NLTK (Natural Language Toolkit) library to perform basic sentiment analysis for each comment.
The function should return a sentiment score for each comment (-1 = negative, 0 = neutral, +1 = positive).

Return the results as a CSV with a new column 'Sentiment_Score'.

<data>
Customer_ID,Comment
1,"The product is good, but the price could be lower."
2,"Great product! I recommend it to everyone."
3,"A bit disappointing. I expected more."
4,"Poor quality and quick wear."
5,"Complete satisfaction!"
6,"No comment"
7,"Fast delivery and good product."
8,"Average product. Nothing special."
9,"Very bad experience. Returning the goods."
10,"Great value for money!"
</data>
```

- "Insert a small R script for univariate analysis and ask for a commentary on the results."

```bash
You are an experienced data analyst and data interpretation expert.

You have CSV data with customer comments and their corresponding sentiment scores (see below).
Analyze the results of the sentiment analysis and write a short report summarizing overall customer satisfaction with the product based on this data.

Pay special attention to identifying the most common negative and positive themes in the comments.

<data>
Customer_ID,Comment,Sentiment_Score
1,"The product is good, but the price could be lower.",-0.2
2,"Great product! I recommend it to everyone.",0.8
3,"A bit disappointing. I expected more.",-0.4
4,"Poor quality and quick wear.",-0.9
5,"Complete satisfaction!",0.9
6,"No comment",0.0
7,"Fast delivery and good product.",0.6
8,"Average product. Nothing special.",0.1
9,"Very bad experience. Returning the goods.",-0.8
10,"Great value for money!",0.7
</data>
```

> -1: very negative sentiment, +1: very positive sentiment, 0: neutral sentiment

---

## Multimodal Prompting

Traditional LLMs work primarily with text. **Multimodal Prompting expands capabilities by allowing the combination of different input types—text, images, audio, video, etc.—in a single prompt.** This opens new ways to interact and solve complex tasks.

**How does it work?**

1. **Combine modalities:** The prompt includes a combination of different data types:
   - **Text description:** Provides context and instructions.
   - **Image:** Can be used for visual recognition, description, or content generation based on the image.
   - **Audio/Video:** Can be used for transcription, emotion analysis, or generating captions.
2. **Multimodal model:** An LLM trained on multimodal data is used. These models can process and integrate different input types.
3. **Generate output:** The model generates output that considers all provided modalities. The output can be text, image, audio, or a combination.

### Practical Example

![image.png](Advanced%20prompty%2020d031acb1608096881fd67996a5fd95/image.png)

```bash
[photo of a sunset]

<task>
Describe this image in detail and then write a short story set in this place.
</task>
```

---

## Automated Prompt Optimization

Creating effective prompts can be time-consuming and requires experimentation. **Automated Prompt Optimization (APO) is a process that automatically searches for the best prompt formulation for a given task to maximize LLM performance.** Instead of manual prompt tuning, APO uses algorithms to systematically test and optimize different prompt variants.

**How does it work?**

1. **Define the goal:** Set the objective—what you want the model to do (e.g., generate accurate answers, create creative texts).
2. **Optimization space:** Define the space of possible prompt changes. This can include:
   - Changing word order
   - Adding/removing keywords
   - Experimenting with different instructions and formatting
3. **Optimization algorithm:** Use an algorithm (e.g., Bayesian Optimization, Reinforcement Learning) to automatically generate and test different prompt variants.
4. **Performance evaluation:** Each prompt variant is tested on a validation dataset and its performance is evaluated using a defined metric (e.g., accuracy, F1 score, BLEU score).
5. **Iteration:** The algorithm iteratively generates new prompt variants to improve performance based on previous results. This process continues until satisfactory performance is achieved or a set number of iterations is reached.

---

## Self-Refinement (Reflexion)

Self-Refinement is an advanced prompting technique where **the LLM not only generates output, but also critically evaluates its own output and then tries to improve it.** It's an iterative feedback and correction process that enables LLMs to achieve higher quality and accuracy.

**How does it work?**

1. **Generate initial output:** The LLM generates a response to the prompt (e.g., answers a question, writes an article).
2. **Critique/Reflection:** The LLM is instructed to critically evaluate its own output. This may include:
   - Identifying errors and inaccuracies
   - Assessing relevance and completeness
   - Judging style and clarity
3. **Generate feedback:** The LLM generates textual feedback describing weaknesses of the initial output and suggests improvements. For example: "The answer is inaccurate because it doesn't consider factor X. It should be expanded with information about Y."
4. **Correction/Refinement:** The LLM uses the feedback to correct and improve its initial output. This may include:
   - Adding new information
   - Correcting errors
   - Changing wording
5. **Iteration:** Steps 2-4 can be repeated several times until satisfactory performance is achieved or a set number of iterations is reached.

---

## Agent-Based Tool Use

Agent-Based Tool Use (ABTU) is a paradigm where **the LLM acts as an intelligent agent capable of using external tools and APIs to solve complex tasks it couldn't solve alone.** Instead of just generating text, the LLM becomes an orchestrator, planning steps, calling tools, and integrating results.

**How does it work?**

1. **Define the task:** The agent receives a complex task (e.g., "Plan a trip from Prague to London considering price and duration.").
2. **Planning:** The LLM analyzes the task and breaks it down into smaller, manageable subtasks (e.g., "Get flight prices", "Get transport info in Prague", "Get transport info in London").
3. **Select tools:** The LLM selects appropriate tools and APIs for each subtask (e.g., Google Flights API, Mapy.cz API).
4. **Call tools:** The agent calls the relevant tools with the required parameters.
5. **Integrate results:** The agent receives results from the tools and integrates them into its plan.
6. **Iteration:** Steps 3-5 are repeated until the task is completed.
7. **Output:** The agent generates the final output (e.g., "The trip includes a flight from Prague to London departing Monday morning and returning Friday evening for a total price of 5000 CZK.").

---

## Fine-Tuning GPT-4o

Fine-tuning is a machine learning technique that allows you to **create a specialized version of an existing large language model (LLM), such as GPT-4o, by training it on a smaller, specific dataset.** Unlike training an LLM from scratch, fine-tuning leverages the model's existing knowledge and capabilities and finely adjusts its parameters to better match a specific task or domain.

**Why Fine-Tune GPT-4o?**

- **Improve performance in specific areas:** GPT-4o is a general model with a wide range of knowledge. Fine-tuning can optimize it for a specific industry (e.g., medicine, finance, law) or tasks (e.g., code generation, writing marketing texts).
- **Increase accuracy and relevance:** Fine-tuning enables the model to better understand the specific terminology and context of a given domain, leading to more accurate and relevant outputs.
- **Control over style and tone:** Fine-tuning allows adjusting the style of the generated text to meet specific requirements (e.g., formal vs. informal, technical vs. layman).
- **Reduce costs and time:** Fine-tuning is much less resource-intensive than training an LLM from scratch.

---

## RAG (Retrieval-Augmented Generation)

RAG is a technique that **combines the power of large language models (LLMs) with external knowledge bases.** Instead of relying solely on the LLM's internal knowledge, RAG allows the model to search for relevant information from an external source and then use it to generate more informative and accurate text.

![image.png](Advanced%20prompty%2020d031acb1608096881fd67996a5fd95/faa87fd1-3ad9-4e64-9140-662e6124620b.png)

**Why Use RAG?**

- **Overcome LLM limitations:** LLMs have limited, sometimes outdated or incomplete knowledge. RAG enables the model to access up-to-date information from external sources and overcome these limitations.
- **Increase accuracy and factual correctness:** RAG reduces the risk of "hallucinations" (generating false information) by giving the model access to verifiable data.
- **Explainability:** RAG allows you to trace the source of information used to generate text, increasing transparency and trust in the model.
- **Flexibility and scalability:** RAG can be easily extended with new data sources without retraining the entire LLM.

---

## CAG (Cache-Augmented Generation)

**Cache-Augmented Generation (CAG)** is a technique designed to address the performance slowdown often associated with Retrieval-Augmented Generation (RAG). While RAG fetches external knowledge bases every time a user asks a question, CAG offers a faster alternative. Instead of performing real-time retrieval, **CAG preloads relevant documents into the model's context and stores this inference state—also known as a Key-Value (KV) cache.**

![image.png](Advanced%20prompty%2020d031acb1608096881fd67996a5fd95/75914564-7cf9-4a29-a04e-4e8fa97b9c4f.png)

**Why Use Cache-Augmented Generation?**

- **Reduce latency:** The main advantage of CAG is significantly reduced latency. By eliminating the need for real-time retrieval, the model can instantly access preloaded information, resulting in faster responses.
- **Increased efficiency:** CAG enables more efficient use of LLM resources by avoiding repeated retrieval operations.
- **Faster answers to multiple questions:** CAG is excellent for quickly answering multiple user queries about preloaded knowledge, as there's no need to reload information for each question.
- **Simplified setup (in some implementations):** As described in the tutorial, CAG can be implemented so that all knowledge is pre-embedded and the cache is reset without reloading the entire context each time.

**Key Differences from RAG:**

- CAG focuses on storing the _inference state_ instead of dynamically retrieving external documents.
- CAG prioritizes speed by preloading information, while RAG emphasizes access to up-to-date knowledge through retrieval.
