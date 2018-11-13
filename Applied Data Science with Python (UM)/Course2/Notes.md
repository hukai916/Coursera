Week1 Introduction
=====
 1. Cairo's visualization wheel technique

 2. Data-ink ratio (non-erasable core of a graphic):should try to increase the data-ink ratio by removing chartjunks:
 type1: unintended optical art (like shading and pattern); <br> type2: grid; <br>
 type3: the duck( non-data creative graphics), the visual embellishments that are not essential to understanding the data

 3. To push minimalism to a new level: sparkline is a tiny chart in a worksheet cell that provides a visual representation of data.

 4. Lie factor is the size of an effect shown in teh graphic divided by the size of the effect actually in the data.

 5. The Truthful Art of Alberto Cairo is one highly recommended book for data scientist.

 6. Cairo's five part frame work for considering the qualities of an information graphic: <br> 1. Truthful; <br> 2. Functional (data-ink ratio, direct labeling can increase comprehension); <br> 3. Beatiful; <br> 4. Insightful; <br> 5. Enlightening (social responsibility dimension).

 7. Alberto Cairo's three misleading mechanisms: hiding relevant data, display too much data and obscuring reality; distorting data through graphic forms.

Week2 Basic Plotting with matplotlib
=====
1. Matplotlib can be confusing to learn from web resources because there is a traditional object-oriented API as well as a MATLAB-like scripting model.

2. To enable web based rendering, use IPython magic: <br> **%matplotlib notebook** <br> The matplotlib will be configured to render into the browser, this configuration is called backend. A backend is an abstraction layer which knows how to interact with the operating system like the browser, and knows how to render matplotlib commands. <br><br> **%matplotlib inline** <br> This changes the backend to inline, the output figures will be displayed right below the figure and will be stored in notebook. <br><br> **import matplotlib as mpl<br>
mpl.get_backend()** <br> The get_ or set_ is not so pythonic, you can use tab to auto-complete them.

3. The artist layer is an abstraction around drawing and layout primitives. The root of visuals is a set of containers which includes a figure object with one or more subplots, each with a series of one or more axes. The **axes** is the most common object to interact with; Matplotlib also has **axis** object as well. **An axes is made up of two axis objects.**

4. Artist layer also contains primitives and collections objects. The scripting layer in this courser is called pyplot which actually creates those artists and choreographs them all together. The pyplot is an example of a procedural information visualization method. Everything you see in a matplotlib Figure is an Artist instance:

5. The primitive artists: the kinds of objects you see in a plot: Line2D, Rectangle, Circle and Text. Composite artists: collections of Artists such as the Axis, Tick, Axes and Figure. Each composite artist may contain other composite artists as well as primitive artists.

6. Axes is the most important composite artist, which is where most of the matplotlib API plotting methods are defined. <br> **Axes.imshow Axes.hist Axes.plot: <br>** AxesImage Rectangel Line2D <br><br>
**import matplotlib <br>
ax = matplotlib.figure.Figure().add_subplot(111)<br>** The Axes artist is added automatically to the figure container fig.axes.

7. Scripting Layer (pyplot): most special-purpose languages for data analysis and visualization provide a lighter scripting interface to simplify common tasks, as the pyplot interface. <br>
**import matplotlib.pyplot as plt <br>
import numpy as np <br>
x = np.random.randn(10000) <br>
plt.hist(x, 10) <br>**
pyplot will check its internal data structures to see if there is a current Figure and Axes.
If no, it will create a Figure and Axes, set these as current and direct the plotting to Axes.hist. <br><br>
**plt.title(r'Normal distribution with $\mu=0, \sigma=1$')** <br>
Also check first and direct the call to the Axes instance method Axes.set_title. <br><br>
**plt.savefig('matplotlib_histogram.png') <br><br>**
**plt.show()<br>**
This will force Figure to render using the specified backend.

8. pyplot is a stateful interface that handles much of the boilerplate for creating figures and axes and connecting them to the backend of your choice. pyplot also maintains module-level internal data structures representing the current figure and axes to which to direct plotting commands. When the pyplot module is loaded, it parses a local configuration file in which the user states. If using a pure image backend like Agg, the script will generate the hard-copy output and exit.

9. zip has lazy evaluation, is actually a generator object. <br>
**zip_generator = zip([1,2,3,4,5], [6,7,8,9,10]) <br>
print(list(zip_generator))<br>
print(*zip_generator)<br>**
Single star unpacks a collection into positional arguments.
**x,y = zip(\*zip_generator)<br>**
Get back the original list pair.

10. Compared to scatter plot, we only provide with y values to line plot, and plot will use index as x values smartly.

11. Convert NumPy dates into standard library dates: <br>
**pd.to_datetime<br>**

Week3
=====
1. Use "\_" to supress teh undesired output because boxplot turns to output raw data as well: <br>
**_ = plt.boxplot()**


2. The animation depends on backend, if using static PNG backend, it won'w work. You can export the animation using third pary tools like FFM.

Week4
=====
1. df.plot is simply a wrapper of plt.plot. df.plot returns an Axes object, you can apply any Axes method on.

2. Parallel coordinate plots are common way of visualizing high dimensional multivariate data.

3. Seaborn is based on matplotlib, good for statistical plotting. It adds more styles and make complicated plotting much simpler.

4. The joint plot creates a scatterplot together with the histogram for each individual variable. <br>
**sns.jointplot**
