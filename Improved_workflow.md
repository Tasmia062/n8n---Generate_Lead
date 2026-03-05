# n8n – Google Maps Lead Generation Workflow (SerpAPI)

Automated lead generation workflow built with **n8n**, **SerpAPI**, and **Google Sheets**.
This workflow searches **Google Maps businesses by ZIP code** and stores structured lead data into Google Sheets.

---

# Overview

This workflow automates the process of finding and collecting business leads based on **ZIP codes and industry search terms**.

It reads ZIP codes with coordinates from **Google Sheets**, searches **Google Maps using SerpAPI**, extracts business data, and saves the results back to a **master Google Sheet**.

The workflow also includes **deduplication logic**, ensuring previously scraped ZIP codes are skipped.

---

# Workflow Architecture

<img width="721" height="152" alt="Lead_Scraper_Workflow(SerpAPI)" src="https://github.com/user-attachments/assets/afc7c499-0050-4299-b9e3-152058f2aeaf" />


---

# Features

* Automated Google Maps scraping using SerpAPI

* Batch processing of multiple ZIP codes

* Deduplication (skips already scraped ZIPs)

* Lead data extraction including:

  * Business Name
  * Address
  * Phone number
  * Website
  * Google Rating
  * Business Category
  * Operating Hours
  * GPS Coordinates
  * Google Maps Link
  * Place ID

* Dynamic input from Google Sheets

* Automatic export to Google Sheets

* Built-in rate limiting to avoid API throttling

* Webhook trigger for automation or API usage

---

# Prerequisites

Before using the workflow you need:

* An **n8n instance** (Cloud or Self-Hosted)
* A **Google account**
* A **SerpAPI account**

Recommended:

* SerpAPI Free Tier (100 searches/month)

---

# Quick Start

## 1. Clone the Repository

```
git clone https://github.com/YOUR_USERNAME/n8n-serpapi-lead-generator.git
cd n8n-serpapi-lead-generator
```

Then import the workflow into n8n.

In n8n:

Workflows → Import from File
Select:

```
serpapi_lead_generator_workflow.json
```

---

# 2. Configure Credentials

## Google Sheets

1. In n8n go to:

```
Settings → Credentials → Create New
```

2. Choose:

```
Google Sheets OAuth2 API
```

3. Complete the OAuth login.

The workflow will then automatically use your credential.

---

## SerpAPI

1. Create an account at:

```
https://serpapi.com
```

2. Copy your API key from the dashboard.

3. Open the **HTTP Request node** called:

```
Find Leads (SerpAPI)
```

Replace:

```
YOUR_SERPAPI_API_KEY
```

with your real key.

---

# 3. Prepare Google Sheets

Create a Google Sheet with two tabs.

## Tab 1 – ZIP Code Input

Example structure:

<img width="309" height="115" alt="zip_input" src="https://github.com/user-attachments/assets/9894048c-bfd8-434f-a41b-8a689758dc55" />


These coordinates allow precise Google Maps searches.

---

## Tab 2 – Output (Lead Results)

Example headers:

<img width="779" height="35" alt="output" src="https://github.com/user-attachments/assets/77d25385-1515-4892-85c7-b23548d9f2c4" />


---

# 4. Configure the Workflow

Update the following nodes.

### Get row(s) in sheet

Set:

```
YOUR_GOOGLE_SHEET_ID
```

Select your **ZIP input tab**.

---

### Read Existing Results

Set the same:

```
YOUR_GOOGLE_SHEET_ID
```

This node checks previously scraped ZIP codes.

---

### Append to Google Sheets

Set:

```
YOUR_GOOGLE_SHEET_ID
```

Select the **output tab** where leads will be stored.

---

### HTTP Request Node

Update the search keyword if needed:

Example:

```
roofing contractor
```

You can replace this with:

* dentist
* restaurant
* gym
* marketing agency
* plumber

---

# Running the Workflow

Trigger the workflow using the **Webhook**.

Example:

```
POST https://YOUR-N8N-DOMAIN/webhook/trigger
```

Or run manually:

```
Execute Workflow
```

The system will:

1. Read ZIP codes
2. Skip already scraped locations
3. Query Google Maps
4. Extract lead data
5. Save results to Google Sheets

---

# Example Use Cases

This workflow can generate leads for many industries:

* Roofing contractors
* Dentists
* Restaurants
* Real estate agents
* Marketing agencies
* Gyms
* Plumbers
* Local service businesses

Simply change the **search query** in the HTTP node.

---

# Tech Stack

* n8n
* SerpAPI
* Google Maps
* Google Sheets
