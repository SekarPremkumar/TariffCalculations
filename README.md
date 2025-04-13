# Tariff Calculator for Shipping Companies

## Technical Explanation

### Document Parsing
Used **llamaParse** for parsing the tariff documentation.

### Embedding Creation
Used **HuggingFace Sentence Transformer** model `all-MiniLM-L6-v2` to generate embeddings.

### Vector DB
Used **FAISS DB** to store and retrieve embedded document sections.

---

## How I Approached Tariff Calculations

### Inputs:
We have two main inputs:
1. **Tariff Documentation**
2. **Vessel Details**

From these inputs, we need to:
- Identify the **correct section of the document** for each tariff type
- Understand how the **tariff is to be calculated**
- Match this with **vessel details** to determine the applicable tariff and perform the calculation

### Key Challenge:
The main challenge is ensuring the model understands the **nuances of the shipping industry**, including:
- Deep understanding of the document
- Strong context and **geographical awareness** (e.g., knowing that "registered port" means a South African port in this context)

### Importance of Retrospection:
Since accurate interpretation is critical, I used a **series of prompt chaining** steps to guide the model logically.

---

## Step-by-Step Prompt Strategy

1. **Understand the Relevant Document Part**
   - Extract and convert it into a **clearly defined instruction manual** of how to approach the problem.

2. **Create Logical Questions**
   - Generate condition-based yes/no questions that must be answered to perform the calculation.

3. **Answer the Questions**
   - Using the **vessel details**, have the model answer each logical question with yes/no to determine which rules apply.

4. **Enrich Vessel Details**
   - Add **contextual awareness** and **geographical understanding** to enhance the raw vessel data.

---

## Final Step: Calculation Using Smol Agents
With the following:
- Detailed instructions
- Context-enriched vessel details
- Logical questions and answers

I used **Smol Agents**, a code-based agent that accurately performs **mathematical calculations** by working directly with code.

---

## Final Output Example:
```json
{
  "light dues": 60062.04, // <Correct>
  "port dues": 309853.1115,
  "towage dues": 7053752.976, // <NoInfoInDocument>
  "vehicle traffic services (VTS) dues": 33345.0, // <Correct>
  "pilotage dues": 51300.0,
  "running of vessel lines dues": 1654.56
}
```

---

## My Thoughts and Observations on the Result and Solution:
- I have tried my best to address the problem and come up with a **solid framework** to approach it.
- The solution **covers most important aspects**.
- It **misses a few edge cases due to time constraints of this assignment**, such as:
  - What if **no information is available** in the document?
  - Other potential **exception scenarios**

### Examples:
1. **Working hours issue:**
   - For `pilotage dues`, there was **no mention of working hours** in the document, so the model made a wrong assumption.

2. **Towage dues:**
   - Info related to this calculation was **not present in the document**, so the output was incorrect.

3. **Other inaccuracies:**
   - Sometimes the LLM gives wrong output even though everything seems fine — usually due to **improper understanding of the instruction**, which I believe can be improved using **prompt tuning**.

---

## Summary
This is how I approached the problem and built a logical, structured framework for calculating tariffs based on real-world documentation.

