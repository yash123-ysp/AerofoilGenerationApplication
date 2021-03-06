# AerofoilGenerationApplication
An application that generates a NACA Aerofoil as per the requirement.
%matplotlib inline

import math

import matplotlib.pyplot as plt

import numpy as np

def camber_line( x, m, p, c ):

    return np.where((x>=0)&(x<=(c*p)),

                    m * (x / np.power(p,2)) * (2.0 * p - (x / c)),

                    m * ((c - x) / np.power(1-p,2)) * (1.0 + (x / c) - 2.0 * p ))

def dyc_over_dx( x, m, p, c ):

    return np.where((x>=0)&(x<=(c*p)),

                    ((2.0 * m) / np.power(p,2)) * (p - x / c),

                    ((2.0 * m ) / np.power(1-p,2)) * (p - x / c ))

def thickness( x, t, c ):

    term1 =  0.2969 * (np.sqrt(x/c))

    term2 = -0.1260 * (x/c)

    term3 = -0.3516 * np.power(x/c,2)

    term4 =  0.2843 * np.power(x/c,3)

    term5 = -0.1015 * np.power(x/c,4)

    return 5 * t * c * (term1 + term2 + term3 + term4 + term5)

def naca4(x, m, p, t, c=1):

    dyc_dx = dyc_over_dx(x, m, p, c)

    th = np.arctan(dyc_dx)

    yt = thickness(x, t, c)

    yc = camber_line(x, m, p, c)  

    return ((x - yt*np.sin(th), yc + yt*np.cos(th)),

            (x + yt*np.sin(th), yc - yt*np.cos(th)))

x=int(input('Enter the 4 Digit NACA Series: '))

m = (x//1000)*(1/100)

p = ((x//100)%10)*(1/10)

t = (x%100)*(1/100)

c = 1.0

x = np.linspace(0,1,200)

for item in naca4(x, m, p, t, c):

    plt.plot(item[0], item[1], 'b')

plt.plot(x, camber_line(x, m, p, c), 'r')

plt.axis('equal')

plt.xlim((-0.15, 1.15))
