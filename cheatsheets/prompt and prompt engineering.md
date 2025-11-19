# 📝 Prompt Engineering Cheatsheet

Most commonly, **prompt techniques** are useful during **real-time interaction** with AI models, while **prompt engineering** focuses on writing successful prompts for **scalable solutions**.  

For successful results, a **structured, strategic approach** is required, often combined with **creativity**. Effective prompts may involve a combination of multiple techniques.

---

## What is a Prompt?  
A **prompt** is a **powerful, comprehensive request for an AI model to generate a response**.

| Technique                     | Purpose                                                   |
|-------------------------------|-----------------------------------------------------------|
| **Contextual Prompt**          | Provide background, scenario, or examples to guide AI output |
| Zero-shot Prompting            | Only instructions, no examples                             |
| One-shot Prompting             | Provide a single example                                   |
| Few-shot Prompting             | Provide multiple examples                                  |
| **Conditional Prompt**         | Use rules or logic to determine AI output                 |
| **Instructional / Direct**     | Give explicit instructions                                 |
| **Chain-of-Thought**           | Encourage step-by-step reasoning                           |
| **Role-based / Persona**       | Assign a role or persona to tailor style or tone          |
| **Instruction + Context**      | Combine instructions with background/context for structured output |

---

## 1️⃣ What is Prompt Engineering?  
**Prompt Engineering** is the art of **crafting inputs (prompts) for AI/LLMs** to get **accurate, useful, and controlled outputs**.
---

## 2️⃣ ICO Framework  
A framework to design **structured prompts** effectively:

1. **Instruction** – Clear instructions for the AI:  
   - **Role:** Assign a persona or role (e.g., “You are a career coach”)  
   - **Rule:** Guidelines or instructions to follow  
   - **Condition:** Conditional logic or branching (if-then statements)  
   - **Boundaries:** Limits like word count, style, tone  

2. **Context** – Additional information to guide the AI:  
   - **Background:** Relevant scenario, user info, or domain data  
   - **Example:** Sample inputs and outputs for clarity  

3. **Output** – Define the expected format or structure of the response

---

## 3️⃣ Core Four AI Prompt Engineering Skills

1. **Delimiter** – Characters used to define boundaries in a prompt  
   - Example: `<tag>content</tag>`  

2. **Definition** – Using a word or phrase to **refer to something** added in your prompt for clarity.

3. **Markdown** – A readable formatting system often used in LLMs  
   - Example: `# Header 1`, `- bullet point`, `**bold text**`  

4. **Handlebars** – Placeholders in prompts that can be dynamically replaced with input or context  
   - Example: `"Summarize the following text: {{text_to_summarize}}"`

---

## ✅ Summary

- **Prompt** – Your request to the AI  
- **Prompt Engineering** – Designing prompts for controlled, high-quality outputs  
- **Techniques** – Contextual and Conditional prompts  
- **Framework** – ICO (Instruction, Context, Output)  
- **Core Skills** – Delimiter, Definition, Markdown, Handlebars
