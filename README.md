# IntelliLoan — Smart Loan Approval System using Spring Boot and H2O AutoML

## Overview
**IntelliLoan** is a smart loan approval system that leverages **machine learning** to automate loan approval decisions and predict optimal interest rates.  
It integrates **H2O AutoML** models within a **Spring Boot REST API**, enabling seamless ML inference as a service for production environments.

---

## Key Features
- **ML-as-a-Service:** Integrates predictive models (Python/R) into Spring Boot REST APIs.  
- **AutoML Integration:** Uses H2O AutoML with Gradient Boosting Models (GBM) for classification and regression tasks.  
- **Cross-language Compatibility:** Exports models as Java POJOs for direct Spring integration.  
- **Dockerized Deployment:** Full containerization for easy scalability and version rollout.  
- **Swagger UI:** Self-contained API documentation and testing interface.  

---

## Machine Learning Models

| Model Type | Objective | Algorithm | Metric |
|-------------|------------|------------|---------|
| **Binary Classification** | Predict whether a loan is good or bad | GBM | AUC = 0.685 |
| **Regression** | Predict loan interest rate | GBM | R² = 0.424, MSE = 11.1 |

### Key Predictors
`loan_amnt`, `term`, `emp_length`, `home_ownership`, `annual_inc`, `dti`, `revol_util`, `total_acc`, `longest_credit_length`, etc.

---

## Tech Stack
- **Backend:** Java, Spring Boot, Gradle  
- **Machine Learning:** H2O AutoML, Python/R  
- **Deployment:** Docker  
- **API Testing:** Swagger UI  

---

## How It Works
1. **Model Training:** Run the H2O script (`loan-approver-model.py` or `.R`) to generate Java POJOs.  
2. **Build Application:**  
   ```bash
   ./gradlew build -PpythonBasedMLModel=true
   ```
3. **Run the Spring Boot App:**
  ```bash
  java -jar intelliloan-0.0.1-SNAPSHOT.jar
  ```
4. **Launch via Docker:**
  ```bash
  docker build -t intelliloan .
  docker run intelliloan
  ```
5. **Access API Docs:**
  ```bash
  http://localhost:8080/swagger-ui.html
  ```
## Example Output
```json
{
  "labelIndex": 0,
  "label": "0",
  "classProbabilities": [0.8777, 0.1223],
  "interestRate": 12.08
}
```
## Interpretation:
Label	Meaning
0	Good loan — approved
1	Atrocious loan — not approved
## Notes
Download h2o-genmodel.jar:
```bash
curl http://localhost:54321/3/h2o-genmodel.jar > h2o-genmodel.jar
Models and predictions can be visualized in the H2O Flow UI.
```
## Applications
Credit risk prediction  
Insurance claim fraud detection  
E-commerce credit scoring  
Retail and inventory demand prediction  

## Author
Anurag Singh  
Indian Institute of Technology, Patna
