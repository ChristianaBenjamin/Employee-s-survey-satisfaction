# Pierce County Employee Engagement Survey Analysis
A data analysis project exploring employee engagement survey responses from Pierce County, WA government employees, built end-to-end with Power Query, DAX, and Power BI.
## Project overview
Pierce County conducts a voluntary employee engagement survey across its government departments. This project cleans, analyzes, and visualizes the raw survey export to answer three core questions:
Which survey questions did respondents agree with or disagree with most?
Are there patterns or trends by department or role?
What steps might the employer take to improve employee satisfaction based on the results?
Beyond the brief, the analysis also investigates whether the gap between leadership and staff sentiment holds up within the lowest-scoring department specifically, or whether it's an organization-wide pattern only.

## Dataset
Source: Pierce County WA employee engagement survey (voluntary, government employees)
Raw size: 14,725 records, 10 fields
Structure: long format — one row per question per respondent, not one row per person
Scale: responses are coded 0–4, where 0 = Not Applicable, 1 = Strongly Disagree, 2 = Disagree, 3 = Agree, 4 = Strongly Agree. There is no neutral midpoint.
Fields: Response ID, Status, Question, Response, Response Text, Department, Director, Manager, Supervisor, Staff

## Data cleaning
- Duplicate rows
15 fully duplicate rows (every field identical)
Removed using Remove Duplicates across all columns — 14,725 → 14,710 rows

-Inconsistent question text
"&" vs. "and" and trailing whitespace created 12 distinct question labels for what should be 10 real questions
Trimmed whitespace and standardized "&" to "and" so each question maps to exactly 1,471 responses

-Incomplete responses
135 question-level skips (0.9% of all question-opportunities), with null Response and Response Text
Excluded from scoring measures (filtered at the DAX level, not deleted from the table) so a completion-rate metric could still be reported

- Blank role tags
10,572 rows (72%) had no Director / Manager / Supervisor / Staff flag set
Recoded as "Unspecified" via a calculated Role column rather than dropped or mislabeled as "Other," since these appear to be respondents who simply didn't disclose seniority

## Tools used
#### Power Query — data cleaning and transformation
#### DAX — calculated measures (agreement rate, average score, completion rate, respondent count)
#### Power BI — dashboard and visualizations
#### Microsoft Word — written report with findings and recommendations

## Dashboard structure
The Power BI report is split across five pages so each visual has room to display fully
![Dashboard preview](https://github.com/ChristianaBenjamin/Employee-s-survey-satisfaction/blob/main/Survey%20dashboard.png)

## Key findings
#### 1. Role clarity is the strongest result; 
Recognition and belonging are the weakest. 92.6% of respondents agree they know what's expected of them at work — the highest score in the survey. By contrast, only 65.2% felt recognized for good work in the past 7 days, and just 52.4% report having a close friend at work.
#### 2. Sheriff's Department is a significant outlier.
Sheriff's Department scores 51.5% agreement overall, more than 20 points below every other department (which range from 74% to 92%). Breaking it down by question shows the gap is driven by the same two weak spots seen organization-wide — recognition (1.94/4) and growth opportunities (2.16/4) — just far more severe.
#### 3. Satisfaction declines steadily from leadership to frontline staff
Average agreement drops from 86.6% among Directors to 73.9% among Staff, a 13-point gap, suggesting leadership's view of organizational morale is more optimistic than what frontline employees actually experience.

#### Recommendations
Build recognition into a recurring habit (e.g. a standing slot for peer shout-outs in team meetings) rather than a one-off campaign — the fastest-moving lever available.
Treat low "belonging" scores as a structural issue, not a morale problem, invest in cross-team projects and protected informal time rather than social events.
Give the Sheriff's Department a dedicated intervention - listening sessions focused specifically on recognition and growth, since an organization-wide rollout won't meaningfully reach the department that needs it most.
Open a direct upward feedback channel - between staff and leadership to close the perception gap between ranks.
Treat growth and development as retention infrastructure - visible internal mobility postings, training stipends, and clear promotion criteria.



