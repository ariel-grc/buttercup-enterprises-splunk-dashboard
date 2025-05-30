# 🛍️ Buttercup Enterprises: Cross-Team Splunk Dashboard

## 📊 Overview

Built a dynamic Splunk dashboard delivering actionable insights for **IT Operations**, **DevOps**, **Business Analytics**, and **Security/Fraud** teams across a simulated eCommerce environment.

This project simulates enterprise-wide use of Splunk at a fictional U.S.-based eCommerce retailer, *Buttercup Enterprises*. As a **Splunk Power User**, I developed a fully interactive dashboard in **Splunk Dashboard Studio** tailored to the insights required by:

- **IT Operations**: Web server status codes over time  
- **DevOps**: Browser failures and OS trends  
- **Business Analytics**: Lost revenue due to failed purchases  
- **Security & Fraud**: Geo-mapped web traffic and non-U.S. access patterns  

The dashboard supports both **light and dark modes** and features visualizations across custom timeframes (e.g., last 60 minutes, last 24 hours).

---

## 🔧 Technologies Used

| Tool / Technology         | Purpose                                      |
|---------------------------|----------------------------------------------|
| **Splunk**                | Data analysis and visualization              |
| **Search Processing Language (SPL)** | Crafting queries for each team’s needs |
| **Dashboard Studio**      | Building interactive visualizations          |
| **CSV Lookups**           | Enriching product purchase data              |
| **iplocation / geostats** | Mapping geographic activity for fraud detection |
| **Windows 11 / Server 2022** | Development environments                  |

---

## 📈 Dashboard Components

### 🔹 IT Operations View
**Use case:** Track successful vs. unsuccessful web server requests  
**SPL Sample:**   
```spl index=main sourcetype=access_combined | timechart count by status limit=10 ```

<img src="https://i.imgur.com/yHcV2Dn.png" height="80%" width="80%" alt="Creating Splunk Dashboard"/>

### 🔹 DevOps View
**Use case:** Top Operating Systems  
**SPL Sample:**   
``` spl index=main sourcetype=access_combined | top limit=20 platform showperc=f ```

<img src="https://i.imgur.com/RTEodWE.png" height="80%" width="80%" alt="Creating Splunk Dashboard"/>

**Use case:** Browsers with Most Failures  
**SPL Sample:**   
``` spl index=main sourcetype=access_combined status>=400 | timechart count by useragent limit=5 useother=f ```

<img src="https://i.imgur.com/OZstsnI.png" height="80%" width="80%" alt="Creating Splunk Dashboard"/>

### 🔹 Business Analytics View
**Use case:** Lost Revenue from Failed Purchases  
**SPL Sample:**   
``` spl index=main sourcetype=access_combined action=purchase status>=400 ```   
``` | lookup product_codes.csv product_id ```   
``` | timechart sum(product_price) ```  

<img src="https://i.imgur.com/APZuASl.png" height="80%" width="100%" alt="Creating Splunk Dashboard"/>

### 🔹 Security & Fraud View
**Use case:** Customer Locations (Geo Heat Map)    
**SPL Sample:**   
``` spl index=main sourcetype=access_combined | iplocation clientip | geostats count by City ```  

<img src="https://i.imgur.com/gIb1t6x.png" height="80%" width="80%" alt="Creating Splunk Dashboard"/>

**Use case:** Exclude U.S. IPs      
**SPL Sample:**   
``` spl index=main sourcetype=access_combined | iplocation clientip ```   
``` | search Country!="United States" ```   
``` | geostats count by City ```   

<img src="https://i.imgur.com/KxpDPcU.png" height="80%" width="80%" alt="Creating Splunk Dashboard"/>

---

## 🖥️ Sample Views

**Dashboard over last 60 minutes**

<img src="https://i.imgur.com/MlSQRTf.png" height="80%" width="80%" alt="Creating Splunk Dashboard"/>

**Dashboard over last 24 hours**

<img src="https://i.imgur.com/SjgoCIN.png" height="80%" width="80%" alt="Creating Splunk Dashboard"/>

**Views in dark mode over time**

<img src="https://i.imgur.com/zfdQUf4.png" height="80%" width="80%" alt="Creating Splunk Dashboard"/>
  
---

## 💡 Business Value
This project demonstrates how security-aware organizations can leverage Splunk to:

- Monitor availability
- Surface performance anomalie
- Identify browser/OS compatibility issue
- Track fraud-related behavior by geography
- Align insights across cross-functional teams in a single platform

---

📬 Contact
Interested in collaborating or learning more?
Let’s connect on [LinkedIn](www.linkedin.com/in/arielbethea) or open an issue in this repo.


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
