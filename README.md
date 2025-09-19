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
R programme :
# Load libraries
library(tidyverse)
library(lubridate)

# Import data (adjust path to your files)
daily_activity <- read_csv("dailyActivity_merged.csv")
sleep_day <- read_csv("sleepDay_merged.csv")
weight_log <- read_csv("weightLogInfo_merged.csv")

# --- 1. Check structure of datasets ---
glimpse(daily_activity)
glimpse(sleep_day)
glimpse(weight_log)

# --- 2. Check missing values ---
colSums(is.na(daily_activity))
colSums(is.na(sleep_day))
colSums(is.na(weight_log))

# --- 3. Remove duplicates ---
daily_activity <- daily_activity %>% distinct()
sleep_day <- sleep_day %>% distinct()
weight_log <- weight_log %>% distinct()

# --- 4. Standardize column names ---
daily_activity <- daily_activity %>% rename_with(tolower)
sleep_day <- sleep_day %>% rename_with(tolower)
weight_log <- weight_log %>% rename_with(tolower)

# --- 5. Convert dates into proper format ---
daily_activity <- daily_activity %>%
  mutate(activitydate = mdy(activitydate))

sleep_day <- sleep_day %>%
  mutate(sleepday = mdy_hms(sleepday))

weight_log <- weight_log %>%
  mutate(date = mdy_hms(date))

# --- 6. Check unique users in each dataset ---
n_distinct(daily_activity$id)
n_distinct(sleep_day$id)
n_distinct(weight_log$id)

# --- 7. Filter out users with less than 30 days of records ---
activity_days <- daily_activity %>%
  group_by(id) %>%
  summarise(days_logged = n_distinct(activitydate))

valid_users <- activity_days %>% filter(days_logged >= 30) %>% pull(id)

daily_activity <- daily_activity %>% filter(id %in% valid_users)
sleep_day <- sleep_day %>% filter(id %in% valid_users)

# --- 8. Handle zero values ---
# For example, if steps = 0 and calories = 0, drop those rows
daily_activity <- daily_activity %>%
  filter(!(totalsteps == 0 & calories == 0))

# --- 9. Verify consistency of units ---
summary(daily_activity$totalsteps)
summary(daily_activity$calories)
summary(sleep_day$totalminutesasleep)

- Loaded Fitbit datasets into R (`read_csv`)  
- Removed duplicates with `distinct()`  
- Checked missing values with `is.na()`  
- Standardized column names → lowercase  
- Converted dates with **lubridate**  
- Filtered users < 30 days logged  
- Removed rows with steps & calories = 0  

## 5. Analyze  
R programme :
# Load libraries
library(tidyverse)
library(lubridate)

# --- 1. Steps vs Calories correlation ---
steps_calories <- daily_activity %>%
  select(totalsteps, calories)

cor(steps_calories$totalsteps, steps_calories$calories, use = "complete.obs")
# --- 2. Active minutes vs Calories ---
activity_calories <- daily_activity %>%
  mutate(total_active_minutes = veryactiveminutes + fairlyactiveminutes + lightlyactiveminutes) %>%
  group_by(id) %>%
  summarise(avg_active_minutes = mean(total_active_minutes),
            avg_calories = mean(calories))

head(activity_calories)

# --- 3. Weekday activity patterns ---
weekday_activity <- daily_activity %>%
  mutate(weekday = wday(activitydate, label = TRUE)) %>%
  group_by(weekday) %>%
  summarise(avg_steps = mean(totalsteps),
            avg_calories = mean(calories))

weekday_activity

# --- 4. Sleep vs Activity relationship ---
sleep_activity <- sleep_day %>%
  inner_join(daily_activity, by = c("id", "sleepday" = "activitydate")) %>%
  select(id, totalminutesasleep, totalsteps, calories)

cor(sleep_activity$totalminutesasleep, sleep_activity$totalsteps, use = "complete.obs")
cor(sleep_activity$totalminutesasleep, sleep_activity$calories, use = "complete.obs")

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
