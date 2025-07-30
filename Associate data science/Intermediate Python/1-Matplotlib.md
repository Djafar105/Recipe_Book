# Matplotlib
* Matplotlib is package that is essentially the core tool for data visualization in Python, and its most commonly used module (sub package) is `pyplot`. 
* The plotting process involves two main steps: 
	* General timeline:
		* First, creating the graph with commands like `pyplot.plot(x_axis, y_axis)` or `pyplot.scatter(x_axis, y_axis)`, where `x_axis` and `y_axis` are data structures such as lists or arrays
		* Second, rendering the graph with `pyplot.show()`, The `plot()` command prepares and stores the visual representation of the data internally, allowing you to add titles, labels, or multiple plots before finally displaying it with `show()`.
	* Plot manipulations :
		* `plt.xscale('log')`: using log as an attempt to linearise a chaotic evolution
		* **`plt.clf()`** (clear figure) is a Matplotlib command that **resets the current plotting canvas** by removing all drawn elements — plots, labels, axes, and decorations — without closing the figure window itself. It’s typically used when generating multiple plots in sequence to avoid overlap or residue from previous visualizations. Calling `plt.clf()` ensures you start with a **completely blank figure** before executing the next plotting commands.
* **Histograms** :
	* A histogram is basically like a **line carrying all the data points on its back**, where the position of each data point along the line corresponds to its value. To make sense of this distribution, we **slice the line into a set of equal segments called bins**. For each bin, we then build a **rectangle**: its **base** spans the width of the bin, and its **height** represents how many data points fall within that segment. The resulting shape visualizes how data is distributed across the entire range.
	* **Unlike curves, histograms are designed to capture the _distribution_ of data rather than its progressive evolution.** A curve (such as a line plot) focuses on how values change over a continuous variable, whereas a histogram groups values into bins (sequences of groups of data ranges) to show their frequency or density. **However, with enough data and sufficiently small bin widths, a histogram can be turned into a smooth curve (e.g., a probability density function). Conversely, a curve, when sampled at discrete points, can be binned and represented as a histogram.**
	* A histogram is inherently **1-dimensional per axis** because it shows the frequency distribution of **one variable** along the x-axis (or y-axis). The y-axis is not a variable but a **count or density** of how many data points fall into each bin.
	* **commands** : 
	* `plt.hist(horizental_parameter,bins=nob #number of bins wanted` : this would result into histograms translating how much data in every bin
* Customizations : 
```python
	# Labeling : 
	`plt.xlabel("label")`
	`plt.ylabel("label")`
	# Title :
	`plt.title("title)`
	# Tracage des axes :
	`plt.yticks([0,2,4,5,6])`  #you specify here the start from 0 
	#same with x 
	`plt.yticks([0,2,4,6],["0B","2B","4B","6B"])`  #you are mapping each tick position to a custom label.
	# Grid:
	`plt.grid(True)`
	# Size :
	plt.scatter(x, y, s=20) # adjusting the size of the scatter's points

	