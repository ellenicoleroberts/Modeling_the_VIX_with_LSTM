![image](https://user-images.githubusercontent.com/100783805/178174658-b394e63d-d224-41fc-9e4e-3bbac8edabfd.png)

# __OptyX__

The proprietary OptyX technology implements machine learning as a means of predicting the percent profit or loss of a weekly call option's contract at two days until expiration using option contract variables (present call option price, strike price, underlying asset price, the Greeks, implied volatility, and volume), along with VIX prices, inflation percent, and various sentiment metrics. 

The predicted profit or loss, the 'y' outcome, is classified into the following three classes: 

    - '0': a loss of a contract's value greater than 30%, which constitutes a "Sell to Open" recommendation
    - '1': a change in a contract's value between -30% and 25%, which constitutes a "Pass" recommendation
    - '2': a gain in a contract's value greater than 25%, which constitutes a "Buy to Open" recommendation.

---

## __README.md Overview__

This README.md serves as a blueprint for navigating the entire OptyX repo. Included here is an explanation of the data gathering process for all OptyX data, relevent to both PART 1 and PART 2 of the OptyX project. Please note, *additional README.md files contained within __'Part1'__ and __'Part2'__ folders will provide further clarification for their respective folder.*

The following instructions will guide the user through the process of installing necessary libraries and running the applicable Jupyter notebooks, as well as provide a step-by-step explanation of the code's usage. 

---

## __Technologies__

This application leverages Python 3.7. 

---

## __Installation Guide__

Begin by cloning the GitHub repo (the same repo that this README.md file is contained within) into your terminal. 

Next, activate the correct environment by inputting the following command into your terminal:
`conda activate dev`

Within this environment, install the above listed dependencies. To do so, in your terminal while in this same repo, enter `pip install -r requirements.txt`.

---

## __Disclaimer__

Within the OptyX repo, the reader will notice numerous versions of notebooks and csv files. Provided OptyX is presently in development, these files remain at this time for record keeping purposes. 

---

## __Data Gathering__ 

Please see **SPY_21Q4_22Q1_V2.ipynb** (contained within the same folder that this README.md file is contained in).

Data for SPY option contracts (e.g. Strike Price, SPY Price, Greeks, Expiration, Call Last Price, etc.) as well as VIX data was directly pulled from [optionsDx](https://www.optionsdx.com/). This website provides a suite of historical options information. 

At present, the data relevent to this repo spans a six month period from October 2021 (Q4) to March 2022 (Q1).

The data was downloaded in the form of text files, with each month of data being a separate file, and then converted into Pandas DataFrames and further filtered. Once the data was formatted accordingly, each month's DataFrame was concatenated into one large dataset. 

This option contract dataset for the six month period was then merged with VIX, Sentiment metrics, and Inflation (determined according to MoM increase, replicated over a month to populate all rows). Together, this combined set of data comprised the features used in the machine learning models. Please consult the __'Sentiment Analysis'__ section below for further details regarding the Sentiment Analysis portion of the OptyX project.

Here is some additional insight into the data gathering and filtering process:

- The options data was in 30 minute increments.
- There were over 9 million rows before data cleaning. 
- Post-data cleaning and filtering, approximately 35K rows remained.
- For the purpose of the initial OptyX model, the focus was exclusively call contracts. With call contracts only, three trade scenarios per a single move of the underlying asset are possible, whereas the inclusion of puts would add another, near inverse dimension.

Features data insight:

- Strikes were filtered within -$3 to +$15 of SPY price to accumulate larger moves.
- Expiration Dates were filtered to include only weekly contracts (contracts expiring the same week, Monday-Friday).
- The max hold period was defined at 2.0DTE (Wednesday close) in order to permit studying of the rapid change of greeks and their effect on the contract.
- The Strike Distance formula was calculated to depict negative values for ITM contracts.

Target variable insight:

- ROI % of a contract was calculated, a preliminary step enabling the calculation of 'y'.
- The target variable, 'y' (classes of percent profit/loss of a contract's value) was defined according to the following criteria: 
    - '0': a loss of a contract's value greater than 30%, which constitutes a "Sell to Open" recommendation
    - '1': a change in a contract's value between -30% and 25%, which constitutes a "Pass" recommendation
    - '2': a gain in a contract's value greater than 25%, which constitutes a "Buy to Open" recommendation.

---

## __Sentiment Analysis__ 

Please refer to the folder titled __'Sentiment'__ and the Jupyter notebook __'sentiment-Copy9.ipynb.'__ 

The goal was to track market sentiment as reflected in tweets from Twitter. Tracking search words “S&P 500" and "stocks”, over 30,000 tweets were pulled. Tweets were collected into a Pandas DataFrame, cleaned, and fed into the NLTK Vader Model, a sentiment analysis tool that is specifically attuned to sentiments expressed in social media. Each tweet passed through the model and was assigned a composite score from -1 (most negative sentiment) to +1 (most positive sentiment). The composite scores for each day were then averaged to obtain a number for daily market sentiment. 

---

## __PART 1: Machine Learning__

Please refer to the README.md within folder **'Part1'** for the machine learning aspect of the OptyX product. Provided instructions detailed in this README.md will guide the user through navigating and comprehending the machine learning aspect of OptyX technology.

---

## __PART 2: Binomial Option Pricing Trees__

Please refer to the README.md within the folder labeled, __'Part2'__, to learn about future developments for OptyX.

---

## __Contributors__

Kfir Bar,
Aarchit Malhotra,
Aliza Naqvi,
Nicole Roberts,
Wilson Rosa
