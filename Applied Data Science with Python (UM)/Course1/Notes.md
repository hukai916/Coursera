Week 1: The Python Functions
======
1. Time epoch is set to Jan 1, 1970.

2. The map function: <br>
**map(min, a,b)**

3. Numpy basics: <br>
**np.random.randint(0,10,(4,3))
**np.arange(0,30,2)**<br>
**np.linspace(0,4,9)**<br>
**np.vstack([X,2*X])**<br>
  * use vstack to stack array in sequence vertically

  **Y.astype('f')**<br>
  **Y.argmax()**<br>
  * return the index of the max value4.

4.  Other notes: <br>
  * Both Pandas and Matplotlib are based on SciPy.
  * Pandas helps bring functionality in R into Python.
  * To iterate (index, value) in array:<br>
**for index, value in X.items():**<br>
  * Sort by modified key using lambda function: <br>
**X.items().sort(key=lambda kv:kv[0])**<br>

Week2: Pandas
=====
1. Several ways to initiate a Series: <br>
from dictionary: **pd.Series(dic_tem)**<br>
from list: **pd.Series([], index=[])**<br>

2. Referring: note that [] is property not method.<br>
**s.iloc[1]** <br>
**s[1]** # May cause conflict if Series indexed by integer<br>
**s.loc['index_label']** <br>
**s['index_label']** <br>

3. Lots of Series operation support vectorization which utilizes parallel computing and is very fast.

4. Pandas functions, like append and drop, will not change in place by default.

5. DataFrame is the core, two-dimensional Series object.<br>
**df = pd.DataFrame([Series1, Series2], index=['label1', 'label2'])**<br>

6. Selecting all rows for specific columns:
**df.loc[:,['Name', 'Cost']]**<br>
  * Chaining should be avoided: df.loc['Store 2']['Cost']

7.  Read in csv files:<br>
**df = pd.read_csv('olympics.csv', index_col = 0, skiprows=1)** <br>

8. Filtering df values:<br>
**df['Name'][df['Cost']>3]** # Or <br>
**df[df['Cost'] > 3]['Name']**, # Note that below returns a DF object <br>
**df[df['Cost']>3]** <br>

9. Set two level indice:<br>
**df = df.set_index([df.index, 'Name'])**<br>

10. Deal with missing values:<br>
**df = df.fillna(method='ffill')** # forward filling

11. Other notes:<br>
  * PlanetPython.org
  * Jupyter notebook cell magic function starts with %%
  * !cat xxx: this would invoke command xxx
  * **df.loc[df['Cost'] > 2] == df[df['Cost'] > 2]**: they both return DF object
  * Groupby:<br>
  **res.groupby('colname')**
      * res.groups is a dictionary of the groups

Week3: More on DF
=====
1. In the case below, if we change df_copy, the base df will also be changed, so use df.copy(). <br>
**df_copy = df**
2. Merge two df:
  * on indice:<br>
  **pd.merge(staff_df, student_df, how='inner', left_index=True, right_index=True)** # merge by using index and inner merge method
  * on colname:<br>
  **pd.merge(staff_df, student_df, how='left', left_on='ColName', right_on='ColName')**
3. Chaining index is generally bad while chaining method is good practice, here is an example: <br>
**df = pd.read_csv('census.csv')
(df.where(df['SUMLEV']==50)
    .dropna()
    .set_index(['STNAME','CTYNAME'])
    .rename(columns={'ESTIMATESBASE2010': 'Estimates Base 2010'}))**
4. Use df.apply() to apply function to each row in the dataframe:<br>
**df.apply(min_max, axis = 1)** # Note that min_max is a customized function. This would apply min_max function upon columns (axis = 1), each row will be sent to min_max as a dataframe.<br>
**df.apply(lambda x: np.max(x[rows]), axis=1** # You can also use lambda function.
5. Groupby: you must index that column before applying groupby<br>
**for group, frame in df.groupby('STNAME')**
6. Pivot tables: a way of summarizing data in a df, itself is a df, the row and column represent the variables you are interested in, the cell value is agg funtion result. <br>
**df.pivot_table(values='(kW)', index='YEAR', columns='Make', aggfunc=[np.mean,np.min], margins=True)** # this one used two agg function.
7. Pandas has four main time related classes: Timestamp, DatetimeIndex, Period and PeriodIndex.
8. Other notes:<br>
  * Pandas applymap will apply to each element of the dataframe, not often used though.
  * Groupby will perform the split and agg will perform the combine
  * Typically, there are 4 types of scales: ratio, interval, ordinal and nominal ratio: units are equally spaced; interval: units are equally space, but there is no true zero; ordinal: the order of the units is important, but not evenly spaced like the letter grades; nominal: categories of data, but the categories have no order with respect to one another.
  * To use string methods:<br>
  **df['df2'].str.split()**

Week4: Distributions in NumPy
=====
1. Binomial:<br>
**np.random.binomial(1,0.5)** # the change of 1 is 0.5 and flip 1 time.
2. Do a random experiment, repeat 10000 of a 20-time flips and count the number of over 15:<br>
**sum(np.random.binomial(20, 0.5, 10000) > 15)**  
3. Other distributions:
**np.random.uniform(0,1)** <br>
**np.random.normal(0.75)** <br>
**np.random.chisquare(2, size=10000)** <br>
4. Hypothesis testing: <br>
**from scipy import stats**<br>
**stats.ttest_ind(x,y)**
5. When using df.append(), be careful about the **ignore_index** option.
