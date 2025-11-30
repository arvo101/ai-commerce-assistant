# AI Commerce Assistant  
Autonomous agent system for a REAL fashion & homewear e-shop, built to operate 24/7 with live product data, semantic search, decision-making logic, and multi-KB reasoning.

This project demonstrates an end-to-end intelligent system:  
- continuous product ingestion (8,000+ SKUs)  
- autonomous decision-making  
- product search & recommendation logic  
- multi-KB domain knowledge  
- error handling & monitoring  
- automated workflows through n8n  

It is designed as a real-world agent that thinks, decides, executes tasks and eventually saves time and money.

---

## System Architecture
![Architecture](./docs/architecture_diagram.png)

The assistant is built as a real-world autonomous system combining:

- **Botpress (reasoning layer)**  
  Intent routing, attribute extraction, product search logic, multi-KB reasoning.

- **n8n (automation & orchestration layer)**  
  Hourly product ingestion (8,000+ SKUs), XML → JSON pipeline, retries, Discord alerts, and Botpress table updates.

- **Botpress Database (data layer)**  
  Live product dataset available directly to the agent for search and recommendations.

  ---

## 🚀 Core Capabilities

### **1. Autonomous Product Data Pipeline (8,000+ SKUs)**
![n8n Pipeline](./docs/n8n_workflow.png)

End-to-end system that keeps the agent’s dataset always up to date without human intervention:
- Hourly XML → JSON → Normalization pipeline  
- Automated field cleaning (category, size, color, gender, price)
- Flattens product variations (color, size) so each variation becomes a standalone product entry  
- Ensures every size/color variation appears as a separate searchable item in the agent  
- Removes old records via DELETE API calls
- Uploads new products in safe 500-item batches via POST API calls, to prevent overload
- Response validation, retry logic, and failure recovery  
- Real-time Discord alerts for any error state  
- Ensures the agent always operates on accurate, live product data  

---

### **2. Multi-Step Reasoning & Decision Flow (n8n + Botpress)**
The system coordinates reasoning (Botpress) with execution (n8n):
- Botpress extracts intent & structured attributes  
- n8n handles execution, transformations, and persistence  
- Autonomous loops ensure tasks complete even after failures  
- Agent routes tasks between KB lookup → attribute extraction → product search → execution workflows  

---

### **3. Intelligent Product Search Engine (Tool + AI Hybrid)**
A hybrid reasoning system combining AI understanding with rule-based filtering:
- AI decomposes user input (category, gender, price, size, color)  
- Custom filtering engine selects relevant SKUs from thousands  
- Semantic reasoning over product descriptions  
- Returns minimal, relevant results (carousel)  
- Handles complex multi-condition queries seamlessly  

---

### **4. Multi-Knowledge-Base Agent Brain**
The agent dynamically selects the correct knowledge source:
- **Default KB** → policies, delivery, returns, etc.
- **Gifts KB** → recommendations based on gender & budget   
- **Advice KB** → domain knowledge (e.g., basic advice on how to buy lingerie and homewear, common questions)  
- Autonomous intent routing ensures minimal back-and-forth  

---

### **5. Orchestration, Monitoring & Recovery**
This system behaves like an autonomous worker:
- Detects frustration and escalates to human support  
- Maintains its own data consistency  
- Recovers from failures without human help 
- Designed to run indefinitely with minimal maintenance


---

## Botpress Agent Layer
Botpress is the conversational and interpretation layer of the system.  
It transforms free-text user messages into structured actions, selects the correct workflow, and collaborates with n8n to complete tasks end-to-end.

### **1. Intent Detection**
The agent identifies what the user wants with high accuracy:
- product search  
- store information & policies   
- gift suggestions  
- domain questions (e.g. lingerie fit, seamless materials)  
- frustration → escalation to human support  

This allows the system to route the user to the correct workflow immediately.

---

### **2. AI Attribute Extraction**
With custom AI tasks, Botpress converts natural language into structured attributes:
- category (π.χ. πιτζάμα, σουτιέν)  
- gender  
- size  
- color  
- price range  
- product codes  
- additional style keywords  

These structured fields feed directly into the product search engine.

---

### **3. Product Search Flow**
![Botpress Search](./docs/productsearch_workflow.png)
Botpress orchestrates the full search logic:
- cleans & normalizes extracted attributes  
- triggers the custom product search tool  
- filters results from 8,000+ live product entries  
- returns highly relevant SKUs in carousel format  
- handles fallback behavior when attributes are missing  

This allows the user to ask complex queries naturally (e.g. *“black men's pajama medium under 20€”*).

---

### 📦 Live Product Dataset (Botpress Table)
![Product Table](./docs/botpress_table.png)

### **4. Multi-Knowledge-Base Routing**
The agent dynamically selects the proper knowledge source:
- **Default KB** → store info, policies, deliveries, returns  
- **Gifts KB** → gender + budget-based recommendations  
- **Advice KB** → sizing guidance & domain tips  

Each category of question is handled with domain-specific accuracy.

---

### **5. Conversational Management**
Botpress manages the flow of the conversation:
- asks clarifying questions (π.χ. size / color)  
- handles follow-up queries without losing context  
- guides the user through product discovery  
- triggers escalation when user frustration is detected  

This gives the assistant a human-like interaction flow.

---

### **Included in this repository**
Only the non-sensitive components of the agent are included:
- **Product search flow export** → `/botpress_flows/`  
- **Screenshots & diagrams** → `/docs/`  

The full private bot and client-specific flows are intentionally excluded.
