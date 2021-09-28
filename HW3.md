HW3:  
Resources could be found [HERE](https://github.com/Yifeng-T/Biostat823_HomeWork/tree/main/HW3)  
The data sets are from [HERE](https://github.com/rfordatascience/tidytuesday/tree/master/data/2018/2018-11-13)    
  
# Introduction:
The three data sets are all related to malaria.  
Through a brief overview of the data sets, I found there are over 200 entities in each data set. In order to provide more efficient data visualization to users and make sure they could easily gain information about malaria in each entity, I used matplotlib and ipywidges libraries. Matplotlib could show a clear relationship between some indexes of malaria and year in every entity, while ipywidges could provide an interface to allow users to select their interested entities. I cannot show the information from all entities on one single graph, so I think giving the selection choice to users to see which one they are interested is a good idea. To enable users to view the current entity information, they can also take into account the data of other entities. I added the curve which representes the average value among all entities in table1 and table3. Below, I will show some details of each dataset and corresponding data visulizations. 
# The first data set:
## Overview: malaria_deaths.csv:
![table1.png](https://i.loli.net/2021/09/29/yjEiz7vYBUGw6QX.png)
The first table contains 6 variables. The column: "value" contains the exact same values as column:"Death-Malaria-Sex: both.... people)". It is just easier to call the values in that column by recreating a new column named "value". Mean_rate column contains the average death rate among all entities in each year. Below is the function to achieve the visulization and interface:
## Data visulization:  
```python
def create_plot(entity):
    
    with plt.style.context("ggplot"):
        fig = plt.figure(figsize=(8,6))
        
        plt.plot(table1[table1.Entity == entity].Year,
                 table1[table1.Entity == entity].value,
                 'o-',
                 color = 'black'
                   )
        plt.plot(table1[table1.Entity == entity].Year,
                 table1[table1.Entity == entity].mean_rate,
                 'o-',
                 color = 'red'
                   )
        plt.legend([f"{entity}", "Average of DeathRate for all entities"], title = "Entity vs Average")
        plt.xlabel("Year")
        plt.ylabel("Death rate/100,000 People")
        plt.title(f"The Death Rate of Malaria vs Year in {entity}")
        
widgets.interact(create_plot, entity=sorted(set(table1.Entity)));
```  
=================================  
Here is a brief gif picture to show how the interface works:
![graph1.gif](https://i.loli.net/2021/09/28/xZSUGlCundIqboQ.gif)

# The second data set
## Overview: malaria_deaths_age.csv
![table2.png](https://i.loli.net/2021/09/29/BQWnalxXmfh3zuV.png)  
The second table contains 5 variables. In the data visulization part, I will show the death rate of all corresponding age_geoups people V.S. year in each entity. Users could select the entity they want to see the information. Below is the function to achieve the visulization and interface:
## Data visulization for the second dataset:
```python
def create_plot2(entity):
    
    with plt.style.context("ggplot"):
        fig = plt.figure(figsize=(10,6))
        for i in range(0, len(age)):
            plt.plot(table2[(table2["entity"] == entity) & (table2["age_group"] == age[i])].year,
                     table2[(table2["entity"] == entity) & (table2["age_group"] == age[i])].deaths,
                     'o-')
        plt.grid(ls='--')
        plt.xlabel("Year")
        plt.ylabel("Death Cases")
        plt.legend(age, title = "Age Groups", loc='best')

        plt.title(f"The Death cases v.s. Year in {entity} for different age groups")
widgets.interact(create_plot2, entity=sorted(set(table2.entity)));
```
=================================  
Here is a brief gif picture to show how the interface works:  
![graph2.gif](https://i.loli.net/2021/09/28/5lAw3EUJXueGMDP.gif)

# The thrid data set
## Overview: malaria_inc.csv
![table3.png](https://i.loli.net/2021/09/29/e1ZjsMRhwKvCu5E.png)  
The third table contains 6 variables. The column: "value" contains the exact same values as column:"Incidence of malaria.... at risk)". It is just easier to call the values in that column by recreating a new column named "value". Mean_INCIDENCErate is a column contains the average death rate among all entities in each year. Below is the function to achieve the visulization and interface:
## Data visulization for the third dataset:
```python
def create_plot3(entity):
    
    with plt.style.context("ggplot"):
        fig = plt.figure(figsize=(8,6))
        
        plt.plot(table3[table3.Entity == entity].Year,
                 table3[table3.Entity == entity].value,
                 'o-',
                 color = 'black'
                   )
        plt.plot(table3[table3.Entity == entity].Year,
                 table3[table3.Entity == entity].mean_INCIDENCErate,
                 'o-',
                 color = 'red'
                   )
        plt.legend([f"{entity}", "Average of INCIDENCErate for all entities"], title = "Entity vs Average")
        plt.xlabel("Year")
        plt.ylabel("Incdidence rate/100,000 People")
        plt.title(f"The Death Rate of Malaria vs Year in {entity}")
        
widgets.interact(create_plot3, entity=sorted(set(table3.Entity)));
```
===========================  
Here is a brief gif picture to show how the interface works:
![graph3.gif](https://i.loli.net/2021/09/28/VbR1ngv9OTNxIPy.gif)