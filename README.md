# PythonCode_Sizzy
# q.1 
from numpy import*
from pandas import*
import matplotlib.pyplot as plt
import csv


def time_series(T,x0,sigma):

  #Results
  x=[x0 for i in range(T)]

  #Errors
  epsilon=[2*random.randint(0,2)-1 for i in range(T)]
   
  for i in range(1,T):
    x[i]=x[i-1]+sigma*epsilon[i]
    
  plt.plot(x)
  plt.show()
  return x
  
print(time_series(60,1,0.1))

#q2
#Useful modules



#Data file
data = read_csv('C:\Users\Laira\Desktop\CPIAUCSL.csv',sep=',').set_index('DATE')

#prices vector & number of points
prices=data["CPIAUCSL"]
n=len(prices)

'''1. Inflation vector'''
#We arbitrary fix pi_0 at 0
pi=[0 for t in range(n)]

#We complete pi
for t in range(1,n):
    pi[t]=(prices[t]-prices[t-1])/prices[t-1]


'''2. Subsamples'''
#Splits in 2 halves
pi1=pi[:n//2]
pi2=pi[n//2:]

#Mean and standard deviation
mu1,mu2=mean(pi1),mean(pi2)
sd1,sd2=std(pi1),std(pi2)

'''3. Display'''

#Mean vector
mu=[mu1 for t in range(n//2)]+[mu2 for t in range(n//2)]

#Display
plt.plot(pi)
plt.plot(mu,label='Means of the two subsamples')
plt.title('Evolution of the inflation rate')
plt.ylabel('Inflation rate')
plt.xlabel('Time')
plt.legend()
plt.show()

