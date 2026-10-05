# DAISISG-HEATGUARD

In the section under "Additional info", we have placed our mock prototype under "Upload a File". This is our draft using Claude showcasing our vision as to how HeatGuard is to be built. We created a roadmap as to how the prototype works.

**------------------------------------------------------------------------------------------------ROADMAP------------------------------------------------------------------------------------------------**

**Get Data Sources:** The NEA real-time air temperature and rainfall (plus WBGT), HDB elderly population, MSF Senior Activity/Activity Ageing Centre locations, and URA subzone boundaries, are all from data.gov.sg 

**Ingestion:** A scheduled Databricks Job polls the real-time APIs every 10-15 minutes and the stored data is saved into the Delta tables. The Static Datasets are loaded once 

**Clean and combine data:** The Bronze to Silver to Gold pipeline runs in Databricks. Bronze is the messy raw data that is saved exactly as it was received. Silver would be when the Data is cleaned up, with bad reading removed and each weather station matched to the neighbourhood.

**Scoring and AI:** Gold computes the Head Hazard, Vulnerability and Access Deficit scores and the overall HeatGuard Priority Score. The MLflow tracks the weighting sensitivity tests, and the LLM (via Foundation Model APIs) writes plain English explanations of each area’s score. For each of the neighbourhood, HeatGuard asks 3 questions: How hot it is? How many elderly residents live in that area? And how far is the nearest senior centre? It combines all the answers into one priority score. 

**Dashboard and alerts**  The AI/BI dashboard shows the priority map and rankings, a Genie space also answers natural-language questions, and SQL alerts to notify the users when an area turns into High priority. A map with neighbourhoods coloured green, amber or red. Including a list of which areas need help first. If an area turns red, an alert would be sent out.

In one sentence, Heatguard collects government data automatically, cleans it, scores every neighbourhood, and shows the results on a map so that people would know where to find help first.

**------------TUTORIAL------------**

You can start by downloading the heatguard.html file and double click it. It would open in your web browser in a tab as per normal. There won’t be anything to install or log into. The website is made preferably for a laptop or desktop screen, but it can also be used on a phone.

How to read what you see?
 
You would see a score that is /100. The higher the score the more attention is needed to the area. 

As for the colours, deep red indicates High, Orange is Medium, pale peach is Low.
 
The ~ symbol or a dashed ring indicates that the area has no weather station of its own so the temperature is gauged from the other nearby weather stations. The site would always tell you when the number is an estimate.  

The badge at the top-right corner (e.g “Heat: High 33.6°C") shows how hot it is overall as of the time you check. 

A first visit:

Starting on the Overview page (the landing page). Reading the big question, look at the “Top priorities right now” card on the right. It would show the three areas that need attention first.  Below it, there would be four number cards that summarized the situation. Click any “Learn more” link to see how each of the three factors are measured. 

Click “Run heat analysis” on the left you set up a scenario: 

Temperature slider, or the quick buttons which include Mild day, Typical, Hot or Heatwave.
Showers toggle lets you simulate that it is raining in the east. 
Region would focus on one part of Singapore 
Weight preset would decide on how much each factor counts but leave it on the Baseline for now. 
Press Analyse. The site would work through the five steps with tickers and a progress bar. Click the “Show reasoning” on any of the steps to see exactly what it did. When it finishes, it would take you to the results page.
On Priority Areas (the main results page), the left side shows a map and the right side would show a ranked list.
On the map: Each of the circles indicate an area, the bigger the circle means that there are more seniors who live there. Hovering over the circle would provide you with a quick summary but clicking it would give you a full detailed report. 
In the list: click a row to see the short and summarised reason. You’re able to use the search box to find an area, click the column titles to sort and turn on “Show all areas” to see all the 25 instead of just the top 10. 
Click any area in order to open its detail panel. A panel slides in from the right showing how the score was built piece by piece, the nearest Senior Activity Centres, and suggested actions, such as “Welfare-check outreach to seniors” or “Set up a cooling point” 
Try the switch “What if we add a cooling point here?” The score would drop immediately and the map and list updates with it. Close the panel with the X, the Esc key, or by clicking outside it.
Try the three “aha” moments. There is a quick control bar at the top of the results page for this. 
Drag the temperature down to about 30°C. No area turns red and the map turns cooler. On a mild day nothing would be indicated as High, even in the areas with many seniors.
Switch between 50/35/25, 60/30/10 and 40/40/20. The list reorders a little, but the same areas stay near the top. Hence, the ranking doesn’t depend on one arbitrary choice. 
Add a cooling point in Choa Chu Kang. It drops from High to Medium.
Methodology explains the formula as to why heat counts the most, what the site deliberately leaves out, and its limitations. It’s useful if a judge asks how we would know if it is fair. 
About covers the problem and the team.

Datasets used in mock prototype: 
HDB Elderly Population:
 https://data.gov.sg/datasets/d_4180067b350bc9839a4cea487841d5d1/view
PM2.5 Air Pollutant:
 https://data.gov.sg/datasets/d_397fe8de643aea9927bdee32e49307ff/view
Realtime Weather Readings collection (groups the 5 below):
 https://data.gov.sg/collections/1459/view
Air Temperature across Singapore:
 https://data.gov.sg/datasets/d_66b77726bbae1b33f218db60ff5861f0/view
Rainfall across Singapore:
 https://data.gov.sg/datasets/d_6580738cdd7db79374ed3152159fbd69/view
Relative Humidity across Singapore:
 https://data.gov.sg/datasets/d_2d3b0c4da128a9a59efca806441e1429/view
Wind Speed across Singapore:
 https://data.gov.sg/datasets/d_7677738484067741bf3b56ab5d69c7e9/view
Wind Direction across Singapore:
 https://data.gov.sg/datasets/d_534cf203023b51f51f879145ccc56ff9/view
