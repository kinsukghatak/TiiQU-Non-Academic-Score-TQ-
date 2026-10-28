# Non-Academic-Score-TQ-
This project implements an automated trustworthiness scoring system for various non academic entities by analyzing their online presence, certifications, transparency reports, and published documents. The system extracts and scores information across multiple dimensions to provide a comprehensive non-academic trustworthiness assessment.


🎯 What Does This Do?
This tool automatically evaluates how trustworthy an organization is by searching the internet for evidence of their:

Certifications and affiliations
Awards and recognition
Security and privacy practices
Sustainability efforts
Scientific credentials
Transparency in funding and governance
Published annual reports

Think of it as: A background check system for companies, NGOs, media outlets, and research organizations.

✨ How It Works (Simple Version)

You provide: Organization name + type (startup, media, NGO, etc.)
System searches Google: Finds relevant pages about that organization
System analyzes content:

Reads webpages for specific keywords
Downloads and reads PDF reports
Looks for evidence of certifications, awards, transparency, etc.


You get: A score showing how trustworthy the organization appears. In some cases the automated scoring may fail owing to non scrapabaility of the web pages or pdf files. In such cases admin should manually search for the key words and assign a relevant score under a specific category. 


📊 What Gets Checked? (12 Categories)
Core Integrity (6 categories)
From Websites and webpages: 
✅ Certifications - ISO, GDPR, industry memberships
🏆 Awards - Industry recognition, excellence awards
🔒 Data Security - Privacy policies, SOC 2, encryption standards
🌱 Sustainability - Carbon neutrality, ESG practices, green certifications
🔬 Scientific Validity - Peer-reviewed research, clinical trials
📝 Content Integrity - Fact-checking, editorial standards

Transparency (6 categories)
From Websites:
💰 Funding sources and donors
🏛️ Board members and leadership
📋 Annual reports and audits

From PDF Documents:
💼 Detailed funding reports
🏢 Governance structure documents
📊 Published annual/ESG reports

Example of the final code run : 

# Analyze an organization
results = analyze_entity_complete_with_transparency(
    entity_name="OpenAI",
    entity_type="startup"
)



📈 How Scoring Works
The system gives points as per the following design:
![TiiQU_Flowchart_Vertical](https://github.com/user-attachments/assets/53a7a938-a559-45a0-8b15-8ea00c227367)



💡 Real-World Examples
Example :  Startup
analyze_entity_complete_with_transparency("clarityAI", "startup")
Result: 
<img width="1258" height="330" alt="image" src="https://github.com/user-attachments/assets/5f3340d8-d352-4dcb-80da-83e1e02bd754" />


🔍 How It Actually Works (Technical)
Step 1: Web Search

Uses Google (via Serper API) to find relevant pages
Searches with category-specific keywords
Example: "Company X ISO certifications"

Step 2: Content Extraction
For Webpages:
Downloads HTML
Extracts all text
Searches for specific keywords

For PDFs:
Detects if result is a PDF file
Downloads and extracts text (first 10 pages)
Uses two methods: pdfplumber (primary) and PyPDF2 (backup)

Step 3: Analysis
Checks for category-specific keywords
Awards points based on entity type
Handles errors gracefully (blocked sites, timeouts, etc.)

Step 4: Reporting
Combines all 12 category results
Returns structured data (pandas DataFrame)
Easy to export to Excel, CSV, or databases


🛠️ Requirements
Python Packages:

beautifulsoup4 - Web scraping
requests - HTTP requests
PyPDF2 - PDF reading
pdfplumber - Advanced PDF processing
pandas - Data handling
Serper - Search API

System Requirements:
Python 3.7+
Internet connection
~100-200 MB memory for processing

- Points to note :
We are using Serper API here for the Google search as DuckDuck Go and Custom Google search didm't work as expected
Serper is google search API; using which the entire internet can be searched quite easily.
The prototype code has been developed using the 2000 free credits obtained through account creation by the developer
For periodic re runs and scoring a paid account has to be created first and then the API key has to be placed in the code below.
The basic plan is $25 per month for 1000 searches
More details can be found here : https://serpapi.com/?gad_source=1&gad_campaignid=1061187028&gbraid=0AAAAADD8kqMvKMgW7uF9GpeoV7rHy3X83&gclid=CjwKCAiAssfLBhBDEiwAcLpwfs6aIyQqasVWDzfYqGuro1NlrB2oaE-nl5P_tnP6JtuV-VlI2ae_whoCmk4QAvD_BwE




Limitations:
Only analyzes publicly available information
English-language content works best
Can't process image-only PDFs (no OCR)
Dependent on search engine results quality
May miss information if not properly tagged online


🔐 Privacy & Ethics
This tool:
Only accesses publicly available information
Does not store or share organization data
Respects website robots.txt files
Does not attempt to bypass authentication
Uses random user agents to avoid blocking (not to hide identity)



🐛 Troubleshooting
"No website found"
Solution: Organization may have weak online presence or ambiguous name. Try adding location or industry descriptor.
"Could not extract PDF text"
Solution: PDF may be image-based or password-protected. Check if PDF is publicly accessible.
"Score is 0 but information exists"
Solution: Keywords may not match exactly. Check keyword lists or add custom keywords.
Timeout errors
Solution: Slow internet or large files. Increase timeout values in code.

📊 Performance
Typical Analysis Time:
Single organization: 120-150 seconds



