
# Going further with dictionaries 

### Introduction

Now that we know a little bit about lists and dictionaries, we can take data in a different digital format, and move it into code.  In this lesson, we'll see that in just a few lines of code, we can use Python to work with data in other formats.  Then we'll learn a couple of other methods for working with dictionaries: `keys()`, `values()`, and the `dict()` constructor.

### Objectives

* Understand how the list data structure aligns with data in non-programming contexts
* Understand how the dictionary data structure aligns with data in non-programming contexts
* See some of the steps involved in getting data from a different format and into code

### From Google Sheet to Local File

For example, here is [our list of travel cities and countries](https://docs.google.com/spreadsheets/d/1kv8z2lZ3NLWbJcdE6ysd40BZLresdl5W6mWrtIunMn4/edit?usp=sharing) in the form of a google sheet.  If you click on the link, you will see our spreadsheet.

<img src="./countries-cities.png" width="500">

You'll notice two additional columns: Population and Area. The Population column contains the population of the city in units of 1000 people. The Area column contains the area of the city in units of $km^2$. Now if we download this spreadsheet in the form of an .xlsx file we can start to work with it.

<img src="./download-xls.png" width="600">

We've already placed that file into this lesson, and you can see it [here](https://github.com/learn-co-curriculum/excel-to-python), where the contents of this lesson are also located.

### From Local File to Python 

Now that we have this file in the folder we are working with, we can get this data into Python code in a few lines.

> **Deep breath, soft eyes**: In the gray box below are four lines of code. They go over some topics we did not cover yet.  So don't worry, if you don't follow everything right now.  By the end of this unit, you will understand all of the code.  For right now, it's fine to just have a slight sense of what's going on.  


```python
import pandas
travel_df = pandas.read_excel('./cities.xlsx')
cities = travel_df.to_dict('records')
cities[0]
```




    {'City': 'Buenos Aires',
     'Country': 'Argentina',
     'Population': 2891,
     'Area': 203}



> Press shift+enter to run the code.

The code above relies on using an outside library called `pandas`, as it's good at reading excel files.  A library is just a set of reusable functions.  The `pandas` library is available for free online.  We tell our current Jupyter notebook that we are about to use it with the line `import pandas`.  

And that gives us an object, like a dictionary, which has a method in it called `read_excel`.  Similar to how we can call `{'foo': 'bar'}.keys()`.  That's the benefit of a library, we can get methods that do not come out of the box with Python.  So we use the `read_excel` data to read our excel file, by providing the name of the file, `cities.xlsx`, and the preceding `./` just indicates that the file is found in the current folder.  Finally with the line `travel_df.to_dict('records')` we return a list of our dictionaries representing our data.  You can see that when we access the first element of this list, it returns our first dictionary.  

Here is the code again, with some comments, if you are interested.


```python
# Here we use a library, which is some code not part of standard Python, to make this process easier 
import pandas
# If we use the `import pandas` we have access to the pandas library 
travel_df = pandas.read_excel('./cities.xlsx')
# We call the pandas.read_excel method and pass through the string './cities.xlsx' as the file is called cities.xlsx.  By saying './' we are saying 
# go to the current folder, excel-to-python, and find the 'cities.xlsx' file there
cities = travel_df.to_dict('records')
```


```python
cities
```




    [{'City': 'Buenos Aires',
      'Country': 'Argentina',
      'Population': 2891,
      'Area': 203},
     {'City': 'Toronto', 'Country': 'Canada', 'Population': 2732, 'Area': 630},
     {'City': 'Marakesh', 'Country': 'Morocco', 'Population': 929, 'Area': 230},
     {'City': 'Albuquerque', 'Country': 'USA', 'Population': 559, 'Area': 491},
     {'City': 'Los Cabos', 'Country': 'Mexico', 'Population': 288, 'Area': 3751},
     {'City': 'Greenville', 'Country': 'USA', 'Population': 93, 'Area': 68},
     {'City': 'Archipelago Sea',
      'Country': 'Finland',
      'Population': 60,
      'Area': 2000},
     {'City': 'Pyeongchang',
      'Country': 'South Korea',
      'Population': 44,
      'Area': 1464},
     {'City': 'Walla Walla Valley',
      'Country': 'USA',
      'Population': 33,
      'Area': 35},
     {'City': 'Salina Island', 'Country': 'Italy', 'Population': 3, 'Area': 26},
     {'City': 'Solta', 'Country': 'Croatia', 'Population': 2, 'Area': 59},
     {'City': 'Iguazu Falls',
      'Country': 'Argentina',
      'Population': 0,
      'Area': 2396}]



Look at that. Our variable `cities` is full of cities from our spreadsheet.

<img src="./countries-cities.png" width="500">

And we got there in four lines of code.


```python
import pandas
file_name = './cities.xlsx'
travel_df = pandas.read_excel(file_name)
cities = travel_df.to_dict('records')
```

And now that we have data, we can operate on it just like a normal list of dictionaries.

### Working with the keys and values functions

Now that we have the data in Python, we can use a couple of other of functions to quickly explore our data.  For example, let's say that we want to remind ourselves of all of the attributes associated with a single city.  If we just look at the first element we see both the keys and values.


```python
cities[0]
```




    {'City': 'Buenos Aires',
     'Country': 'Argentina',
     'Population': 2891,
     'Area': 203}



But, we really only need to see the keys.


```python
cities[0].keys()
```




    dict_keys(['City', 'Country', 'Population', 'Area'])



Note that the `keys()` function returns a `dict_keys` object.  It's a little tricky to work with that type of object, so let's coerce it into a list.


```python
list(cities[0].keys())
```




    ['City', 'Country', 'Population', 'Area']



Much better.

If we would like to also see our values of a dictionary in a list, we can do something similar with the `.values()` function for a dictionary.


```python
cities[0].values()
```




    dict_values(['Buenos Aires', 'Argentina', 2891, 203])




```python
list(cities[0].values())
```




    ['Buenos Aires', 'Argentina', 2891, 203]



Once again, we call the method, and then coerce it into a list, by using the `list` function.

### Creating Dictionaries

So far, we have seen one way of creating dictionaries: 


```python
philadelphia = {'City': 'Philadelphia'}
```

But there is another way!


```python
pittsburgh = dict(city='Pittsburgh')
pittsburgh
```




    {'city': 'Pittsburgh'}



As you can see, by using the keyword `dict`, we can pass through the name of the key followed by the equal sign.  Notice that the key name is provided as a string, but Python still knows how to handle it.  

Let's do one more.


```python
dict(city="Las Vegas", state="Nevada")
```




    {'city': 'Las Vegas', 'state': 'Nevada'}



### Summary

In this section we saw how to get our data from the outside world and into Python.  As we become better at Python, the usefulness of taking data and operating on it in code rather than a spreadsheet will become more apparent. We can even begin to try out our new skills with Python and our own data files outside of this lesson.

Next, we saw a few more methods for operating on dictionaries in Python.  Namely, we saw how to use the `keys()` function to retrieve the keys of a dictionary, and the `values()` function to retrieve the dictionary's values.  Finally, we saw how to use the `dict()` constructor to create a new dictionary.
