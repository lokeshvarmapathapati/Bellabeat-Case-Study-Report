# Bellabeat Case Study

# 📌 Introduction
# Bellabeat Case Study Report

## 1. Introduction
Bellabeat is a high-tech company that manufactures health-focused smart products...

## 2. Ask
### Business Task
Analyze smart device usage data to identify trends in consumer behavior...

### Key Questions
- What are some trends in smart device usage?  
- How could these trends apply to Bellabeat customers?  
- How could these trends help influence Bellabeat’s marketing strategy?  

### Stakeholders
- Urška Sršen – Cofounder and Chief Creative Officer  
- Sando Mur – Cofounder and key executive team member  
- Bellabeat Marketing Analytics Team  

## 3. Prepare
### Data Source
For this case study, I used the Fitbit Fitness Tracker Data available on Kaggle...

### Data Organization
- dailyActivity.csv → wide format  
- heartrate_seconds.csv → long format  

### Data Credibility & Limitations
- ✅ Reliable source (Kaggle)  
- ⚠️ Small sample size (30 users)  
- ⚠️ No demographics  
- ⚠️ Old data (2016)  

## 4. Process
- Loaded Fitbit datasets into R (`read_csv`)  
- Removed duplicates with `distinct()`  
- Checked missing values with `is.na()`  
- Standardized column names → lowercase  
- Converted dates with **lubridate**  
- Filtered users < 30 days logged  
- Removed rows with steps & calories = 0  

## 5. Analyze  
- Steps vs Calories → positive correlation  
- Active Minutes vs Calories → strong link  
- Weekly Trends → weekdays more active than weekends  
- Sleep vs Activity → slight negative correlation  

## 6. Share
### Key Findings
- Higher steps = higher calories burned  
- Weekday activity > weekend activity  
- Sedentary/lightly active users dominate  
- Very active users sleep slightly less  

### Recommendations
- Personalized coaching via app  
- Weekend wellness campaigns  
- Balanced messaging (activity + sleep)  
- Gamification & rewards system  
- Tie-in Bellabeat Leaf/Time as lifestyle trackers  

## 7. Act
### Conclusion
This analysis provides actionable insights that can help Bellabeat grow in the women’s wellness market.  

### Action Plan
- **Product Innovation** → integrate activity + sleep metrics  
- **User Engagement** → weekend challenges & notifications  
- **Marketing** → promote holistic wellness, not just steps  
- **Gamification** → badges, rewards, leaderboards  
- **Long-Term Strategy** → predictive analytics for personalization
- 
## 🎯 Business Task
Analyze Fitbit data to uncover consumer trends and develop marketing recommendations for Bellabeat.

## 📂 Dataset
- Source: [Fitbit Fitness Tracker Dataset (Kaggle)](https://www.kaggle.com/datasets/arashnic/fitbit)
- 30 users, activity, sleep, and calories data.

## 🛠️ Tools Used
- **R** → data cleaning, transformation, and analysis
- **Tableau** → visualization dashboards
- **CSV** → raw data

## 🔍 Process
- Cleaned and prepared Fitbit datasets in R  
- Removed duplicates, handled missing values  
- Standardized formats, filtered incomplete logs  
- Analyzed steps, calories, active minutes, sleep  

## 📊 Dashboard
Insights were visualized in Tableau.  
https://1drv.ms/b/c/d691e9daa9c26077/Eb4u4bq8_4JGp7tcuzd2KnsBnW4nNV8e8eZmrkby3Tfw0A?e=nGJF26

## 📈 Key Findings
- Higher steps = higher calories burned  
- Weekday activity > Weekend activity  
- Sedentary/lightly active users dominate → growth potential  
- Activity slightly reduces sleep duration  

## 💡 Recommendations
- Personalized coaching & notifications  
- Weekend challenges for engagement  
- Balanced messaging on activity + sleep  
- Gamification and rewards  

## ✅ Conclusion
Bellabeat should position itself as a **holistic women’s wellness brand**, combining fitness, sleep, and mindfulness tracking.

---
