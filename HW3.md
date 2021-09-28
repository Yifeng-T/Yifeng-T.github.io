HW3
# Data visulization for the first dataset:  
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
![graph1.gif](https://i.loli.net/2021/09/28/xZSUGlCundIqboQ.gif)

# Data visulization for the second dataset:
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

![graph2.gif](https://i.loli.net/2021/09/28/5lAw3EUJXueGMDP.gif)

# Data visulization for the third dataset:
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
![graph3.gif](https://i.loli.net/2021/09/28/VbR1ngv9OTNxIPy.gif)
