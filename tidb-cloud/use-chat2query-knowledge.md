---
title: Get Started with Knowledge API
summary: Learn how to use TiDB Cloud Knowledge API to optimize the SQL generation performance of the chat2query.
---

# Get Started with Knowledge API

TiDB Cloud provides the Knowledge API to support users in adding or modifying domain-specific knowledge to improve the SQL generation capabilities of Chat2Query. Its usage aligns with the [Chat2Query API](/tidb-cloud/use-chat2query-api.md). 


> **Note:**
>
> Knowledge API is available for [TiDB Serverless](/tidb-cloud/select-cluster-tier.md#tidb-serverless) clusters. To use the Knowledge API on [TiDB Dedicated](/tidb-cloud/select-cluster-tier.md#tidb-dedicated) clusters, contact [TiDB Cloud support](/tidb-cloud/tidb-cloud-support.md).


## Introduction to Knowledge Utilized in Chat2Query
Currently, Chat2Query supports the use of the following three types of Knowledge. Each type is specifically designed for different scenarios and has a unique knowledge structure.

### Few-Shot Example
Few-shot examples refer to the Q&A learning samples provided to Chat2Query, which include sample questions and their corresponding answers. By learning from these few samples, Chat2Query can improve its ability to handle new tasks more effectively.

> **Note:**
>
> It's important to remember that the quality of the examples affects how well Chat2Query learns. If the examples are bad, like if the answers don't match the questions, it could make Chat2Query perform worse, not better, on new tasks.

#### The Knowledge Sturcture
Each example consists of a sample question along with its corresponding answer. Here is an example:

```json
{
    "question": "每月的收入趋势分布", 
    "answer": "SELECT DATE_FORMAT(`billing2_invoices`.`invoice_date`, '%Y-%m') AS `Month`, SUM(`billing2_invoices`.`cost_price`) AS `total_revenue` FROM `billing2_invoices` GROUP BY `Month` ORDER BY `Month`"
}
```


#### When To Use
Few-shot examples can significantly improve the performance of Chat2Query in various scenarios, including but not limited to, the following two circumstances:

1. **When dealing with rare or complex question**: If Chat2Query encounters questions that are infrequent or complex, leading to inadequate responses, Adding few-shot examples can assist in enhancing its understanding.

2. **When struggling with a certain type of question**: If Chat2Query frequently errs or has difficulty with specific questions, Adding few-shot examples can help improve its performance on these questions.



### Term-Sheet Explanation
Term-Sheet Explanation refers to the detailed explanation of a specific term or a group of similar terms. It includes a list of terms along with their corresponding comprehensive descriptions.

> **Note:**
>
> Similarly, it is essential to ensure the accuracy of each newly added term explanation. Incorrect interpretations could not only fail to improve the generation results of Chat2Query but also potentially lead to adverse effects.

#### The Knowledge Sturcture
Each explanation includes a list of terms along with their corresponding comprehensive descriptions. Here is an example:
```json

```


#### When To Use