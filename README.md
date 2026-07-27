# Team

This project was developed by a **3-person team** for the **University of Auckland × BNZ Hackathon**.

The team collaborated across different areas including:

- Machine Learning customer segmentation.
- Backend API development and AI integration.
- Frontend application development and user experience design.

Each team member contributed to different parts of the end-to-end system, combining machine learning, generative AI, and software engineering to build the Synthetic Customer Lab prototype.
Synthetic Customer Lab

Synthetic Customer Lab is a hackathon MVP developed for the University of Auckland × BNZ Hackathon.

It is an AI-assisted pre-launch testing platform that allows banking teams to evaluate marketing messages, customer communications, and UI experiences before releasing them to real customers.

Instead of sending one generic message to all customers, this system simulates how different customer groups may interpret, trust, and react to a banking campaign.

The platform combines:

* Customer segmentation using machine learning.
* Dynamic synthetic customer persona generation.
* AI-powered customer reaction simulation.
* Marketing message analysis.
* Risk detection and improvement recommendations.
* Optional UI screenshot analysis.

It acts as an early-stage assurance layer for banking campaigns, helping teams identify potential confusion, trust issues, accessibility concerns, and customer risks before launch.

This MVP is designed to support customer research and decision-making, not replace real customer testing, compliance review, or accessibility validation.

⸻

System Architecture

Synthetic Customer Lab consists of two connected services:

1. Synthetic Customer Lab (Main Application)

Repository:

https://github.com/Maishi226/bnz-hkt

Responsible for:

* Frontend user interface.
* Backend API.
* OpenAI integration.
* Synthetic customer generation.
* Customer simulation.
* Campaign analysis.
* Risk scoring.
* Recommendation generation.

⸻

2. Bank Customer Segmentation Service

Repository:

https://github.com/Maishi226/bank-segmentation-service

Responsible for:

* Customer behaviour analysis.
* Machine learning based segmentation.
* K-Means clustering.
* Segment assignment.
* Customer profile generation.

The two repositories work together.

The segmentation service must be running before using the Synthetic Customer Lab because the simulation pipeline depends on customer segment information.

Architecture:

                 Marketing Team
                       |
                       |
                Synthetic Customer Lab
                       |
        --------------------------------
        |                              |
        |                              |
   OpenAI GPT-5.5              Segmentation Service
                                      |
                                      |
                               K-Means ML Model
                                      |
                                      |
                            Customer Segments

⸻

Key Features

1. AI Marketing Message Analysis

The system analyses banking advertisements and communication messages.

It evaluates:

* Message clarity.
* Customer trust.
* Potential stress or anxiety.
* Fairness concerns.
* Financial wellbeing impact.
* Operational risks.
* Communication effectiveness.

Example:

Input:

Get your first home loan with BNZ.
Competitive rates and expert support available.

Output:

Strengths:
- Clear financial goal.
- Relevant customer benefit.
Potential risks:
- May not explain eligibility requirements.
- Could create unrealistic expectations.
Recommendations:
- Add transparent qualification information.
- Provide clearer next steps.

⸻

2. Machine Learning Customer Segmentation

The platform integrates with the Bank Customer Segmentation Service.

Customer behaviour data is processed using:

* Feature engineering.
* Standardisation.
* K-Means clustering.
* Segment assignment.

The model identifies different customer groups based on behavioural patterns.

Examples:

Affluent Investors
High value customers with:
- Higher savings.
- Investment activity.
- Lower financial stress.
Digital Everyday Customers
Customers with:
- Frequent app usage.
- Regular transactions.
- Preference for digital banking.

These segments are used as the foundation for synthetic customer generation.

⸻

3. Dynamic Synthetic Persona Generation

The system generates customer personas based on:

* Campaign objective.
* Target audience.
* Banking message.
* Customer segments.
* Communication channel.
* Timing.

Each persona contains:

* Demographic context.
* Financial behaviour.
* Banking relationship.
* Needs and motivations.
* Concerns.
* Expected reaction.

Example:

Persona:
Young First Home Buyer
Characteristics:
- Early career professional.
- Saving for a deposit.
- Interested in mortgage products.
Reaction:
Positive about support but concerned about affordability.

⸻

4. Synthetic Customer Simulation

Generated personas are simulated as customers interacting with the banking message.

The system evaluates:

* Trust level.
* Understanding.
* Emotional response.
* Financial wellbeing impact.
* Accessibility concerns.
* Likelihood of taking action.

The simulation produces:

* Customer reactions.
* Segment-level insights.
* Risk indicators.
* Improvement recommendations.

Example:

Customer Segment:
First Home Buyers
Reaction:
7.8 / 10 trust score
Concerns:
- Unsure about eligibility.
- Needs clearer repayment information.
Suggested improvement:
Add mortgage calculator link and eligibility explanation.

⸻

5. AI Advertisement Optimisation

After analysing customer reactions, the platform generates recommendations to improve campaign effectiveness.

It can suggest:

* Better wording.
* More personalised messaging.
* Different customer benefits.
* Reduced ambiguity.
* Improved call-to-action.

Example:

Original:

Get a better mortgage today.

Improved:

Explore your first home options with BNZ.
Understand your borrowing ability and receive personalised guidance.

⸻

6. UI Screenshot Analysis

The system supports optional screenshot uploads.

When OpenAI vision capability is enabled, it analyses:

* Text hierarchy.
* Button clarity.
* Information layout.
* Accessibility concerns.
* Customer action clarity.

Example checks:

Potential issue:
The primary action button is unclear.
Recommendation:
Use stronger CTA wording:
"Check my eligibility"

⸻

7. Risk Scoring Framework

The platform provides early risk indicators:

Customer Risk

* Confusing language.
* Low trust.
* Financial stress.
* Unexpected customer reactions.

Accessibility Risk

* Poor readability.
* Unclear actions.
* Complex explanations.

Operational Risk

* Potential customer complaints.
* Misunderstanding of product conditions.
* Increased support workload.

⸻

Project Structure

bnz-hkt/
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── api/
│   │   └── types/
│
├── backend/
│   ├── app/
│   │   ├── main.py
│   │   ├── models.py
│   │   ├── personas.py
│   │   ├── openai_client.py
│   │   └── scoring.py
│
└── README.md

⸻

Running the Application

You need to run three services.

1. Start Customer Segmentation Service

Repository:

https://github.com/Maishi226/bank-segmentation-service

cd ~/Desktop/bank-segmentation-service
source .venv/bin/activate
uvicorn app.main:app --reload --port 8000

Service:

http://127.0.0.1:8000

⸻

2. Start Backend

cd ~/Desktop/bnz-hkt/backend
source .venv/bin/activate
uvicorn app.main:app --reload --port 8001

Backend:

http://127.0.0.1:8001

⸻

3. Start Frontend

cd ~/Desktop/bnz-hkt/frontend
npm install
npm run dev

Frontend:

http://localhost:5173

⸻

Environment Configuration

Backend .env:

OPENAI_API_KEY=your_openai_api_key
OPENAI_MODEL=gpt-5.5
SEGMENTATION_SERVICE_URL=http://127.0.0.1:8000

The OpenAI key is only stored and used in the backend.

The frontend never accesses the OpenAI API key.

⸻

API Endpoints

Generate Personas

POST /api/generate-personas

Input:

{
  "featureName": "First Home Buyer Campaign",
  "bankingMessage": "Buy your first home with BNZ",
  "targetCustomers": "Young professionals",
  "channel": "Email",
  "sendTiming": "Monday morning",
  "personaCount": 5
}

Returns:

* Synthetic customer personas.
* Customer characteristics.
* Segment information.

⸻

Analyse Advertisement

POST /api/analyze-ad

Returns:

* Marketing analysis.
* Risk signals.
* Recommendations.

⸻

Run Simulation

POST /api/run-simulation-jobs

Runs:

Customer segments
        |
Synthetic personas
        |
AI simulation
        |
Customer reactions
        |
Optimisation suggestions

Returns:

* Overall campaign score.
* Persona reactions.
* Risk factors.
* Improved message suggestions.

⸻

Example Demo Scenario

Feature:

Smart overdraft warning

Message:

Your account may go into overdraft before Friday.
Consider transferring $120 from savings.

Target customers:

Customers with low balance and upcoming bills.

Channel:

Mobile notification

Timing:

2 days before expected overdraft

The system evaluates how different customer groups may react before launch.

⸻

Technology Stack

Frontend

* React
* TypeScript
* Vite
* Tailwind CSS

Backend

* FastAPI
* Python
* REST API

Machine Learning

* Scikit-learn
* K-Means clustering

AI

* OpenAI GPT-5.5 API

Authentication

* Supabase Authentication

⸻

Limitations

Synthetic personas are simulated customers and do not represent real individuals.

For example, the system may generate personas such as:

* First home buyers.
* High value customers.
* Digital banking users.

However, real banks may not directly know all personal characteristics of customers.

Therefore, this platform should be used as:

* A campaign risk screening tool.
* A communication improvement assistant.
* A pre-launch testing layer.

High-impact banking decisions should still include:

* Real customer research.
* Accessibility testing.
* Compliance review.
* Operational review.

⸻

Future Improvements

Potential extensions:

* Connect with real anonymised banking behaviour data.
* Add reinforcement learning for campaign optimisation.
* Support A/B testing of multiple marketing messages.
* Integrate real customer feedback loops.
* Add compliance policy checking.
* Deploy on AWS for production-scale usage.