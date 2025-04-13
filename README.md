Tariff Calculator for Shipping Companies

Technical Explanation

Document Parsing - Used llamaParse
Embedding Creations - Used Hugging Sentence Transformer (all-MiniLM-L6-v2)
Vector DB - Used Faiss DB 

How I approached Tariff Calculations:
Inputs We have is Tariff Documentation and Vessel Details,
In this we have to find the right part of documentation for each tariff calculation and understandhow to calculate the tariff and with the vessel details , we need logically choose what tariff we need levy on them.

Here the challenge is  Model to undersatnd the nuance of shipping industry, understandingthe docuemnt without mistake and context awareness, geographical awareness.

So if you see here retrospection is very important here,
So I have used series prompt chaining to first it to understand the context, relevant document part and vessel details first.

1. Understand the relevant document part and convert it into clearly defined instructions manual of how ot appraoch teh problem.
2. Create logical questions that can be asked based on the intructions to do the calcuation.
3. Then With teh vessel details and questions, ask the model answer it in Yes/No answer to what conditions it have met.
4. Enriching the vessel details with Context Awareness and geograhical awareness.


Now with all these results like, Detailed instructions, Context enriched Vessel Details, Logical questions and answers.
I use Smol agents, which is a Code Agent, which can do mathematical calculations accurately as it is working with code.


So this is how I approached the problem.

Result I get 


Now my Thoughts and Observations of m solution:

I can see some times it gives wrong results, but it is due to some factors missing in the docuements.
For ex: What is a working hours range in this scenario, it is not mentioned anywhere, so calculations were off in that calculations. 
