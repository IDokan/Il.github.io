---
layout: post
title:  "Hello Python and matplotlib"
date:   2020-09-23 21:40:58 +0900
categories: AI basics
---
I just have started AI basics because some of my twitter followers recommend a book about AI.

I would begin my AI basics to remember my Python knowledge and how to use external libraries.
!Notice! I would not cover any AI stuffs today.

Here is today's code. Let me dive into it.
```
# Floating Population data which Gabriel researched for a week (Monday ~ Sunday)
floatingPopulation = [242, 256, 237, 223, 263, 81, 46]  # Initialize floating population in List
print('Floating population = ', floatingPopulation)

# Calculate sum and avg of the data
length = len(floatingPopulation)
sum = 0
avg = 0
i = 0

weekdaySize = 5

for i in range(0, length):
    sum = sum + floatingPopulation[i]

avg = sum / length
print('Total Sum: ', sum)
print('Total Average: ', avg)

# Declare external module to draw graph
import matplotlib.pyplot as plt
from matplotlib import font_manager, rc

dateNames = ['MON', 'TUE', 'WED', 'THR', 'FRI', 'SAT', 'SUN']   # Save name of date in List
# Make title of the graph
plt.title('Floating Population for a week', fontsize = 16)  # Big title
plt.xlabel('Day', fontsize = 12)                            # x-axis title
plt.ylabel('Floating Population', fontsize = 12)            # y-axis title
# Draw Line graph

# 1
# plt.scatter(dateNames, floatingPopulation)
# 2
plt.scatter(dateNames[0:weekdaySize], floatingPopulation[0:weekdaySize], c = 'red', edgecolor = 'none', s = 50)
plt.plot(dateNames, floatingPopulation)
plt.show()
```

First of all, I have defined variables
```
# Floating Population data which Gabriel researched for a week (Monday ~ Sunday)
floatingPopulation = [242, 256, 237, 223, 263, 81, 46]  # Initialize floating population in List
print('Floating population = ', floatingPopulation)

# Calculate sum and avg of the data
length = len(floatingPopulation)
sum = 0
avg = 0
i = 0

weekdaySize = 5
```

floatingPopulation is a list for integer. sum, avg, and i is defined as 0 because sum and avg is going to be calculated soon.

```
for i in range(0, length):
    sum = sum + floatingPopulation[i]

avg = sum / length
print('Total Sum: ', sum)
print('Total Average: ', avg)
```

Calculate sum with floating population. In this moment, I used for loops the formula would be
```
for var in range(begin, end):
  operation
```
In my code, var is i, begin is 0, end is length, and operation is add sum and variable in the array.

```
# Declare external module to draw graph
import matplotlib.pyplot as plt
```
I declared external modules to draw graph.

Python need to call import opeartor to use other module.
Python code in one module gains access to the code in another module by the process of importing it. When I call import, this statement do two operations. First, it searches for the named module and initialize the module if necessary. Second, it binds the results of that search to a name in the local scope. In middle of second operation, if I would give new name to module, I can use 'as' opeartor. Thus, like import matplotlib.pyplot as plt, I am able to use matplotlib.pylot module with a simple name "plt".
```
Note: For efficiency reasons, each module is only imported once per interpreter session. Therefore, you have to restart the interpreter if you change modules imported.
```
If you want to import font_manager, rc, you probably add a line.
```
from matplotlib import font_manager, rc
```
In this line, I did not import matplotlib twice, rather just font_manager and rc are imported as a variables.
All the functions and constants can be imported using *(Asterisk).

```
dateNames = ['MON', 'TUE', 'WED', 'THR', 'FRI', 'SAT', 'SUN']   # Save name of date in List
# Make title of the graph
plt.title('Floating Population for a week', fontsize = 16)  # Big title
plt.xlabel('Day', fontsize = 12)                            # x-axis title
plt.ylabel('Floating Population', fontsize = 12)            # y-axis title
```
Save day names in list and set title, x-axis title, y-axis title.

Finally I can draw a graph.
```
# Draw Line graph
# 1
# plt.scatter(dateNames, floatingPopulation)
# 2
plt.scatter(dateNames[0:weekdaySize], floatingPopulation[0:weekdaySize], c = 'red', edgecolor = 'none', s = 50)
plt.plot(dateNames, floatingPopulation)
plt.show()
```
Actually, plt.plot() is the easy way to draw line graph. First argument would be x-axis and second is going to be y-axis. Since plt.plot() is versatile, It is able to call with different argument call. Let me tell you later when necessary.

Furthermore, because I would like to emphasize weekday, I called plt.scatter(). This function adds points. In this function call, color is red and there is no edge color with 50 scale. FYI, details can be found in ![here](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.scatter.html).

```
plt.show()
```
Finally, you can show your graph with this only one function!

Thank you for visiting my blog. I hope you get something that you wanted.
