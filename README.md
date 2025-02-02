# ChatData

## Sqlite
We are using a file system called **sqlite**. It looks and acts like a real single user relational database (RDB). sqlite3 comes packaged with python. You do not need to install the library. You simply import it (as below).

- We are using Pandas to write and read to sqlite. Pandas will manage a lot of the complexity of dealing with a RDB. There are other ways of reading and writing to a RDB that are VERY common and often used in production systems.  

- The most common other way is to read or write to the RDB row by row. As you can see Pandas puts the entire dataframe into the RDB or extracts a new dataframe from the RDB. These are not row by row operations. These are set operations. Set operations ARE more efficient. However, it is common to use row by row operations to avoid needing large memory computers to hold the dataframes. One row only takes a few bytes. An entire dataframe could be many gigabytes and even petabytes of data. Obviously you will end up with problems with your compute resource if your files are this big. This will not happen to you in this activity and may never happen to you while you are a data analyst. Please just be aware of this. 

- This activity is primarily about querying a RDB, so, we are using a simple way that Pandas provides. If you want to learn the more complex way, just google 'reading and wrting to a relational database using python'. There are many resources to learn from.

- The data types that sqlite supports are quite limited. for example, it does not have a DATE type.  This is not a challenge for this project. However, more sophisticated database systems,such as Postgresql, have a large array of data types, such as "DATE", etc. that give those systems additional capability. 

- All of the SQL queries could also be performed on the Pandas DataFrames directly.  You may want to try this yourself for comparison (but make sure you do the SQL queries first, as this is an exercise in using SQL!).


## SQL Magic
Within the Jupyter notebook we will be using something called **SQL Magic**.  This provides a convenient way to write SQL queries directly into code cells in the notebook and to read the results back into a Pandas DataFrame.  This makes working with SQL much easier!

Note that you may need to update your sqlite version using `conda update -c anaconda sqlite` in order for the SQL Magic to work correctly.

## The Data Analysis Lifecycle
The sections in this notebook follow the stages of the Data Analysis Lifecycle introduced in an earlier activity.  The stages are:

- Acquire
- Transform
- Organise
- Analyse
- Communicate
- Maintain

## Preliminary Steps: Create a Database
First let's import Sqlite and the other libraries we will need.
```python
# Import Libraries
import numpy as np
import pandas as pd
import sqlite3
```

### Create the Database
Now we will create the Sqlite database.  Here is some code that does this for you.  We use the `%load_ext` magic command to load the SQL Magic extension and then use `%sql` to connect to the database.
```python
# If the db does not exist, sqlite will create it.
con = sqlite3.connect('chatdata.db')

# loads sql magic
%load_ext sql

# connects sql magic command to the correct db
%sql sqlite:///chatdata.db
```
