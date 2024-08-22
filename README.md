# Sharepoint Opportunity Management (CRM Solution)

## Overview
This document provides a detailed guide on the Opportunity Management CRM Solution built using SharePoint and Power Automate. The solution is designed to manage opportunities efficiently through a series of automated workflows. The process is divided into multiple stages, each involving different teams and flows that work together to manage the entire lifecycle of an opportunity, from initial client contact to opportunity closure.

## Stage 1: Inbound Process

### Objective
The first stage focuses on capturing essential client information in the "Contact Management" list. This information serves as the foundation for evaluating potential opportunities.

### Process Overview
- **List Involved**: "Contact Management"
- **Team Responsible**: Sales Team / Front-line Team

### Step-by-Step Process

1. **Fill in Client Information**: 
   - Navigate to the "Contact Management" list in SharePoint.
   - Enter the necessary details as outlined below:

   | Field Name         | Data Type           | Description                                    |
   |--------------------|---------------------|------------------------------------------------|
   | **Contact Person** | Single line of text | Enter the full name of the contact.            |
   | **Client Name**    | Managed Metadata    | Enter or choose the client's name.             |
   | **Client Number**  | Number              | Enter the client's phone number.               |
   | **Client Email**   | Single line of text | Enter the client's primary email address.      |
   | **Address**        | Single line of text | Provide the complete address of the client.    |
   | **Required Service** | Choice            | Choose the service the client is interested in.|
   | **Industrial**     | Choice              | Select the industrial sector of the client.    |

2. **Save the Record**: After filling in all required fields, save the record in the "Contact Management" list.

3. **Alert Auto Triggered**: 
   - An alert is triggered upon saving the record to notify the Opportunity Department that a new potential client has been registered.

## Stage 2: Opportunity Evaluation

### Objective
In this stage, the Opportunity Department evaluates the client based on the information provided and completes the necessary evaluation fields.

### Process Overview
- **List Involved**: "Contact Management"
- **Team Responsible**: Opportunity Department

### Step-by-Step Process

1. **Evaluate the Customer**: 
   - Review the client information recorded in the "Contact Management" list.

2. **Complete Evaluation Fields**:
   - Enter the required information in the following fields:

   | Field Name             | Data Type | Description                                        |
   |------------------------|-----------|----------------------------------------------------|
   | **Customer Type**       | Choice    | Select the type of customer (e.g., New, Existing). |
   | **Customer Segmentation** | Choice | Choose the appropriate customer segment (e.g., High Value, Standard). |

3. **Save the Record**: Ensure all fields are accurately filled out, then save the record.

4. **Flow Triggered**: 
   - After all fields are filled, a Power Automate flow is triggered when the "Lead Generation" button is clicked. This flow creates an opportunity in the "Opportunity Management" list.

## Stage 3: Opportunity Creation and Assignment

### Objective
This stage focuses on creating an opportunity in the "Opportunity Management" list based on the evaluated client data and assigning it to the appropriate team or individual for further action.

### Process Overview
- **Lists Involved**: "Opportunity Management", "Contact Management"
- **Team Responsible**: Opportunity Department

### Step-by-Step Process

1. **Trigger Lead Generation Flow**:
   - The Opportunity Department clicks the "Lead Generation" button in the "Contact Management" list.
   - The flow generates a new record in the "Opportunity Management" list, copying relevant details.

2. **Assign Opportunity**:
   - The flow automatically assigns the opportunity to a team or individual based on predefined criteria (e.g., service required, customer segmentation).
   - An email notification is sent to the "Account Manager".

3. **Update Status**:
   - The opportunity status is automatically updated to "Prospect" in the "Opportunity Management" list.

## Stage 4: Opportunity Tracking and Follow-Up

### Objective
Track the progress of the opportunity and ensure timely follow-up actions are taken to convert the opportunity into a business win.

### Process Overview
- **Lists Involved**: "Opportunity Management"
- **Library Involved**: "RFP Requests"
- **Team Responsible**: Opportunity Department, Account Manager

### Step-by-Step Process

1. **Opportunity Tracking**:
   - Team members update the status of the opportunity in the "Opportunity Management" list as they progress through different stages (Prospect, Qualified, Negotiation, On Hold, Closed Won, Closed Lost).

## Stage 5: Proposals System

### Objective
Generate Technical and Financial Proposals.

### Process Overview
- **Lists Involved**: "Opportunity Management"
- **Libraries Involved**: "RFP Requests", "Stamped Proposals"
- **Team Responsible**: Opportunity Department, Account Manager

### Step-by-Step Process

1. **Proposals Templates**:
   - Each department can have up to 30 templates, and there is also one universal template for the company.

2. **Technical Proposal Creation Flow**:
   - A Power Automate flow triggers the creation of proposals in the "RFP Requests" library whenever the opportunity reaches the "Qualified" stage.
   - When the proposal is generated, the stage changes to "Negotiation".

3. **Financial Proposal Creation Flow**:
   - A Power Automate flow triggers the creation of financial proposals in the "RFP Requests" library whenever the Technical Proposal status reaches the "Finalized" stage.
   - When the proposal is generated, it uses the same reference number as the Technical Proposal.

4. **Stamped Proposals**:
   - A Power Automate flow triggers the creation of both Technical and Financial Proposals as PDF files, also stamped (probably using Adobe Docusign), and generated in the "Stamped Proposals" library.
   - A Power Automate flow sends an email to the client's email address with both proposal PDFs attached.

## Stage 6: Opportunity Closure

### Objective
Successfully close the opportunity, marking it as won, lost, or on-hold, and perform post-closure actions such as reporting.

### Process Overview
- **Lists Involved**: "Opportunity Management"
- **Team Responsible**: Opportunity Department, Account Manager

### Step-by-Step Process

1. **Close the Opportunity**:
   - Update the opportunity status to "Closed Won", "Closed Lost", or "On-Hold" in the "Opportunity Management" list.

## Maintenance and Updates
- Regularly review the Power Automate flows to ensure they align with business processes and update them as necessary.
- Update this documentation to reflect any changes in the flows or business requirements.
