
 SSN-college-software-architecture-Assignments — Custom Python ETL (AlienVault OTX)

Student: Priyadharshini T (Roll No: 3122225001100)
Connector: AlienVault OTX – Subscribed Pulses

 📌 Project Overview

This ETL pipeline interacts with the AlienVault OTX API (`/api/v1/pulses/subscribed`) to retrieve the threat intelligence pulses you’re subscribed to. Each pulse contains related threat indicators (e.g., IPs, domains, file hashes) contributed by the cybersecurity community.

The workflow:

1. Extract subscribed pulses from OTX.
2. Transform them into a MongoDB-compatible schema.
3. Load them into a dedicated MongoDB collection (`alienvault_raw` by default).

The script adheres to the assignment requirements for secure credential handling, pagination, data validation, and proper Git practices.



 🌐 API Details

Base URL:
`https://otx.alienvault.com/api/v1`

Endpoint:
`/pulses/subscribed`

* Method: GET
* Authentication: API key in request header



 🧰 Technology Used

* Python 3.10+
* `requests`
* `python-dotenv`
* `pymongo`
* MongoDB (local or Atlas)



 🔐 Setup & Configuration

1. Clone repository & create branch

   ```bash
   git clone <shared-repo-url>
   cd SSN-college-software-architecture-Assignments
   git checkout -b <your-branch-name>
   ```

2. Install dependencies

   ```bash
   pip install -r requirements.txt
   ```

3. Configure environment variables (`.env`)

   ```
   OTX_API_KEY=your_alienvault_otx_api_key
   MONGO_URI=your_mongo_connection_uri
   DB_NAME=etl_database
   ```

4. Run the connector

   ```bash
   python etl_connector.py
   ```



 📦 MongoDB Output

Database: `DB_NAME` (default: `etl_database`)
Collection: `alienvault_raw`

Example document:

```json
{
  "id": "12345",
  "name": "Suspicious IP Activity",
  "description": "Indicators linked to a phishing campaign",
  "author_name": "Cyber Researcher",
  "tags": ["phishing", "malware"],
  "created": "2025-08-01T10:00:00",
  "modified": "2025-08-02T12:00:00",
  "indicators": [ ... ],
  "extracted_at": "2025-08-14T18:30:00+00:00",
  "_source": "alienvault_otx_pulses_subscribed",
  "_page": 1
}
