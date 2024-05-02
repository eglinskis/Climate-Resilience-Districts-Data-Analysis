# ClimateResilienceDistricts_Analysis
This github page contains my Capstone Analysis for the UC Berkeley Master's in City Planning Program as supported by the Urban Informatics Spring '24 Course.

## Topic Summary

My Master's thesis is looking at the distributional impact of flood risk related to financial . I am including a case study in San Mateo County that looks at the following data sources:

1. **Parcel Data:** desired attributes = assessed value, lot size, building area. <br>*Source:* ParcelAtlas, 2021 data, proprietary but made available through UC Berkeley GIS Librarian. <br>*Format:* shapefile.


2. **Annual Avoided Losses (AAL):** Expected annual structure and contents damage from coastal flooding, aggregated over and averaged across 2020–2060, utilizing the values for RCP Scenario 8.5. <br>*Source:* Bick et al. (2021). Rising seas, rising inequity? Communities at risk in the San Francisco Bay Area and implications for adaptation policy. Earth's Future, 9, e2020EF001963 [link.](https://doi-org.libproxy.berkeley.edu/10.1029/2020EF001963) <br>*Format:* CSV, needs to be joined to building footprint data to be spatialized and merged with parcel dataset. 


3. **Community Vulnerability Data:** The San Francisco Bay Conservation and Development Commission Adapting to Rising Tides Program developed a dataset to better understand community vulnerability to current and future flooding due to sea level rise and storm surges. Data is sources from ACS and CalEnviroScreen and is at the census block group level. <br>*Source:* 2023 Community Vulnerability Data from San Francisco Bay Conservation & Development Commission (BCDC). <br>*Format:* shapefile. 


4. **ABAG Flood Protection Project Costs Data:** Sea Level Rise Adaptation Funding and Investment Framework Shoreline Project Inventory, published in 2023. <br>*Source:* Association of Bay Area Government (ABAG). <br>*Format:* Project Costs by County, including San Mateo County, as a xlsx workbook [here]('https://mtc.ca.gov/digital-library/5024319-sea-level-rise-adaptation-funding-and-investment-framework-shoreline-project-inventory'). Project Inventory and Placeholders shapefile sent directly by email from  ABAG staff. 

My research analysis design utilzing these datasets hopes to answer the following questions:

1. What could a special financing district for flood protection look like in San Mateo County?
<br>
<br>
2.  How much revenue would it raise, given design defensible assumptions for a (1) Special Assessment District and (2) a Mello-Roos District? Is it enough to fill the present flood protection costing gap for this region?  
<br>
<br>
3.  What is the distributional impact of raising such a levy to locally finance future climate resilient infrastructure? What could this imply for considerations of equity in the design of the financing district (exemptions, abatements, etc)? 
