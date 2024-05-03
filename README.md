# Climate Resilience Districts: Data Analysis
This github page contains my Capstone Analysis for the UC Berkeley Master's in City Planning Program as supported by the Urban Informatics Spring '24 Course.

Research Summary
----------------

By 2100, our shorelines will undergo an unprecedented scale of transformation due to sea-level rise (SLR), but it remains to be seen who will foot the bill for future adaptation. My Master's thesis examines the potential distributional impacts of deploying local financing strategies for coastal protection infrastructure. In 2022, state bill [SB 852](https://legiscan.com/CA/text/SB852/id/2606300)  "Climate Resilience Districts: Formation: Funding Mechanisms" was passed authorizing a city, county, special district, or a combination of those entities to form a special financing district (Climate Resilience District, CRD) to raise and allocate money towards the construction and operation of projects that address climate change -- which can consist of shoreline armoring  through gray infrastructure (seawalls, levees, bulkheads, retaining walls) or "nature-based solutions" like living shorelines, ecological breakwaters, constructed wetlands, beach nourishment, or a combination of all approaches. Across the state, a suite of tools (often called "land value capture") are now available to local governments to raise local funds for infrastructure, from levying an special assessment, Mello-Roos special tax, property-related fee, sales tax, and/or a tax-increment financing (TIF).

While no local jurisdiction has yet to form a CRD in California, costing gaps are becoming clear in key coastal geographies such as the Bay Area. In July 2023, BCDC teamed up with Metropolitan Transportation Commission (MTC) / Association of Bay Area Governments (ABAG) to create the [first ever inventory](https://mtc.maps.arcgis.com/apps/webappviewer/index.html?id=4cfbec7006d542a5913a46ec15d7cd24) of planned and constructed flood protection infrastructure in the Bay, highlighting gaps in flood protection where no plans exist to expose site-specific vulnerabilities. Importantly, the coalition also produced high-level costing estimates to calculate how much financing would be necessary to protect the Bay area from rising seas and floods by 2050. In this groundbreaking report, they put forth an estimated price-tag of $110 billion--only $5 billion of which could be accounted for by existing federal, state, regional, and local funding programs, leaving a gap of approximately $105 billion USD to fill in the next few decades. While this pricetag is daunting, the report concludes that failing to make these resilience investments would cost the region two-fold in damages.

In response to these issues, this research analysis hopes to answer the following questions:

1.  What could a special financing district for flood protection look like in San Mateo County?

2.  What is the distributional impact of raising such a levy to locally finance future climate resilient infrastructure? 

3.  What could this imply for considerations of equity in the design of the financing district (exemptions, abatements, etc)?

The county of San Mateo has approximately 738,000 residents and is made up of 27 jurisdictions and unincorporated areas. [According to the ABAG/BCDC](https://mtc.ca.gov/sites/default/files/documents/2023-07/SLR_Framework_Final_Report.pdf), San Mateo county makes up the largest share (almost 25%, or 21.7 B USD) of Bay Area-wide flood protection costs, as well as over 50% of the total assessed value at risk of inundation (4.9 ft SLR). An estimated 55,000 San Mateo households are expected to experience major flood exposure by 2050 as the county has more people and property value from SLR than any other county in the state. As such, it is often referred to as the "ground zero" for SLR vulnerability.

[[INSERT VIZ??]] SMC with slider?

-   Infrastructure slide with attributes

-   4 snapshots of SLR (bay only)

-   Zoom into san mateo county 

Key Datasets
------------

1.  San Mateo County Tax Parcel Data: desired attributes are assessed value, lot size, building area.\
    Source: ParcelAtlas, 2021 data, proprietary but made available through UC Berkeley GIS Librarian.\
    Format: shapefile.

2.  Annual Avoided Losses (AAL): Expected annual structure and contents damage at the building from coastal flooding, aggregated over and averaged across 2020--2060, utilizing the values for RCP Scenario 8.5.\
    Source: Bick et al. (2021). Rising seas, rising inequity? Communities at risk in the San Francisco Bay Area and implications for adaptation policy. Earth's Future, 9, e2020EF001963 [link.\
    ](https://doi-org.libproxy.berkeley.edu/10.1029/2020EF001963)Format: CSV, needs to be joined to building footprint data to be spatialized and merged with parcel dataset.

3.  Community Vulnerability Data: The San Francisco Bay Conservation and Development Commission Adapting to Rising Tides Program developed a dataset to better understand community vulnerability to current and future flooding due to sea level rise and storm surges. Data is sources from ACS and CalEnviroScreen and is at the census block group level.\
    Source: 2023 Community Vulnerability Data from San Francisco Bay Conservation & Development Commission (BCDC). [link.](https://gis.data.cnra.ca.gov/datasets/BCDC::community-vulnerability-bcdc-2023/about)\
    Format: shapefile.

4.  ABAG Flood Protection Project Costs Data: Sea Level Rise Adaptation Funding and Investment Framework Shoreline Project Inventory, published in 2023.\
    Source: Association of Bay Area Government (ABAG).\
    Format: Project Costs by County, including San Mateo County, as a xlsx workbook [here](https://mtc.ca.gov/digital-library/5024319-sea-level-rise-adaptation-funding-and-investment-framework-shoreline-project-inventory). Project Inventory and Placeholders shapefile sent directly by email from ABAG staff.

Methodology
-----------

The case study focuses on 53 projects along the majority of the eastern bay-facing shoreline of San Mateo county. The state of projects and their specific funding status varies by shoreline segment in the study area. Costs within this study site total to around 13.9 billion USD, less than 5% of which have been completed or are in construction, leaving around $12.9 billion USD in project costs that will form the baseline revenue goal for the example financing district.

Special assessments related to resilience infrastructure calculate direct proportional benefit for rate-setting through the concept of annual avoided losses (AAL), which is a common metric used in cost-benefit analyses for flood protection projects. They are often quantified in terms of monetary value based on damages to the structure and contents of individual properties anchored to annualized flood probabilities. Assumptions for rate design and apportionment were loosely modeled off of the Sacramento Area Flood Control Agency (SAFCA) Assessment Engineering Report for the  [Consolidated Capital Assessment District No. 2 (CCAD#2](https://www.safca.org/assessments/assessment-districts/)), which was approved by voters in June 2016 to provide capital assessments to fund flood control improvements.

Next, the annual project costs are divided by the total benefit (summed AAL values for the whole district) to get an absolute assessment rate. Assessments are separated out by land use type and divided by the total building square foot or acres of land (depending on if use type building-to-land ratio is > or < 0.05%) to get an assessment amount (USD$) per square foot or acre. Assessment rates were applied to parcel data and grouped at the census block scale by land use type. It is important to note that this financial model assumes all required project costs will be met.

In order to assess key questions about distributional impacts of financing strategies on households, two statistical modeling techniques were explored: Ordinary Least Squares (OLS) regression and K-means Unsupervised Clustering. Explanatory variables were extracted from the BCDC Community Vulnerability dataset and included socio-demographic features like race, income, age, and housing ownership status (see below for full list of eight model variables). The outcome variable is defined as the percentage of financial contribution by block group for the full annual assessment levied on residential parcels (other land use types were not included here, since I am interested in fiscal impacts to resident households). In both models all variables were standardized, and 98 total observations included (number of block groups in the CRD). For the K-means approach, the elbow method was applied to determine an optimal value of 3 clusters. Classification was performed in order to determine distinct socio-demographic clusters across geographical space within the example CRD. 

*Model Input Variables from 2023 BCDC Community Vulnerability Dataset.*

![](https://lh7-us.googleusercontent.com/9ZvvSjWWY5-CMeD0Fh8akHUp9rpd9TZBTlA3yIcYb_NgrEfedKJE71ySep0aKzaocYlRKFEg3pbaCheh6P0hlEO3g8BAVBP1M5F53ogglzn1cYEi2MQbiXI0ccDTvtKnLlyzAdC9Yq2LzXSL79WLUY4)


Results
-------

### **Which Land Use Types are Assessed the Most?**
![](https://lh7-us.googleusercontent.com/WZlzibHlBc2wOwQ1VLuz5ifU7VuZIiQwnTzMBqAJAYYc2VbyrojO_vGC2pi7q9S6JrNPWwuEAMR4CqKNvaumoUU6unefzuEUqnfaHm47LPD1gjOCyLIBnHMqizH1MnXaZLiUqPq1NOUnvASiryUeLHM)

*Left shows the percentage of total annual assessment contributed by the census block group, with the majority land use type reflected on the right. Below shows the percentage breakdown of the annual assessment share based on parcel land use type.*

There are select census blocks with non-Residential ownership that bear a high percentage of costs according to the benefits received -- notably for SFO, which is technically owned by the City of San Francisco (public ownership) and would contribute $2 M annually, or 5% of the assessment. Importantly however, residential parcels would pay 48% of the annual special assessment for San Mateo flood protection ($23 Million). Thus the burden of which types of households contribute these costs becomes more apparent.

### **What Household Typologies are Assessed the Most?**

The OLS regression examines how socio-demographic characteristics correlate with the total cost share for residential assessments. The model produced an R-squared of 0.7 and train/test RMSEs of 0.82 and 0.97 respectively. Both the training and test RMSE values are lower than the standard deviation of the outcome variable (1.00), suggesting that this model is performing fairly well but may slightly overfit the data due to the higher test error.

Overall, the resulting model had relevant results for the proposed CRD in San Mateo County. First, demographically homogeneous neighborhoods (60% or more of one demographic group) are likely to bear a higher share of the residential assessment. Additionally, block groups with higher percentages of owners are likely to bear a higher share of the residential assessment compared to majority renter block groups. This strong correlation suggests costs will be passed down more directly to individual homeowners than landlords. Importantly, from an equity perspective, elderly and low-income households are less likely to bear a higher share of the residential assessment.

![](https://lh7-us.googleusercontent.com/rjWNKVHXHe6sl2e_oc_TZ2Hi_A0MCBv2PYRSSHHd09Lr6jniW7YU56f9lKHCG_JHYhWZNDZrl13PnehZw1EkPnmeSUheBiAiikp880JGkmVfQmfdSKFJiMlvNruEeEhBa-tdHRjuRA4HXx0sWfRmLLg)

*Coefficient values of standardized features from the OLS regression model assessing factors correlated with total cost share for annual residential assessments in the San Mateo CRD.*

The k-means classification method produced distinct geographically-distributed classes of neighborhood characteristics in relation to assessment burden. Below I  map the three distinct classes produced, along with key identifying features for each class. For example, jurisdictions such as East Palo Alto encompass class 1, where there are high proportions of Black and Latinx communities, high proportions of financial instability, and medium levels of homeownership. In contrast, cities like Foster City have higher dominance from Class 3, which exhibits higher Asian dominant households, the lowest financial instability and housing cost burdens, and the highest percentages of homeowners. San Mateo city is more mixed in terms of classes. 

![](https://lh7-us.googleusercontent.com/CRlUFQO5X7Mn8YWODKieOURk4__cLpPqShvDJeyD9JbRlfNObsfSJl4Iw6-xA7ywD-oXxpT0o45y16mRPXtlMwKJcrK-4HcGKh4hH1_rvooeddbuniFlqqKBmLe4ZH6iLoZCI1SXNrIjEp7XeEZGS_s)

*K-means classification of socioeconomic clusters in the San Mateo shoreline CRD with associated attributes and characteristics.*

From an equity and policy design perspective it is critical to zero in a household's ability to pay  additional assessments on their property on an annual basis. Financial stability was calculated at the census block group level by classifying households that have zero or negative discretionary income after accounting for the high Bay Area cost of living, signifying a minimal ability to pay for additional expenses. As referenced in [Bick et al, 2021](https://agupubs-onlinelibrary-wiley-com.libproxy.berkeley.edu/doi/full/10.1029/2020EF001963#), consumer prices are multiplied by a regional price parity of 1.3 to account for increased cost of goods and services in San Mateo relative to the U.S. at-large.  Generally, income brackets below $75,000-100,000 show negative discretionary incomes.

Zooming into financial instability by demographic majority group, in the next plot, we see distinct relationships: Asian majority block groups are the most financially stable, and face higher contributions to the special assessment. Hispanic households show higher rates of financial instability but bear less of the overall cost burden. It is clear from this analysis that financially insecure households are thus less likely to disproportionately bear the burden of special assessments levied for resilience infrastructure financing in this proposed Climate Resilience District. 

![](https://lh7-us.googleusercontent.com/8_zODi4y59IBXJ7U4NfHEvtkqDOK972ZGGOnCGNHmJc1olsUGTzI4GezY8vaCl2PyCacRfxSpeFg0LTdBH7bxWdcFurnDNlyfK5VjlXOElGNn3_fKrbWjtlM4JaTThpZKSVzy6t6e7iHlFwAH5640aA)

*Linear regression showing that the higher percentage of households classified as financially unstable, the lower the contribution to the annual assessment.* 

Conclusion
----------

This analysis has examined potential policy design tools to create scalable adaptation financing strategies and minimize distributional impact to historically disinvested households. While the analysis in San Mateo shows that financially insecure and socially vulnerable households are less likely to disproportionately bear the burden of assessments levied for resilience infrastructure financing, it is critical to underscore that the absolute value of the assessment on a cost-constrained household may still be burdensome. In other words, even if financially insecure households are on average paying less than households with large discretionary incomes, that value may still be more than these households can bear. Thus, abatements and exemptions are a powerful policy design tool that should complement any proposed Climate Resilience District. Additionally, unexplored opportunities could include utilizing new local financing strategies to allocate for in parallel anti-displacement work, such as affordable housing development, land acquisition and rehabilitation, and other community programs.

References
----------


Assessment Districts. (n.d.). SAFCA - Sacramento Area Flood Control Agency. Retrieved April 28, 2024, from <https://www.safca.org/assessments/assessment-districts/>
Bick, I. A., Santiago Tate, A. F., Serafin, K. A., Miltenberger, A., Anyansi, I., Evans, M., et al. (2021). Rising seas, rising inequity? Communities at risk in the San Francisco Bay Area and implications for adaptation policy. Earth's Future, 9, e2020EF001963. <https://doi-org.libproxy.berkeley.edu/10.1029/2020EF001963>
Metropolitan Transportation Commission / Association of Bay Area Governments and the San Francisco Bay Conservation and Development Commission. Sea Level Rise Adaptation Funding and Investment Framework Technical Methodology Report (2023, July). Retrieved April 2024, from <https://mtc.ca.gov/sites/default/files/documents/2023-07/SLR_Framework_Technical_Methodology_Report_0.pdf>
San Francisco Bay Conservation and Development Commission. (2023). Community Vulnerability Data User Guide -- 2023 Update. Retrieved April 2024, from <https://www.adaptingtorisingtides.org/wp-content/uploads/2024/01/CommunityVulnerability_Data_UserGuide_BCDC_2023_Final.pdf>

