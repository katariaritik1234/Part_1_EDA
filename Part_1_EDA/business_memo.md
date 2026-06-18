# Internal Business Memo: Pre-Campaign Churn Investigation

**To:** Product, Marketing, and Customer Success Teams
**From:** Data Science & Machine Learning Engineering
**Subject:** Urgent vulnerabilities identified prior to D2C retention campaign launch

Before allocating budget to widespread discount or retention campaigns, an exploratory data analysis (EDA) of our historical 2,400-customer dataset has revealed several critical vulnerabilities driving a highly elevated **47.0% baseline churn rate**. 

Deploying blanket discounts will not solve these root issues. The data strongly suggests we must investigate the following five areas immediately:

### 1. The "Google Search" Acquisition Trap
While organic and referral channels yield positive retention, customers acquired via **Google Search** are churning at a higher absolute rate than they are staying. 
* **Action Required:** Marketing must audit current Google Ad copy and targeting parameters. We are likely acquiring low-intent, single-purchase buyers, or our ad messaging is misaligned with the actual product experience.
* **Evidence:**
*![Churn by Acquisition Channel](Outputs\chart2_churn_by_channel.png)*


### 2. The Silent Churner Phenomenon
Counter-intuitively, retained customers actually submit *more* support tickets than churned customers. The median ticket count for churned customers is strictly zero.
* **Action Required:** Customer Success must stop viewing a lack of complaints as a sign of satisfaction. Churning customers do not complain; they simply disengage. We need proactive outreach rather than reactive ticket resolution.
* **Evidence:**
*![Do Support Tickets Predict Churn?](Outputs\chart3_support_tickets_vs_churn.png)*


### 3. The 14-Day Inactivity Danger Zone
A customer's website login recency is a massive predictor of churn risk. Retained customers log in with a median recency of ~7 days, whereas churned customers sit at a median of ~25 days.
* **Action Required:** Product and CRM teams must trigger automated re-engagement workflows the moment a customer crosses the 14-day inactivity threshold. Waiting 60 days to intervene is too late.
* **Evidence:**
*![Website Inactivity vs. Churn Risk ](Outputs\chart4_web_activity_vs_churn.png)*

### 4. The Premium Abandonment Risk
While general discount usage is similar between both groups, there is a distinct cluster of zero-discount (full-price) buyers who are actively churning. 
* **Action Required:** The retention strategy may be over-indexing on deal-hunters. We must design VIP retention strategies for premium buyers who are silently abandoning the brand despite being insensitive to price.
* **Evidence:**
*![Discount Sensitivity vs. Churn Risk](Outputs\chart5_discount_usage_vs_churn.png)*

### 5. The "Baby Care" Product Bleed
"Baby Care" is the only product category suffering a negative retention ratio (the total number of churned customers exceeds retained customers). 
* **Action Required:** Merchandising must investigate pricing, formulation, and competitor alternatives for our baby products. The data suggests parents treat these as highly commoditized, easily swappable purchases compared to our core beauty lines.
* **Evidence:**
*![Churn Risk by Product Category](Outputs\chart6_churn_by_category.png)*