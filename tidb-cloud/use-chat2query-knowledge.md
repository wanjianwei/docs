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
Currently, Chat2Query supports the use of three types of Knowledge: `Few-Shot Example`, `Term-Sheet Explanation` and `Instruction`. Each type is specifically designed for different scenarios and has a unique knowledge structure.

### Few-Shot Example
`Few-Shot Example` refer to the Q&A learning samples provided to Chat2Query, which include sample questions and their corresponding answers. By learning from these few samples, Chat2Query can improve its ability to handle new tasks more effectively.

> **Note:**
>
> It's important to remember that the quality of the examples affects how well Chat2Query learns. If the examples are bad, like if the answers don't match the questions, it could make Chat2Query perform worse, not better, on new tasks.

#### The Knowledge Sturcture
Each example consists of a sample question along with its corresponding answer. Here is an example:

```json
{
    "question": "How many records in the 'test' table", 
    "answer": "SELECT COUNT(*) FROM `test`;"
}
```


#### When To Use
Few-Shot examples can significantly improve the performance of Chat2Query in various scenarios, including but not limited to, the following two circumstances:

1. **When dealing with rare or complex question**: If Chat2Query encounters questions that are infrequent or complex, leading to inadequate responses, Adding few-shot examples can assist in enhancing its understanding.

2. **When struggling with a certain type of question**: If Chat2Query frequently errs or has difficulty with specific questions, Adding few-shot examples can help improve its performance on these questions.



### Term-Sheet Explanation
`Term-Sheet Explanation` refers to the detailed explanation of a specific term or a group of similar terms. It includes a list of terms along with their corresponding comprehensive descriptions.

> **Note:**
>
> Similarly, it is essential to ensure the accuracy of each newly added term explanation. Incorrect interpretations could not only fail to improve the generation results of Chat2Query but also potentially lead to adverse effects.

#### The Knowledge Sturcture
Each explanation comprises either a single term or a list of similar terms, accompanied by their detailed descriptions. Here is an example:
```json
{
    "term": ["AR"],
    "description": "refers to the outstanding invoices a company has or the money clients owe the company"
}
```


#### When To Use
The primary function of the `Term-Sheet Explanation` is to improve Chat2Query's comprehension of user queries. It is typically utilized in the following situations:

1. When handling industry-specific terminology or acronyms that may not be universally recognized.
2. When ambiguities in the user's query can be clarified using a Term-Sheet Explanation.
3. When users employ terms that carry different meanings in various contexts, a Term-Sheet Explanation can assist Chat2Query in discerning the correct interpretation.


### Instruction
`Instruction` is a piece of textual command. It is used to guide or control the behavior of Chat2Query, specifically instructing it on how to generate SQL according to specific requirements or conditions.

> **Note:**
>
> The `Instruction` has a length requirement and it should not exceed 512 characters.

#### The Knowledge Sturcture
As mentioned above, `Instruction` is a piece of textual command. Here is an example:
```json
{
    "instruction": "If the task requires calculating the sequential growth rate: Using LAG function with OVER clause in SQL"
}
```

#### When To Use
There are many scenarios where `Instruction` can be used. What you need to remember is that the purpose of using `Instruction` is to guide Chat2Query to output according to your requirements. What you need to do is to provide as clear and specific `Instruction` as possible. Here are two use case scenarios:

1. When you want to limit the scope of the query: If you only want the SQL to consider certain tables or fields, you can use an `Instruction` to specify this.

2. When you want to guide the structure of the SQL: If you have specific requirements for how the SQL should be structured, you can use an `Instruction` to guide Chat2Query.


## How To Use Knowledge API
