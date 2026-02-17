# AI Security Scanner for AWS S3
**Automated Cloud Security Auditing with Google Gemini AI**

**Author:** Wajd Alfehaid  
**Email:** wajdalfehaid@gmail.com  
**Tech Stack:** AWS Lambda, Amazon S3, EventBridge, Python, Google Gemini AI

---

## 🚀 Project Overview
In modern cloud environments, misconfiguration is a leading cause of data breaches. This project implements an **AI-powered security scanner** that automatically monitors AWS S3 bucket encryption configurations. 

By integrating **AWS Lambda** with the **Google Gemini API**, the system doesn't just flag issues—it provides intelligent, context-aware analysis of security risks and offers precise remediation steps. This project bridges the gap between theoretical cloud security and practical, automated implementation.



## 🛠 System Architecture & Workflow
The scanner operates through a serverless lifecycle to ensure zero infrastructure management:

1.  **Trigger:** An **AWS EventBridge** rule initiates the Lambda function every 12 hours.
2.  **Scan:** The Python script (using `boto3`) iterates through all S3 buckets to check for `ServerSideEncryptionConfiguration`.
3.  **Analysis:** Raw JSON configuration data is sent to the **Gemini Pro** model.
4.  **Reporting:** Gemini interprets the technical data and returns a human-readable security assessment, identifying risks and suggesting fixes.

---

## 💻 Implementation Details

### 1. The Intelligence: Integrating Gemini AI
Google Gemini acts as a virtual Security Analyst. While traditional scanners provide binary (Pass/Fail) results, Gemini analyzes the *impact* of the configuration.

* **Authentication:** The Gemini API key is stored securely as an **AWS Lambda Environment Variable** (`GOOGLE_API_KEY`), ensuring no sensitive credentials are hardcoded.
* **Logic:** The function uses the `google-generativeai` library to transform raw AWS metadata into actionable security insights.

### 2. The Compute: AWS Lambda Setup
The core logic resides in a serverless Python environment.

* **Handler Configuration:** The runtime is set to `s3_scanner.lambda_handler`, identifying the specific entry point for execution.
* **Environment Variables:** Accessible via `os.environ['GOOGLE_API_KEY']`, allowing the code to remain portable and secure.

### 3. Deployment Packaging
Because the `google-generativeai` library is not native to the Lambda environment, I created a custom **Deployment Package**:
1.  Installed dependencies locally into a virtual environment (`venv/`).
2.  Bundled the `site-packages/` directory with the `s3_scanner.py` script.
3.  Compressed the contents into a `.zip` file for deployment to the AWS Console.

---

## ⏱️ Automation & Scheduling
To ensure continuous monitoring without manual intervention, I utilized **Amazon EventBridge**. 
* **Rule Type:** Schedule-based trigger.
* **Rate:** `rate(12 hours)`.
* **Benefit:** This transforms the tool from a reactive script into a proactive security guardrail that maintains a strong cloud security posture.

---

## 📝 Key Takeaways
* **Serverless Proficiency:** Gained hands-on experience packaging Python dependencies for AWS Lambda.
* **AI Integration:** Learned how to prompt-engineer raw infrastructure data for concise security summaries.
* **Security Best Practices:** Reinforced the importance of Least Privilege (IAM) and Secret Management (Environment Variables).

---

## 🔮 Future Enhancements
* **Slack/Email Integration:** Send Gemini-generated reports directly to a security team via Amazon SNS.
* **Multi-Service Scanning:** Expand the script to analyze IAM Policies and Public Access Blocks.
* **Auto-Remediation:** Allow the AI to suggest and execute Python snippets to automatically enable encryption on non-compliant buckets.
