# **Report (29/8): Comparison between two papers related to Anonymized Data**
## **Introduction**
This report aims to make a comparison between the problem of two papers related to collaborative anonymization. 
- The first one is _K. Wong, N. A. Tu, D. Bui, S. Y. Ooi, and M. H. Kim, "PrivacyPreserving Collaborative Data Anonymization with Sensitive QuasiIdentifiers," in 2019 12th CMI Conference on Cybersecurity and
Privacy (CMI), 28-29 Nov. 2019 2019, pp. 1-6, doi:
10.1109/CMI48017.2019.8962140._
- and the second one is 
## **Similarities and differences**
### **Similarities**
- Respondents are not willing to submit their **full data** due to privacy concern.
- **Trust-party oriented**:  Collaborative data anonymization performed by **data collector** is neccessary because locally data anonymization may not result in desired privacy protection level.
### **Differences**

|First paper|Second paper 2|
|-|-|
|The collected data is used for a local analysis to support a **query-answer system**. - No data should be leaked to external parties|The data anonymization helps vehicles to share information safely in an **insecure vehicular ad-hoc network** - Run-time privacy-related issues inherited from superset Internet-of-Things (_IoT_)|
|**The agency** is responsible for collecting data|**Cluster-head** is responsible for collecting data|
|Each respondent **submit primary**  and **secondary-QIDs** to agent|The vehicle submit the **locally anonymized data** which is **encrypted** with a preselected symmetric key cryptography|
|**No local data anonymization** - not resulting in desired privacy protection level, distribution of equivalence class can be unbalanced|**Combined** privacy-preserving data anonymization technique - participating vehicles achieve an initial level of anonymization|
|_sensitive_-QID is not submitted due to the risk of deriving sensitive attribute|_sensitive_-QID is used to form equivalence class
