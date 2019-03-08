Gas Transfer Lab analysis
Group 7
Ken Rivero-Rivera - hours
Catherine Johnson  - hours



number 8: Comment on the oxygen transfer efficiency and the trend or trends that you observe.
Oxygen transfer efficiency decreases as air flow increases
number 9: Propose a change to the experimental apparatus that would increase the efficiency.

number 10: Verify that your report and graphs meet the requirements.






```python
from aguaclara.core.units import unit_registry as u
u.define('equivalent = mole = eq')
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
from scipy import stats
import aguaclara.research.environmental_processes_analysis as epa
from scipy import optimize
import math

data_file_path_1 = "https://raw.githubusercontent.com/klr227/EnvELab/master/Gas_Transfer/350_Flow_Rate.tsv"
df_1 = pd.read_csv(data_file_path_1,delimiter='\t')
time_350 = epa.column_of_time(data_file_path_1,0).to(u.s)
DO_350 = df_1.iloc[1:,2].values * u.mg/u.L

data_file_path_4 = "https://raw.githubusercontent.com/klr227/EnvELab/master/Gas_Transfer/475_Flow_Rate.tsv"
df_4 = pd.read_csv(data_file_path_4,delimiter='\t')
time_475 = epa.column_of_time(data_file_path_4,0).to(u.s)
DO_475 = df_4.iloc[1:,2].values * u.mg/u.L

data_file_path_2 = "https://raw.githubusercontent.com/klr227/EnvELab/master/Gas_Transfer/525_Flow_Rate.tsv"
df_2 = pd.read_csv(data_file_path_2,delimiter='\t')
time_525 = epa.column_of_time(data_file_path_2,0).to(u.s)
DO_525 = df_2.iloc[1:,2].values * u.mg/u.L

data_file_path_3 = "https://raw.githubusercontent.com/klr227/EnvELab/master/Gas_Transfer/575_Flow_Rate.tsv"
df_3 = pd.read_csv(data_file_path_3,delimiter='\t')
time_575 = epa.column_of_time(data_file_path_3,0).to(u.s)
DO_575 = df_3.iloc[1:,2].values * u.mg/u.L

data_file_path_5 = "https://raw.githubusercontent.com/klr227/EnvELab/master/Gas_Transfer/650_Flow_Rate.tsv"
df_5 = pd.read_csv(data_file_path_5,delimiter='\t')
time_650 = epa.column_of_time(data_file_path_5,0).to(u.s)
DO_650 = df_5.iloc[1:,2].values * u.mg/u.L



columns = df_1.columns
columns
fig, ax = plt.subplots()
plt.plot(time_350,DO_350,'y')
plt.plot(time_475,DO_475,'b')
plt.plot(time_525,DO_525,'r')
plt.plot(time_575,DO_575,'g')
plt.plot(time_650,DO_650,'k')
plt.xlabel('Time(seconds)')
plt.ylabel('Dissolved Oyxgen (mg/L)')
ax.legend(['350 microM/s','475 microM/s', '525 microM/s', '575 microM/s','650 microM/s'])
plt.savefig('/Users/kenrivero/Documents/EnvELab/Gas_Transfer/DO_vs_time')
plt.show()

# number 3: Calculate C* based on average water temperature, barometric pressure, and the equation from environmental processes analysis.
temp = 22 * u.degC
pressure = 1 * u.atm
C_star = epa.O2_sat(pressure,temp)

#number 4: estimate K_vl using linear regression for each data set
#ln((C*-C)/(C*- C_0)) = -k_vl*(t-t0)
#put all data in an array
C_values = [DO_350,DO_475,DO_525,DO_575,DO_650]
time_data = [time_350,time_475,time_525,time_575,time_650]
#find the C_0 values
C_0_350 = data_file_path_1(2,0)
C_0_475 = data_file_path_2(2,0)
C_0_525 = data_file_path_3(2,0)
C_0_575 = data_file_path_4(2,0)
C_0_650 = data_file_path_5(2,0)

#create an array of all C_0 values
C_0_values = [C_0_350, C_0_475, C_0_525, C_575, C_0_650]

k_vl = np.zeros((24,),dtype=int) #initialize k_vl values
for i in range(0,23):
    y = np.log((C*-C_values[i])/(C*-C_0_values[i]))
    x = time_data[i] - time_data[i][0]
    slope, intercept, r_value, p_value, std_err = stats.linregress(x,y)
    k_vl[i] = slope

#number 5: plot model and actual data -- will need to create a model
#number 6: plot k_vl as a function of air flow rate
figure
plt.scatter(airflows, k_vl)
plt.xlabel('Air Flow Rate in micromoles/second')
plt.ylabel('k_vl values')
#number 7: plot OTE as a function of air flow rate with oxygen deficit (C*-C) set at 6 mg/L
f_O2 = 0.21
V = 750 *u.mililiters
O2_deficit = 6 * u.mg/u.L
n_air = these are the flow rates
MWO2 = 15.999*2 * u.g/u.mole
OTE = np.zeros(air_flow.size)

for k in range(airflows.size)
  OTE[k] = V*k_vl[k]*(O2_deficit)/(f_O2*air_flows[k]*MWO2)

figure
plt.scatter(air_flows,OTE)
plt.xlabel('Air Flow Rate in micromoles/second')
plt.ylabel('Oxygen Transfer Efficiency')

#number 8: Comment on the oxygen transfer efficiency and the trend or trends that you observe.
#Oxygen transfer efficiency decreases as air flow increases
#number 9: Propose a change to the experimental apparatus that would increase the efficiency.

#number 10: Verify that your report and graphs meet the requirements.



```
