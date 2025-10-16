# NBER-CES Manufacturing Industry Database

## Introduction
This database is a joint effort between the National Bureau of Economic Research (NBER) and U.S. Census Bureau's Center for Economic Studies (CES), containing annual industry-level data from 1958-2018 on output, employment, payroll and other input costs, investment, capital stocks, TFP, and various industry-specific price indexes (see https://www.nber.org/research/data/nber-ces-manufacturing-industry-database)

The NBER-CES Manufacturing Industry Database contains annual data from the United States manufacturing sector for the period from 1958 to 2018. The data used for the development of the database come from various sources, but chiefly from three government agencies: the U.S. Census Bureau, the Bureau of Economic Analysis (BEA), and the Bureau of Labor Statistics (BLS). The goal is to provide a long time-series of data for a large number of industries, adjusting for changes in industry definitions, and creating price deflators and capital stocks.

## Data and Sources

### ASM/Census (emp, pay, prode, prodh, prodw, vship, matcost, vadd, invest, invent, energy)
The majority of the variables provided in the database are taken from the Census Bureau’s Annual Survey of Manufactures (ASM). The ASM includes about 50,000 establishments selected from the approximately 300,000 establishments included in the Census of Manufactures (CMF). The ASM is conducted annually, except for years ending in 2 and 7, when it is part of the CMF.

The variables defined in the dataset are:

- North American Industrial Classification System (NAICS) 2012 6-digit industry (naics)
- NAICS industry Class (naics_title)
- Year ranges from 1958 to 2018 (year) 
- Total employment in 1000s (emp)
- Total payroll in $1m (pay)
- Production workers in 1000s (prode)
- Production worker hours in 1m (prodh)
- Production worker wages in $1m (prodw)
- Total value of shipments in $1m (vship)
- Total cost of materials in $1m (matcost)
- Total value added in $1m (vadd)
- Total capital expenditure in $1m (invest)
- End-of-year inventories in $1m (invent)
- Cost of electricity & fuels in $1m (energy)
- Total real capital stock in $1m (cap)
- Real capital: equipment in $1m (equip)
- Real capital: structures in $1m (plant)
- Deflator for VSHIP 2012=1.000 (piship)
- Deflator for MATCOST 2012=1.000 (pimat)
- Deflator for INVEST 2012=1.000 (piinvest)
- Deflator for ENERGY 2012=1.000 (pien)
- 5-factor TFP annual growth rate (dtfp5)
- 5-factor TFP index 2012=1.000 (tfp5)
- 4-factor TFP annual growth rate (dtfp4)
- 4-factor TFP index 2012=1.000 (tfp4)

Variables are denominated in millions of nominal dollars, except for labor variables that are denominated in thousands of workers or millions of worker hours. To convert nominal dollars to real (“fixed-base”) dollars and calculate productivity factors, four different deflators are used. These are discussed in the following sections. More detailed explanations of these variables can be found in the appendixes of various CMF publications, including the General Summary of the 1997 Economic Census Manufacturing Subject Series.

### Industry Capital Stocks and the Investment Deflator (piinv, plant, equip, cap)
The FRB data are used to calculate separate depreciation rates for equipment and structures for each industry, backing the depreciation numbers out of a standard perpetual inventory equation:

<a href="https://www.codecogs.com/eqnedit.php?latex=K_t=(1-d_{t-1})K_{t-1}&plus;I_t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?K_t=(1-d_{t-1})K_{t-1}&plus;I_t" title="K_t=(1-d_{t-1})K_{t-1}+I_t" /></a>

In this equation, d is the rate of depreciation, which we derive based on the FRB data for K, the real capital stock in years t and t-1, and I, the real capital investment in year t.

To calculate the investment deflator (piinv), separate price indexes for equipment and structures are computed from the ratio of nominal to real investment for the NAICS industries in the FRB data. The final investment deflator values in our dataset are created as the weighted mean of the deflators for equipment and structures. The shares used for the weights are averaged over years t and t-1:

<a href="https://www.codecogs.com/eqnedit.php?latex=\Delta&space;P_t=\sum_{n=1}^{2}[\frac{1}{2}(S_{n,t}&plus;S_{n,t-1})\Delta&space;P_{n,t}&space;]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Delta&space;P_t=\sum_{n=1}^{2}[\frac{1}{2}(S_{n,t}&plus;S_{n,t-1})\Delta&space;P_{n,t}&space;]" title="\Delta P_t=\sum_{n=1}^{2}[\frac{1}{2}(S_{n,t}+S_{n,t-1})\Delta P_{n,t} ]" /></a>

In this equation, <a href="https://www.codecogs.com/eqnedit.php?latex=\Delta&space;P" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Delta&space;P" title="\Delta P" /></a> is the annual growth in the price level of investment overall, S is the share of total capital investment for each category, and the summation occurs over n=2 categories (equipment and structures). Note that the data on investment shares comes from the ASM/CMF data, while the investment deflators come from the FRB data. We apply the price growth to the existing 2011 piinv value to grow values from 2012-2016, with the resulting series normalized to be 1 in 2012.

### The Shipments Deflator (piship)
In past years, the price indexes used in the calculation of the shipments deflator came from the BEA GDP-by-Industry data, found at www.bea.gov under the “Industry” tab. However, these detailed deflators are no longer available after 2011, so we switch to using producer price data from BLS at https://www.bls.gov/ppi/data.htm, specifically the average price over the year. This provides 6-digit NAICS prices based on the 2012 NAICS definitions through 2018. We calculate annual growth rates in prices for each industry and use them to grow the 2011 piship value forward to 2018. The series is then normalized to have a value of 1 in 2012. A few industries do not have a BLS deflator available; we use the closest fit we could find, either from a broader industry group or from a similar industry.

### The Materials Cost Deflator (pimat)
The materials cost deflators are calculated using data from the benchmark “use-make” (input-output) tables and the GDP-by-Industry data of the BEA. The raw data are available at the BEA website (https://www.bea.gov/data/industries/input-output-accounts-data). The detailed input-output tables are provided every 5 years, for years corresponding to the Economic Census (ending in 2 and 7). The most recent detailed table is used until the next one is issued, so the 2007 table provides the numbers for calculations between 2007 and 2011, shifting to the 2012 table for calculations starting with the 2012 data.

The price deflators for each input coming from the BEA integrated industry accounts, specifically the chain-type price index for gross output by industry detail (https://www.bea.gov/data/industries/gross-output-by-industry). These prices match the industry codes used in the input-output tables.

### Energy Usage Data and the Energy Deflator (pien)
The energy deflator is based on each industry's expenditures on seven types of energy: electricity,residual fuel oil, light oils, liquefied petroleum, coal, coke, and natural gas. 

The expenditure data for six of the fuels in the current update (excluding electricity) come from the Manufacturing Energy Consumption Survey (MECS), available at the U.S. Energy Information Administration website (www.eia.gov/consumption/manufacturing/index.cfm). MECS provides energy consumption in trillions of British thermal units (BTUs) and the average price per million BTUs for each energy type. The MECS data (price × quantity) are used to calculate the share of total energy spending allocated to each energy type. Meanwhile, the ASM data provides information on electricity and non-electricity energy spending. The MECS data are used to disaggregate the non-electricity spending into the six other fuels. The MECS survey is done every 4 years, and the values from that year are used for the subsequent 3 years until the next version appears. Currently the 2014 MECS is being used for calculations in 2014 through 2018; when the 2018 MECS becomes available it will be used for calculations in 2018 through 2021 (so the current numbers for 2018 will be revised then).

There are a number of missing values in the MECS data. Extremely small values (less than 0.5), as well as values with high relative standard error (more than 50%) are not published. Additionally, some values are withheld to avoid disclosing information for individual establishments in cases where an industry has relatively few plants. Extremely small values are replaced by 0.1, consistent with the approach taken in previous updates. Since MECS reports totals by industry and type of energy, we can impute most remaining missing values by running a cross-check against the unassigned residuals from those totals. In other cases, the missing data is extrapolated using the MECS data from the previous year.

Price indexes for each energy type are obtained from BLS producer prices (www.bls.gov/ppi): wpu051 coal (also used for coke), wpu0532 liquefied petroleum gas, wpu054321 industrial electric power, wpu055321 industrial natural gas, wpu0573 light fuel oils, wpu0574 residual fuel oils. Electricity prices are calculated from electricity consumption and expenditures data in the ASM tables.

The annual growth in aggregate energy prices is calculated as the weighted mean of the price changes for the seven different types of energy, following the structure of the second equation. The annual energy price growth numbers for 2012-2018 are then applied to the existing 2011 pien value to extend the price index through 2018, which is then normalized to 1 in 2012.
