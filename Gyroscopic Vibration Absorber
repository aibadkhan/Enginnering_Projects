# -*- coding: utf-8 -*-
"""
Created on Tue Dec 13 00:23:17 2022

@author: aibad
"""

# -*- coding: utf-8 -*-
"""
Created on Tue Dec 13 00:20:39 2022

@author: aibad
"""

# -*- coding: utf-8 -*-
"""
Created on Tue Dec 13 00:00:03 2022

@author: aibad
"""

import pylab as pl
import numpy as np
import scipy.integrate
time = np.reshape(ME2315_time, 1000000)
nospe = np.reshape(ME2315_acceleration_nospeed, 1000000)
maxspee = np.reshape(ME2315_acceleration_maxspeed, 1000000)
maxspee[0] = 0; nospe[0] = 0

#Acceleration vs. Time
pl.figure(1)
pl.plot(time, nospe, label = 'No Speed.', color = 'orange')
pl.plot(time, maxspee, label = 'Max Speed.', color = 'black')
pl.title('Acceleration vs. Time')
pl.xlabel('Time (secounds)')
pl.ylabel('Acceleration (meter/secound^2)')
pl.grid(); pl.legend()

#Simpson's 3/8th Rule
hv = (time[-1] - time[0]) / len(maxspee) #step size for velocity
hs = (time[-1] - time[0]) / (len(maxspee)/4) #step size for displacement ...:

#Max V

i=0
m=0
velocitymax = np.zeros(250000)
for m in range(250000):
    velocitymax[m] = 3/8*hv*(maxspee[i] + 3*maxspee[i + 1] + 3*maxspee[i + 2] + maxspee[i + 3])
    i=i+3
    m=m+1
velocitymax[0] = 0

#Max Displacement
i = 0
m = 0
speedmax = np.zeros(62500) #(1000000/4)/4
for m in range(62500):
    speedmax[m] = 3/8*hs*(velocitymax[i] + 3*velocitymax[i + 1] + 3*velocitymax[i + 2] + velocitymax[i + 3])
    i=i+3
    m=m+1
speedmax[0] = 0

#No Velocity
i = 0
m = 0
novelocity = np.zeros(250000)
for u in range(250000):
    novelocity[m] = 3/8*hv*(nospe[i] + 3*nospe[i + 1] + 3*nospe[i + 2] + nospe[i + 3])
    i=i+3
    m=m+1  
novelocity[0] = 0

#No Displacement
i = 0
m = 0
nospeed = np.zeros(62500)
for m in range(62500):
    nospeed[m] = 3/8*hs*(novelocity[i] + 3*novelocity[i + 1] + 3*novelocity[i + 2] + novelocity[i + 3])
    i=i+3
    m=m+1
nospeed[0] = 0
timecumtrapz = np.linspace(0,20,999999)

#Max Velocity 
velocitymaxcumtrapz = scipy.integrate.cumtrapz(maxspee, time)
velocitymaxcumtrapz[0] = 0

#Max Displacement 
speedmaxcumtrapz = scipy.integrate.cumtrapz(velocitymaxcumtrapz, timecumtrapz)

#No Velocity
novelocitycumtrapz = scipy.integrate.cumtrapz(nospe, time)
novelocitycumtrapz[0] = 0

#No Displacement 
nospeedcumtrapz = scipy.integrate.cumtrapz(novelocitycumtrapz, timecumtrapz)

#Figure 2 Velocity vs. Time (trapezoid )
pl.figure(2)
timecumtrap2 = np.linspace(0,20,999998) 
timedisplacement = np.linspace(0,20,62500)
pl.plot(timecumtrap2, nospeedcumtrapz, label = 'No Speed Velocity', color = 'blue')
pl.plot(timecumtrap2, speedmaxcumtrapz, label = 'Max Speed Velocity.', color = 'black')
pl.title('Velocity vs. Time (trapz)')
pl.xlabel('Time (secounds)')
pl.ylabel('velocity (meters/secound)')
pl.grid(); pl.legend()

#Figure 3 Displacement Vs. time (3/8th Simpsons Rule)
pl.figure(3)
placement = np.linspace(0,20,62500)
pl.plot(timedisplacement, nospeed, label = 'No Speed Displacement' , color = 'green')
pl.plot(timedisplacement, speedmax, label = 'Max Speed Dispplacement' , color = 'black')
pl.title("Displacement vs. Time (3/8th rule)")
pl.xlabel('Time (secounds.)')
pl.ylabel('Displacement (meters)')
pl.grid(); pl.legend()

#Figure 4 Velocity Vs. time (trapz)
pl.figure(4)
timecumtrap2 = np.linspace(0,20,999998)
timedisplacement = np.linspace(0,20,62500)
pl.plot(timecumtrap2, nospeedcumtrapz, label = 'No Speed Velocity', color = 'purple')
pl.plot(timecumtrap2, speedmaxcumtrapz, label = 'Max Speed Velocity.', color = 'black')
pl.title('Velocity vs. Time (trapz)')
pl.xlabel('Time (secounds)')
pl.ylabel('velocity (meters/secound)') 
pl.grid(); pl.legend()

#Figure 5 Displacement Vs. time (3/8th Simpsons Rule) 
pl.figure(5)
placement = np.linspace(0,20,62500)
pl.plot(timedisplacement, nospeed, label = 'No Speed Displacement' , color = 'yellow')
pl.plot(timedisplacement, speedmax, label = 'Max Speed Dispplacement' , color = 'black')
pl.title("Displacement vs. Time (3/8th rule)")
pl.xlabel('Time (secounds.)')
pl.ylabel('Displacement (meters)')
pl.grid(); pl.legend()

#Amplitudes max and no displacement at 5 and 10 seconds (3/8th Simpsons Rule)
nospeed5 = nospeed[15625]#62500/4
speedmax5 = speedmax[15625]
nospeed10 = nospeed[31250]#62500/2
speedmax10 = speedmax[31250]

#Absorbtion change (3/8th)
vibrationabsorbtion5 = np.abs((nospeed5 - speedmax5) / nospeed5)*100
vibrationabsorbtion10 = np.abs(nospeed10 - speedmax10) / nospeed10*100
print('Vibe absorbption. in 5 seconds is {:.1f}% using 3/8th rule'.format(vibrationabsorbtion5))
print('Vibe absorbption. in 10 seconds is {:.1f}% using 3/8th rule'.format(vibrationabsorbtion10))

#Amplitudes of max and no displacement at 5 and 10 sec (trapzoid)
nospeedcumtrapz5 = nospeedcumtrapz[250000]#1000000/4
speedmaxcumtrapz5 = speedmaxcumtrapz[250000]
nospeedcumtrapz10 = nospeedcumtrapz[500000]#1000000/2
speedmaxcumtrapz10 = speedmaxcumtrapz[500000]

#Absportion change with (trapzoid)
vibrationabsorbtion5c=np.abs((nospeedcumtrapz5 - speedmaxcumtrapz5) / nospeedcumtrapz5)*100
vibrationabsorbtion10c=np.abs(nospeedcumtrapz10 - speedmaxcumtrapz10) / nospeedcumtrapz10*100
print('Vibe absorbption. in 5 seconds is {:.1f}% using trapz'.format(vibrationabsorbtion5c))
print('Vibe absorbption. in 10 seconds is {:.1f}% using trapz'.format(vibrationabsorbtion10c))

#Comments on the data and graphs
print('Using the 3/8th rule is the Disp. is off by 1e^-7 due to step size or roundoff error because plotting 1000000 data points. Use cumtrapz and 3/8th displacement vs. time to produce graph but they are different because its off by magnitude -7. Cumtrapz vibration absorption calculation produces percentages that are close together and are more belivable at the time given.')


