# Stubble Burning vs Air Quality: Punjab/Haryana to Delhi

**Author:** Shreya Mishra | B.E. CSE (AIML), Chandigarh University

An interactive Tableau dashboard that tests whether crop-residue fires in Punjab and Haryana line up with air-quality spikes in Delhi and other Indian cities during the Oct-Nov burning seasons of 2015-2019.

**Live dashboard:** [Tableau Public link]

![Dashboard](dashboard.png)

## Question
Do spikes in satellite-detected fires in Punjab and Haryana coincide with worse air quality in downwind cities, and with what delay?

## Data
| Dataset | Source | Used for |
|---|---|---|
| VIIRS S-NPP 375 m active fire detections, Oct-Nov 2015-2019 | NASA FIRMS (firms.modaps.eosdis.nasa.gov) | Daily fire counts and fire intensity (FRP) |
| Air Quality Data in India (2015-2020), `city_day.csv` | CPCB, republished on Kaggle by Rohan Rao | Daily AQI, PM2.5, PM10 by city |

The raw FIRMS file (about 207 MB, 2.59M detections for all of India) is not included because of GitHub's file-size limit. Re-download it from the FIRMS Archive Download page.

## Method
1. Kept vegetation fires only (`type = 0`) and removed low-confidence detections.
2. Clipped detections to an approximate Punjab + Haryana boundary (a hand-drawn polygon, not an official map).
3. Aggregated to daily fire counts and total fire radiative power.
4. Joined daily fires to city AQI by date for 8 cities: Amritsar, Chandigarh, Delhi, Gurugram, Lucknow, Patna, plus Bengaluru and Mumbai as comparison cities.
5. Added a 4-day lagged fire count to capture smoke travel time.
6. Built the dashboard in Tableau using calculated fields, LOD expressions, dual-axis charts, calendar heatmaps, and a fire map.

## Files
- `stubble_aqi_daily.csv`: one row per city per day (AQI, PM2.5, PM10, Fire_Count, Total_FRP, Season, Fire_Count_Lag4)
- `fire_map_grid.csv`: fires aggregated to 0.1 degree grid cells by year
- `dashboard.png`: screenshot of the final dashboard

## Key findings
- Delhi's average AQI was about 269 on low-fire days (under 500 detections) and about 453 on extreme-fire days (over 3,000).
- Bengaluru, far from the fire region, stayed flat at an AQI of about 95-102 across fire levels.
- Fire detections peaked on 7 Nov 2016 (8,131), the same day Delhi recorded its highest AQI in the dataset (716).
- Delhi's AQI correlates most strongly with fire counts from 4-5 days earlier (r of about 0.5).

## Limitations
- This shows association, not proof of cause. Winter weather and Diwali fireworks also raise Oct-Nov pollution.
- The fire data covers Oct-Nov only. The AQI data ends in July 2020, so 2020 is not covered.
- Chandigarh has only one season of data (from Sep 2019) and Amritsar starts in Feb 2017. Ludhiana is not in the dataset.
- Satellite passes see each location only a few times a day, so counts are detections, not exact numbers of fires.
- The state boundary is approximate, so counts near borders are rough.

## Tools
Tableau Public, Python (pandas) for preprocessing.

## Acknowledgements
NASA FIRMS (EOSDIS), Central Pollution Control Board, and Rohan Rao for the Kaggle dataset.

## Author
**Shreya Mishra**
B.E. Computer Science and Engineering (AI & ML), Chandigarh University

Project created as part of the Business Intelligence Tools course assessment.

Connect with me on LinkedIn: [add your profile link]