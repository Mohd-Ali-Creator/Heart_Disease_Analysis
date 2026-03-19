# Heart Disease Analysis - Interactive Web Application

![Project Banner](https://via.placeholder.com/1200x300/3498db/ffffff?text=Heart+Disease+Analysis+Dashboard)

A Flask-based web application that integrates Tableau dashboards and stories to provide interactive visualization and analysis of heart disease data. This project aims to make cardiovascular health insights accessible to healthcare professionals, researchers, and the general public.

## 📋 Table of Contents
- [Overview](#-overview)
- [Features](#-features)
- [Technology Stack](#-technology-stack)
- [Project Structure](#-project-structure)
- [Installation Guide](#-installation-guide)
- [Configuration](#-configuration)
- [Integrating Tableau Visualizations](#-integrating-tableau-visualizations)
- [Troubleshooting SSL Certificate Issues](#-troubleshooting-ssl-certificate-issues)
- [Deployment](#-deployment)
- [Screenshots](#-screenshots)
- [Contributing](#-contributing)
- [License](#-license)
- [Contact](#-contact)

## 🔍 Overview

Heart disease remains one of the leading causes of death worldwide. This project leverages data visualization to help understand the patterns, risk factors, and demographics associated with cardiovascular diseases. By combining Tableau's powerful visualization capabilities with Flask's lightweight web framework, we've created an interactive platform that makes complex medical data accessible and understandable.

**Key Insights:**
- Gender distribution in heart disease cases
- Impact of diabetes on heart health
- Effects of physical activity and lifestyle choices
- Age demographics and risk patterns
- Correlation between smoking, alcohol, and stroke

## ✨ Features

- **Interactive Dashboards**: Real-time data exploration with Tableau visualizations
- **Story Narratives**: Guided data stories explaining key findings
- **Responsive Design**: Mobile-friendly interface that works on all devices
- **Risk Factor Analysis**: Visual breakdown of obesity, sedentary lifestyle, and smoking impacts
- **Demographic Filters**: Gender, age, and ethnicity-based data segmentation
- **Educational Content**: Information about heart disease causes and prevention

## 🛠 Technology Stack

| Component | Technology |
|-----------|------------|
| Backend Framework | Flask (Python) |
| Frontend | HTML5, CSS3, JavaScript |
| Visualization | Tableau Public / Tableau Server |
| Styling | Custom CSS, Google Fonts |
| Deployment | Gunicorn, Nginx (optional) |
| Version Control | Git |

## 📁 Project Structure
heart_disease_analysis/
│
├── app.py # Main Flask application
├── requirements.txt # Python dependencies
├── README.md # Project documentation
│
├── static/
│ ├── css/
│ │ └── style.css # Custom styles
│ └── images/ # Project images
│
├── templates/
│ ├── base.html # Base template with navigation
│ ├── index.html # Home page
│ ├── dashboard.html # Dashboard page
│ └── story.html # Story page
│
└── ssl/ # SSL certificates (for local HTTPS)
└── tableau_cert.crt # Tableau server certificate

text

## 🚀 Installation Guide

### Prerequisites
- Python 3.8 or higher
- pip (Python package manager)
- Git (optional)
- Tableau Public account (for embedding)

### Step 1: Clone the Repository
bash
git clone https://github.com/yourusername/heart-disease-analysis.git
cd heart-disease-analysis
Step 2: Create Virtual Environment
bash
# Windows
python -m venv venv
venv\Scripts\activate

# Mac/Linux
python3 -m venv venv
source venv/bin/activate
Step 3: Install Dependencies
bash
pip install -r requirements.txt
Step 4: Run the Application
bash
python app.py
Step 5: Access the Application
Open your browser and navigate to: http://localhost:5000

⚙️ Configuration
Environment Variables
Create a .env file in the root directory:

env
FLASK_ENV=development
FLASK_APP=app.py
SECRET_KEY=your-secret-key-here
TABLEAU_SERVER_URL=https://your-tableau-server.com
TABLEAU_SITE_ID=your-site-id  # If using Tableau Online/Server
requirements.txt
text
Flask==2.3.3
python-dotenv==1.0.0
gunicorn==21.2.0  # For production deployment
📊 Integrating Tableau Visualizations
For Tableau Public (Free)
Publish your workbook to Tableau Public:

Open Tableau Desktop

Go to Server > Tableau Public > Save to Tableau Public

Create an account if needed

Name your workbook and publish

Get the embed code:

Visit your published workbook on Tableau Public

Click the Share button

Copy the iframe embed code

Add to your template:

html
<!-- In templates/dashboard.html -->
<div class="tableau-embed">
    <iframe src="https://public.tableau.com/views/YourWorkbook/Dashboard1?:embed=y&:showVizHome=no" 
            width="100%" 
            height="600" 
            frameborder="0">
    </iframe>
</div>
For Tableau Server (Private/Enterprise)
Configure Tableau Server settings:

Ensure your Tableau Server allows embedding

Set up trusted authentication if required

Use Tableau JavaScript API:

html
<script type="text/javascript" src="https://your-tableau-server.com/javascripts/api/tableau-2.min.js"></script>
<div id="tableauViz"></div>
<script>
    var placeholderDiv = document.getElementById('tableauViz');
    var url = 'https://your-tableau-server.com/views/Workbook/Dashboard';
    var options = {
        hideTabs: true,
        width: "100%",
        height: "600px"
    };
    var viz = new tableau.Viz(placeholderDiv, url, options);
</script>
🔒 Troubleshooting SSL Certificate Issues
If you encounter the error: Server's certificate is not trusted, follow these steps:

Option 1: Import Certificate to Java TrustStore
Step 1: Download Tableau Server Certificate

bash
# Using OpenSSL
openssl s_client -connect your-tableau-server.com:443 -showcerts </dev/null 2>/dev/null | openssl x509 -outform PEM > tableau_cert.crt
Step 2: Find Java TrustStore Location

bash
# Windows
"C:\Program Files\Java\jre1.8.0_*\lib\security\cacerts"

# Mac/Linux
/usr/lib/jvm/java-8-openjdk/jre/lib/security/cacerts
Step 3: Import Certificate

bash
keytool -import -alias tableauserver -keystore "path/to/cacerts" -file tableau_cert.crt
# Default password: changeit
Option 2: Configure Flask to Skip SSL Verification (Development Only)
Warning: Only use this for development/testing!

python
# In your Flask app, when connecting to Tableau
import ssl
import requests

# Create unverified SSL context
ssl._create_default_https_context = ssl._create_unverified_context

# Or use requests with SSL verification disabled
response = requests.get('https://your-tableau-server.com', verify=False)
Option 3: Set Environment Variables
bash
# For Java-based Tableau connections
export JAVA_TOOL_OPTIONS="-Djavax.net.ssl.trustStore=/path/to/cacerts -Djavax.net.ssl.trustStorePassword=changeit"
🌐 Deployment
Deploy to Heroku
Create a Procfile:

text
web: gunicorn app:app
Create runtime.txt:

text
python-3.9.18
Deploy:

bash
heroku create your-app-name
git push heroku main
heroku open
Deploy to PythonAnywhere
Upload files to PythonAnywhere

Set up a web app with manual configuration

Configure WSGI file to point to your Flask app

Deploy to AWS EC2
Launch an EC2 instance

Install Python and dependencies

Set up Nginx as reverse proxy

Configure Gunicorn

Set up SSL with Let's Encrypt

📸 Screenshots
Home Page
https://via.placeholder.com/800x400/e74c3c/ffffff?text=Home+Page+Screenshot

Dashboard View
https://via.placeholder.com/800x400/3498db/ffffff?text=Dashboard+Screenshot

Story View
https://via.placeholder.com/800x400/2ecc71/ffffff?text=Story+Screenshot

🤝 Contributing
Contributions are welcome! Please follow these steps:

Fork the repository

Create a feature branch (git checkout -b feature/AmazingFeature)

Commit changes (git commit -m 'Add AmazingFeature')

Push to branch (git push origin feature/AmazingFeature)

Open a Pull Request

Code Style Guidelines
Follow PEP 8 for Python code

Use meaningful variable names

Add comments for complex logic

Keep templates clean and well-indented

📄 License
This project is licensed under the MIT License - see the LICENSE file for details.

📞 Contact
Project Maintainer: Your Name

Email: your.email@example.com

GitHub: @yourusername

LinkedIn: Your Profile

Project Link: https://github.com/yourusername/heart-disease-analysis

🙏 Acknowledgments
National Heart, Lung and Blood Institute, Framingham (USA) for the data

Tableau for visualization tools

Flask community for the excellent framework

All contributors and testers

Made with ❤️ for better heart health awareness

text

## Additional Files to Include

### 1. `requirements.txt`
Flask==2.3.3
python-dotenv==1.0.0
gunicorn==21.2.0
requests==2.31.0

text

### 2. `Procfile` (for Heroku)
web: gunicorn app:app

text

### 3. `runtime.txt` (for Heroku)
python-3.9.18

text

### 4. `.gitignore`
Virtual Environment
venv/
env/
ENV/
env.bak/
venv.bak/

Python
pycache/
*.py[cod]
*$py.class
*.so
.Python

Distribution
dist/
build/
*.egg-info/

IDE
.vscode/
.idea/
*.swp
*.swo

Environment variables
.env
*.env

SSL certificates (keep if needed for deployment)
ssl/.crt
ssl/.key

Database
*.db
*.sqlite
*.sqlite3

Logs
*.log

text

This README provides everything needed for someone to understand, install, and use your project. Customize the placeholder text (like your name, GitHub URL, etc.) with your actual information.

