# ✈️FlightRank 2025: Aeroclub RecSys Cup
**Personalized Flight Recommendations for Business Travelers**

A data-driven journey into flight recommendation systems. Presented by Aeroclub for the RecSys Cup 2025, this visual blends aviation with algorithmic precision—featuring a stylized aircraft built from numerical data points, set against a sleek grid backdrop. Innovation takes flight

![FlightRank Header](https://github.com/Ishita95-harvad/flightrank-2025-aeroclub-recsys-cup/blob/main/header.jpg)

***

**Dataset Description**
Data Description
**Overview**
This dataset contains flight booking options for business travelers along with user preferences and company policies. The task is to predict user flight selection preferences.

**Data Structure**
The dataset is organized around flight search sessions, where each session (identified by ranker_id) contains multiple flight options that users can choose from.

**Main Data**

'train.parquet' - train data
'test.parquet' - test data
'sample_submission.parquet' - submission example
JSONs Raw Additional Data

'jsons_raw.tar.kaggle'* - Archived raw data in JSONs files (150K files, ~50gb). To use the file as a regular .gz archive you should manually change extension to '.gz'. Example jsons_raw.tar.kaggle -> jsons_raw.tar.gz
'jsons_structure.md' - JSONs raw data structure description
**Column Descriptions**
Identifiers and Metadata
Id - Unique identifier for each flight option
ranker_id - Group identifier for each search session (key grouping variable for ranking)
profileId - User identifier
companyID - Company identifier
**User Information**
sex - User gender
nationality - User nationality/citizenship
frequentFlyer - Frequent flyer program status
isVip - VIP status indicator
bySelf - Whether user books flights independently
isAccess3D - Binary marker for internal feature
**Company Information**
corporateTariffCode - Corporate tariff code for business travel policies
Search and Route Information
searchRoute - Flight route: single direction without "/" or round trip with "/"
requestDate - Date and time when search was performed
**Pricing Information**
totalPrice - Total ticket price
taxes - Taxes and fees component
Flight Timing and Duration
legs0_departureAt - Departure time for outbound flight
legs0_arrivalAt - Arrival time for outbound flight
legs0_duration - Duration of outbound flight
legs1_departureAt - Departure time for return flight
legs1_arrivalAt - Arrival time for return flight
legs1_duration - Duration of return flight
Flight Segments
Each flight leg (legs0/legs1) can consist of multiple segments (segments0-3) when there are connections. Each segment contains:

**Geography and Route**
legs*_segments*_departureFrom_airport_iata - Departure airport code
legs*_segments*_arrivalTo_airport_iata - Arrival airport code
legs*_segments*_arrivalTo_airport_city_iata - Arrival city code
Airline and Flight Details
legs*_segments*_marketingCarrier_code - Marketing airline code
legs*_segments*_operatingCarrier_code - Operating airline code (actual carrier)
legs*_segments*_aircraft_code - Aircraft type code
legs*_segments*_flightNumber - Flight number
legs*_segments*_duration - Segment duration
**Service Characteristics**
legs*_segments*_baggageAllowance_quantity - Baggage allowance: small numbers indicate piece count, large numbers indicate weight in kg
legs*_segments*_baggageAllowance_weightMeasurementType - Type of baggage measurement
legs*_segments*_cabinClass - Service class: 1.0 = economy, 2.0 = business, 4.0 = premium
legs*_segments*_seatsAvailable - Number of available seats
**Cancellation and Exchange Rules**
Rule 0 (Cancellation)
miniRules0_monetaryAmount - Monetary penalty for cancellation
miniRules0_percentage - Percentage penalty for cancellation
miniRules0_statusInfos - Cancellation rule status (0 = no cancellation allowed)
Rule 1 (Exchange)
miniRules1_monetaryAmount - Monetary penalty for exchange
miniRules1_percentage - Percentage penalty for exchange
miniRules1_statusInfos - Exchange rule status
Pricing Policy Information
pricingInfo_isAccessTP - Compliance with corporate Travel Policy
pricingInfo_passengerCount - Number of passengers
**Target Variable**
selected - In training data: binary variable (0 = not selected, 1 = selected). In submission: ranks within ranker_id groups
**Important Notes**
Each ranker_id group represents one search session with multiple flight options
In training data, exactly one flight option per ranker_id has selected = 1
The prediction task requires ranking flight options within each search session
Segment numbering goes from 0 to 3, with segment 0 always present and higher numbers representing additional connections
**JSONs Raw Data Archive**
The competition includes a json_raw_tar.gz archive containing the original raw data from which the train and test datasets were extracted. This archive contains 150,770 JSON files, where each filename corresponds to a ranker_id group. Participants are allowed to use this raw data for feature enrichment and engineering, but it is not obligatory and only an option.

**Warning:** The uncompressed archive requires more than 50GB of disk space.

'jsons_raw.tar.kaggle'* - Compressed JSONs raw data (150K files, ~50gb). To use the file as a regular .gz archive you should manually change extension to '.gz'. Example jsons_raw.tar.kaggle -> jsons_raw.tar.gz
'jsons_structure.md' - JSONs raw data structure description
