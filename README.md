# Supply_Chain_Greenhouse_Gas_Emission-
this is my 9th project with Quantum Analytics

## Table of Contents

- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Recommendations](#recommendations)

### Project Overview
---

**Project Overview: Supply Chain Greenhouse Gas Emissions Analysis**  

This project focuses on analyzing the greenhouse gas (GHG) emissions associated with various sectors of the economy, measured in terms of CO2 equivalent per monetary unit spent (2021 USD). By examining both direct emissions and those from supply chain margins, this dataset provides critical insights into the environmental impact of economic activities across different industries. The analysis aims to support sustainability efforts, inform policy formulation, and assist in the development of strategies to reduce the carbon footprint of economic operations.  

### Objectives:  
1. **Carbon Footprint Assessment**: Evaluate the greenhouse gas emissions associated with different sectors of the economy.  
2. **Direct vs. Supply Chain Emissions**: Investigate the contribution of direct emissions versus emissions generated through supply chain activities.  
3. **Industry-Specific Insights**: Identify high-emission sectors and explore potential areas for reducing their carbon footprint.  
4. **Sustainability Strategies**: Develop strategies to reduce emissions in industries with the highest environmental impact.  
5. **Lifecycle Assessment**: Conduct lifecycle assessments to understand the environmental impact of products and services across their entire supply chains.  
6. **Policy and Investment Recommendations**: Provide insights that can guide policymakers and investors in promoting low-carbon economic activities.

### Key Areas of Analysis:  
1. **Sector Emission Analysis**:  
   - Examine the GHG emissions by sector, focusing on industries with the highest emissions per unit of monetary spending.  
   - Compare emissions from various sectors (e.g., manufacturing, agriculture, energy) to identify the most carbon-intensive industries.  

2. **Supply Chain Margins**:  
   - Assess how supply chain margins contribute to overall emissions, helping businesses understand the full environmental impact of their operations.  
   - Identify supply chains that generate significant emissions, offering opportunities for intervention.  

3. **Carbon Footprint Modeling**:  
   - Build models to predict the environmental impact of future economic activities based on current spending patterns.  
   - Explore how changes in supply chain practices, sourcing, and logistics can reduce emissions.  

4. **Policy Implications**:  
   - Provide insights to help policymakers create regulations that encourage low-carbon practices across industries.  
   - Identify key sectors where governmental incentives or regulations could drive substantial emissions reductions.  

5. **Sustainable Investment Opportunities**:  
   - Recommend industries or sectors that are poised for low-carbon transformation and represent sustainable investment opportunities.  
   - Analyze the potential financial impact of reducing emissions within various industries.  

### Potential Use Cases:  
1. **Environmental Impact Assessment**: Conduct detailed assessments of the environmental impact of various economic activities to guide corporate social responsibility (CSR) strategies.  
2. **Sustainability Reporting**: Help organizations report their carbon footprint in compliance with sustainability frameworks such as GRI (Global Reporting Initiative) or CDP (Carbon Disclosure Project).  
3. **Green Supply Chain Optimization**: Suggest best practices for creating more sustainable supply chains with reduced carbon emissions.  
4. **Policy Development**: Provide evidence-based recommendations to assist governments in creating policies aimed at reducing national and global carbon footprints.  
5. **Investment Strategy Development**: Guide investment decisions in companies and sectors with a focus on sustainability and carbon reduction initiatives.  

By leveraging this dataset, the project will offer valuable insights into how industries can mitigate their environmental impact, enabling more sustainable business practices and policies.

![Dashboard]![9 Supply Chain Greenhouse Gas Emission ](https://github.com/user-attachments/assets/df27e03e-11ac-4bae-a906-c3b4757bcc60)



### Data Sources

SupplyChain GHG Emission Factors dataset: The primary dataset used for this analysis is the "SupplyChainGHGEmissionFactors-v1-2-NAICS-CO2e-USD2021-csv" file, containing detailed information about SupplyChain GHG Emission Factors.

### Tools

- Excel - Data Cleaning
  - [Download here](https://microsoft.com)
- SQL Server - Data Analysis
- PowerBI - Creating reports


### Data Cleaning/Preparation

In the initial data preparation phase, we performed the following tasks:
1. Data loading and inspection.
2. Handling missing values.
3. Data cleaning and formatting.

### Exploratory Data Analysis

EDA involved exploring the sales data to answer key questions, such as:

- What is the overall sales trend?
- Which products are top sellers?
- What are the peak sales periods?

### Data Analysis

Include some interesting code/features worked with

**Industries with the Highest Emissions**
```sql
SELECT 
    `2017 NAICS Code`, 
    `2017 NAICS Title`, 
    MAX(`Supply Chain Emission Factors with Margins`) AS Max_Emission_Factor
FROM 
    emissions_data
GROUP BY 
    `2017 NAICS Code`, `2017 NAICS Title`
ORDER BY 
    Max_Emission_Factor DESC
LIMIT 10;  -- Adjust the limit as needed
```

**Comparison of Emission Intensities**
```sql
SELECT 
    `2017 NAICS Code`, 
    `2017 NAICS Title`, 
    AVG(`Supply Chain Emission Factors with Margins`) AS Avg_Emission_Intensity
FROM 
    emissions_data
GROUP BY 
    `2017 NAICS Code`, `2017 NAICS Title`
ORDER BY 
    Avg_Emission_Intensity DESC;
```

**Impact of Margins**
```sql
SELECT 
    `2017 NAICS Code`, 
    `2017 NAICS Title`, 
    AVG(`Margins of Supply Chain Emission Factors`) AS Avg_Margin_Impact,
    AVG(`Supply Chain Emission Factors with Margins`) - AVG(`Supply Chain Emission Factors without Margins`) AS Margin_Impact
FROM 
    emissions_data
GROUP BY 
    `2017 NAICS Code`, `2017 NAICS Title`;
```

**Efficiency Analysis**
```sql
SELECT 
    `2017 NAICS Code`, 
    `2017 NAICS Title`, 
    AVG(`Supply Chain Emission Factors with Margins`) / AVG(`Supply Chain Emission Factors without Margins`) AS Efficiency_Ratio
FROM 
    emissions_data
GROUP BY 
    `2017 NAICS Code`, `2017 NAICS Title`;
```

**Sectoral Contributions**
```sql
SELECT 
    `2017 NAICS Title`, 
    SUM(`Supply Chain Emission Factors with Margins`) AS Total_Emissions,
    SUM(`Supply Chain Emission Factors with Margins`) / (SELECT SUM(`Supply Chain Emission Factors with Margins`) FROM emissions_data) * 100 AS Supply_Chain_Contribution_Percent
FROM 
    emissions_data
GROUP BY 
    `2017 NAICS Title`;
```

**Total Industry Emissions**
```sql
SELECT 
    SUM(`Supply Chain Emission Factors with Margins`) AS Total_Industry_Emissions
FROM 
    emissions_data;
```

**Max Emission Factor**
```sql
SELECT 
    MAX(`Supply Chain Emission Factors with Margins`) AS Max_Emission_Factor
FROM 
    emissions_data;
```

**Margin Impact**
```sql
SELECT 
    AVG(`Margins of Supply Chain Emission Factors`) AS Avg_Margin_Impact
FROM 
    emissions_data;
```

**Median Emission Intensity**
```sql
SELECT 
    PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY `Supply Chain Emission Factors with Margins`) AS Median_Emission_Intensity
FROM 
    emissions_data;
```

### Results/Findings

The analysis results are summarized as follows:

**Industries with the Highest Emissions:**

The analysis revealed that certain industries, such as Agriculture, Manufacturing, and Transportation, have the highest emissions based on the maximum emission factors.

**Comparison of Emission Intensities:**

Industries exhibited varying average emission intensities, with some sectors, like Energy Production, showing significantly higher values than others, indicating a need for targeted interventions.

**Impact of Margins:**

The average margin impact analysis indicated that industries with higher margins tend to have a more substantial difference between emissions with and without margins, suggesting that profit margins influence emission factors.

**Efficiency Analysis:**

The efficiency ratio showed that some industries are operating with better emission efficiencies than others, highlighting potential areas for improvement.

**Sectoral Contributions:**

The sectoral contributions analysis indicated that Agriculture and Manufacturing are the largest contributors to total emissions, accounting for a significant percentage of overall emissions.

**Total Industry Emissions:**

The total emissions across all industries were quantified, providing a baseline for future comparisons and tracking progress over time.

**Max Emission Factor:**

The maximum emission factor identified was significantly high, pinpointing industries that may require immediate regulatory scrutiny or intervention.

**Margin Impact:**

The average margin impact indicated that higher margins correlate with higher emissions, suggesting that profit-driven practices may not align with sustainability goals.

**Median Emission Intensity:**

The median emission intensity provided insights into the central tendency of emissions across industries, which can help identify outliers and industries needing attention.

### Recommendations

Based on the analysis, we recommend the following actions:

**Targeted Policy Interventions:**

Implement stricter regulations and incentives for industries with the highest emissions, particularly in agriculture and manufacturing.

**Efficiency Improvement Programs:**

Encourage industries to adopt cleaner technologies and practices through grants or subsidies that promote energy efficiency and lower emissions.

**Margin Analysis:**

Conduct further analysis to understand how profit margins affect emissions and develop strategies to align financial and environmental goals.

**Public Awareness Campaigns:**

Launch campaigns to raise awareness about the environmental impacts of high-emission industries, encouraging consumer choices that favor sustainable practices.

**Regular Monitoring and Reporting:**

Establish a framework for ongoing monitoring of emissions across industries to track progress and adapt strategies as necessary.

**Collaboration with Industry Stakeholders:**

Foster partnerships with industry leaders to share best practices and develop joint initiatives aimed at reducing emissions.

### Limitations

**Data Quality and Completeness:**

The findings are contingent on the accuracy and completeness of the data provided. Missing or inaccurate data could skew results.

**Generalization of Findings:**

The analysis is based on aggregated data, which may overlook specific nuances within sub-sectors or regional variations.

**Temporal Limitations:**

Emission factors and industry practices can change over time, and the analysis reflects a snapshot that may not account for future developments or trends.

**External Factors:**

Economic conditions, regulatory changes, and technological advancements can significantly impact emissions but may not be captured in the current analysis.

**Assumptions in Calculations:**

Some calculations, such as median and average emission intensities, rely on statistical assumptions that may not fully represent the underlying data distribution.

**Lack of Contextual Factors:**

The analysis does not account for external factors influencing emissions, such as supply chain logistics, consumer behavior, and geographic considerations.

This structured approach provides a comprehensive overview of the findings, actionable recommendations, and a clear understanding of the limitations associated with the analysis of emissions data.

### References

`column_1`

**bold**

*italic*
