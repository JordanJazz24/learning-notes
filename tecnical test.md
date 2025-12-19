# Technical Assessment

**Candidate:** Jordan Alvarez Gonzalez  
**Date:** 19/12/2025

## Part 1 – Code Analysis

### Bug
The method starts iterating over the list of payments without checking whether `payments` is null.  
Additionally, it does not validate whether the fields `payment.amount` or `payment.status` exist or contain valid values.  
This could cause the program to fail at runtime or make the method behave unexpectedly if the data comes in an incorrect format.

---

### Performance
It is necessary to investigate what the `save(payment)` method does exactly, since if its purpose is to persist data in the database and a large number of payments are received (for example, 10,000), saving each payment one by one could generate high latency.  
This type of implementation can slow down the system due to the number of operations performed against the database.

---

### Data Congruence
The definition of the `total` variable suggests that integer numbers are being used, which is not the most appropriate option for handling financial data.  
It would be more suitable to use a decimal data type, as it is more precise and helps avoid possible accounting errors in the system.

Additionally, considering that payment processing is a critical operation that cannot be left halfway, it is important to ensure that the `save(payment)` method is atomic at the database level.  
This helps prevent inconsistent data if a failure occurs during execution.

---

### Security
Since this method handles payments, it is important to validate the input data to ensure it is not being manipulated.  
It is also necessary to control which parts of the system have access to this method, as it should not be publicly accessible or allow improper modifications to payments.

---

### Maintainability
The code has a high level of coupling, since the `"completed"` state is hardcoded.  
If new states are added in the future or the business logic changes, this method would need to be modified directly.  
Abstracting this logic would make the code easier to maintain and extend.

---

## Part 2 – Change of Requirements

### 1. What new problem does this introduce?
This could generate duplicated payments or cause the calculated total to not represent the real state of the payments, directly affecting data consistency and the business.

---

### 2. What concept or strategy would you use to solve it?
To solve this problem, the concept of idempotency could be used.  
This way, even if the same payment reaches the system multiple times, the final result would always be the same and the payment would not be processed more than once.

---

### 3. What additional data or information would be required?
It would be necessary to have a unique identifier for the payment and the date of the last payment attempt, which would allow identifying whether it has already been processed.

---

## Part 3 – Small Implementation

```csharp
int AverageNonNegative(List<int> intList){
    if (intList == null)
        throw new ArgumentNullException(nameof(intList));

    int sum = 0; 
    int count = 0;

    foreach (int num in intList){
        if (num >= 0){
            sum += num;
            count++;
        }
    }

    return count == 0 ? 0 : (int)(sum / count);
}
```

---

### 1. Why did you implement it this way?

I think that the main point to solve the problem is to consider that the list cannot be null and that it can also be empty or contain only negative values.
At first, I tried to use C# LINQ syntax, but I realized that I was performing two iterations to obtain the result. After analyzing this, I decided to use a manual `foreach`, since it is simpler and more readable.

In this way, I use only two variables: one to accumulate the sum of non-negative values and another as a counter. At the end, I perform a simple return, checking whether the counter is zero (empty list or only negative values), in which case I return 0; otherwise, I return the division between the sum and the counter.

---

### 2. What happens if the input list is empty?

If the list is empty or contains only negative values, the counter remains at zero.
In that case, returning the division directly could result in an invalid operation, so this condition is validated before performing the calculation and 0 is returned as the result.

---

### 3. How would you improve it if performance became critical?

For simplicity, I used a list as the data structure, but if the volume of information were very large, the use of lighter structures such as an array could be evaluated.
In any case, the main logic would remain the same, since the method already iterates over the collection only once and avoids unnecessary operations. In my understanding, this solution is efficient enough without resorting to more complex techniques.

---

## Part 4 – Conceptual Understanding

### 1. Backend: What is idempotency and why is it important in backend systems?

Idempotency, in very simple words, is a mechanism that allows the same process to be executed multiple times while ensuring that the final result is always the same, as if it had been executed only once.
This is very important in backend systems, since it prevents a single action from generating duplicated effects when, for example, a common case is when a user clicks a button multiple times and the system receives the same action many times, but it should only be executed once.

---

### 2. Frontend: Explain the difference between client-side and server-side rendering, and give an example of when each is useful.

Client-side rendering (CSR) is used in web applications whose main goal is to be fluid and dynamic, since the browser receives a base page and then small interface elements are updated using JavaScript, without reloading the entire page.

Server-side rendering (SSR) is used when the main content of the page needs to be generated on the server before being sent to the client.
This approach is useful when faster initial loading, better security handling, or greater control over the page content is required.

---

### 3. Databases: What is a foreign key and why is it important for data integrity?

A foreign key is important because it is the foundation of relational databases.
Basically, it represents a relationship or connection between two tables, indicating that the data in one table depends on another.
This is important for data integrity, since it prevents invalid records from existing and ensures that relationships between tables remain consistent.

---

## Part 5 – Technical Judgment

### 1. What was the most difficult part of this assessment and why?

The most difficult part of this assessment, and the one that took me the most time, was the code analysis. This is because it is not only about understanding what the code does, but also about thinking of possible problems in a real future production environment, which is not always clear without having the full business logic context.

---

### 2. What assumption did you make that could be wrong?

I assumed that the input data, such as the list of payments and the values of each payment, arrive in a reliable and expected format.
In a real system, this data could be incomplete or contain incorrect values, which would require additional validations that were not considered in this exercise.

---

### 3. What would most likely fail first in production?

Most likely, the first thing to fail in production would be error handling and data consistency in the presence of partial failures, such as network issues or errors when saving information.

---

## Part 6 – Learning Mindset

### What I am currently learning

I am currently learning more about how microservices and monoliths work, as well as deepening my knowledge of cloud deployment using Kubernetes.
This topic interests me because these technologies are widely used today by many companies, and I consider it important to better prepare myself in order to understand how real systems are designed and deployed.

My goal is to continue learning about these tools to become a more complete programmer.
