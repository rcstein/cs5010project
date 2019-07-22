#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Created on Thu Jul 18 13:51:34 2019

@author: becca
"""
import pandas as pd

import numpy as np

from matplotlib import pyplot

import mapplotlib.dates

import re




df_bydeath = pd.read_csv("incidents.csv")

#%%### Data pre-processing ####

# Remove URL and description (because of redundancy) columns. Remove age demographic because of redundancy with age column. Rename MFI column for clarity. 

df_bydeath.drop(["Description", "Media URL"], axis = 1, inplace = True)

df_bydeath.rename(columns = {"MFI" : "Total Deaths"}, inplace = True)

# Replace blank values in MFI with 1 to indicate 1 total fatality. Remove "# of" strings so that MFI column only shows total number of fatalities. 

total_fatalities = []

for i in df_bydeath["Total Deaths"]:
    
    if type(i) == float:
        
        i = 1 
    
    
    if type(i) == str:

        i = re.sub("\d\sof", "", i)
        
        i = re.sub("\d\s", "", i)
        
        i = int(i)
        
    total_fatalities.append(i)
    
df_bydeath["Total Deaths"] = total_fatalities

# Make Date column datetime type

df_bydeath["Date"] = pd.to_datetime(df_bydeath["Date"])

# Group data frame by event

df_byevent = df_bydeath.groupby(["Date", "State", "City"]).min().reset_index()


#print(df_bydeath["Date"].dtype)

# Dataframe with unknown ages removed

df_knownage = df_bydeath[df_bydeath.Age != "Unknown"]

# Dataframe with unknown smoke alarm status removed

df_knownalarm = df_bydeath[df_bydeath["Smoke alarms"] != "Not reported"]

# Dataframe with unknown causes removed

df_knowncause = df_bydeath[df_bydeath["Cause"] != "Under investigation"]

#%%################################# Data analysis ##################################

# Age: average age, average age of youngest victim, average age of oldest victim

# Most common cause, least common cause


## Extra -- compare to dataset of all fires if such a dataset exists (can check by locality / state), compare fatal incidents to all incidents. 



#%%################################# Data visualization #############################


# Plot incidents on map

# Overlay map with other data (e.g. temperature)

# Visualize by month



# Deadliest days plot

df_bydate = df_byevent.groupby(["Date"]).sum()

df_bydate.plot(style = 'k.', c = "red")



######################## Export results to files as needed ########################



################################## User interaction? ##############################




################################### Testing #######################################

