# Cyber Threat Analytics

AI-powered cyber threat analytics platform for network intrusion detection, explainable AI, and interactive cyber-security analytics.

## Project Goals

- Detect malicious network traffic using machine learning.
- Classify different attack categories such as DDoS, PortScan, Botnets, and Web Attacks.
- Provide explainable predictions using SHAP.
- Build interactive dashboards with modern web technologies.
- Deploy a publicly accessible live demo.

## Dataset

**CICIDS2017 (MachineLearningCVE)**

- 2,830,743 network flows
- 79 network traffic features
- 11 attack categories
- ~844 MB raw data

### Attack Timeline

| Day | Attacks |
|------|---------|
| Monday | BENIGN |
| Tuesday | FTP-Patator, SSH-Patator |
| Wednesday | DoS, Heartbleed |
| Thursday | Web Attacks, Infiltration |
| Friday | Bot, PortScan, DDoS |

## Tech Stack

### Data Analysis
- Python
- Pandas
- Polars
- NumPy
- Plotly

### Machine Learning
- Scikit-Learn
- XGBoost
- LightGBM
- SHAP

### Full Stack
- Next.js
- TypeScript
- TailwindCSS

### Database
- PostgreSQL
- Prisma

### Deployment
- Docker
- Vercel
- Railway

## Repository Structure

```text
data/
notebooks/
reports/
ml/
web/
docs/
