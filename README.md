# n8n---Generate_Lead
Automated lead generation workflow using n8n, SerpAPI, and Google Sheets. Scrapes Google Maps for hospital data based on location and exports structured results.


## Overview
This n8n workflow automates the process of finding and collecting business leads based on location (ZIP codes) and industry. Originally built to generate hospital leads across Dhaka, but easily adaptable for any industry or location.


## ✨ Features
- **Automated scraping** from Google Maps via SerpAPI
- **Batch processing** of multiple ZIP codes
- **Rich data extraction**:
  - Hospital name & address
  - Phone & website
  - Google ratings
  - Operating hours
  - GPS coordinates
  - Direct Google Maps links
- **Dynamic input** - reads ZIP codes from Google Sheets
- **Export to Google Sheets** with structured data
- **Rate limiting** to avoid API throttling
- **Error handling** for failed requests


## 📋 Prerequisites
- n8n instance (self-hosted or cloud)
- Google account with Sheets API access
- SerpAPI account ([Free tier: 100 searches/month](https://serpapi.com))


## 🚀 Quick Start
### 1. Clone & Import
```bash
# Download the workflow
git clone https://github.com/YOUR_USERNAME/lead-scraper-workflow.git
cd lead-scraper-workflow
```

In n8n:
- Go to **Workflows** → **Import from File**
- Select `lead-scraper-workflow.json`


### 2. Set Up Credentials
#### Google Sheets:
1. In n8n: **Settings** → **Credentials** → **Create New**
2. Select **Google Sheets OAuth2 API**
3. Follow OAuth flow to connect your Google account

#### SerpAPI:
1. Sign up at [serpapi.com](https://serpapi.com)
2. Get your API key from the dashboard
3. In the workflow's HTTP Request node:
   - Find the `api_key` parameter
   - Replace `YOUR_SERPAPI_KEY` with your actual key

### 3. Prepare Google Sheet
Create a Google Sheet with two tabs:
**Tab 1: Input (ZIP Codes)**
Name: `Zip_code` (or your preferred name)

<img width="447" height="585" alt="smple-input-data" src="https://github.com/user-attachments/assets/fb3444ed-5f9b-4c75-8a69-ac105be945fc" />

**Tab 2: Output (Results)**
Name: `Lead_info` (or your preferred name)

Headers: `searchedZip | hospitalName | address | latitude | longitude | phone | rating | hospitalType | departments | services | hours | website | googleMapsUrl | placeId |  | scrapedDate`

### 4. Configure Workflow
Update these nodes:
**"Get row(s) in sheet" node:**
- Set your Google Sheet document
- Set sheet name to your input tab
- Range: `A2:D` (dynamic - reads all rows)

**"Append to Google Sheets" node:**
- Set your Google Sheet document  
- Set sheet name to your output tab

**"HTTP Request" node:**
- Update `q` parameter with your search term (e.g., "hospital", "restaurant")
- Optionally adjust `ll` radius (currently 14z ≈ 25 miles)

### 5. Run
- Click **Execute Workflow**
- Monitor progress in real-time
- Check your Google Sheet for results


## 📊 Workflow Structure

<img width="1393" height="394" alt="workflow-diagram" src="https://github.com/user-attachments/assets/e86f9738-ce8f-4cd4-91ec-380e997b7aa2" />


## 📈 Expected Output

<img width="1678" height="303" alt="sample-output-data" src="https://github.com/user-attachments/assets/0b4869d3-1aea-4da6-befa-edf70dd6870e" />
