# GenAI Multi-Agent Retail Assistant on AWS

A production-style Generative AI retail assistant built using **Amazon Bedrock Agents**, **AWS Lambda**, **Amazon Athena**, **Amazon S3**, **AppSync**, and **AWS CDK**.

This project demonstrates a multi-agent orchestration system for mobile phone product discovery, recommendation, personalization, order management, and troubleshooting.

## Architecture Diagram

```mermaid
flowchart TD
    User[User / Customer] --> Frontend[Frontend Application]
    Frontend --> AppSync[AWS AppSync / API Layer]
    AppSync --> Resolver[Streaming API Resolver Lambda]

    Resolver --> Supervisor[Amazon Bedrock Supervisor Agent]

    Supervisor --> ProductAgent[Product Recommendation Agent]
    Supervisor --> PersonalizationAgent[Personalization Agent]
    Supervisor --> OrderAgent[Order Management Agent]
    Supervisor --> TroubleshootAgent[Troubleshooting Agent]

    ProductAgent --> ActionLambda[Action Group Executor Lambda]
    PersonalizationAgent --> ActionLambda
    OrderAgent --> ActionLambda
    TroubleshootAgent --> ActionLambda

    ActionLambda --> Athena[Amazon Athena]
    Athena --> S3[(Amazon S3 CSV Data Lake)]

    TroubleshootAgent --> KB[Bedrock Knowledge Base]
    KB --> Docs[(Product FAQ / Troubleshooting Docs)]

    Resolver --> ChatStore[Conversation History / AppSync Persistence]
    Resolver --> Frontend

Business Problem

Customers often struggle to compare mobile phones because product information, specifications, reviews, pricing, and availability are scattered across different sources.

This GenAI assistant allows users to ask natural language questions such as:

Which is the best Samsung phone under ₹60,000?
Compare iPhone 16 and Samsung Galaxy S24 Ultra.
Recommend a phone for gaming and battery life.
Show my order status.
Help troubleshoot battery drain issues.
Key Features
Multi-agent orchestration using Amazon Bedrock Agents
Supervisor Agent for intent understanding and routing
Specialized agents for recommendation, personalization, orders, and troubleshooting
Athena-based structured product search
S3-backed retail dataset
Streaming response experience
AWS Lambda action group execution
Improved agent instructions to reduce hallucination
Mobile phone retail dataset replacing sample demo data
AWS Services Used
Amazon Bedrock Agents
AWS Lambda
Amazon Athena
Amazon S3
AWS AppSync
Amazon Cognito
AWS CDK
AWS CloudWatch
IAM
Knowledge Bases for Amazon Bedrock
Agents
Supervisor Agent

The Supervisor Agent understands user intent and routes the request to the correct specialized agent.

Product Recommendation Agent

Handles product discovery, product comparison, budget-based recommendations, and feature-based phone suggestions.

Personalization Agent

Provides recommendations based on customer preferences, brand interest, budget, and purchase history.

Order Management Agent

Handles order status, shipping status, return status, and inventory-related queries.

Troubleshooting Agent

Answers product troubleshooting questions using FAQs and knowledge base content.

Dataset Upgrade

The original sample retail dataset was replaced with a realistic mobile phone dataset containing:

Product catalog
Purchase history
Customer preferences
Orders
Inventory
Reviews
Offers
Accessories
Troubleshooting data
Debugging Improvement

During testing, the Recommendation Agent initially returned placeholder responses such as Product Name 1 and Nova 5G Smartphone.

The issue was fixed by improving the agent instructions to:

Always query Athena before recommending products
Avoid placeholder product names
Use actual product records from the dataset
Support partial product matching using LIKE
Ask clarification only when required
Example Prompts
Recommend best Samsung phone under 60000
Compare iPhone 16 and Samsung Galaxy S24 Ultra
Which phones are currently in stock?
Show order status for o003
Recommend a phone for customer cust009
My Contributions
Deployed the multi-agent application on AWS
Replaced the sample dataset with mobile phone retail data
Updated Bedrock Agent instructions
Debugged hallucinated placeholder responses
Validated Athena queries
Tested end-to-end agent responses
Published the customized implementation to GitHub
Project Status

Completed and tested successfully with the mobile phone dataset.
