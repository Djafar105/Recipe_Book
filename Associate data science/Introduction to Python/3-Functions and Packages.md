# Functions and Packages
## Introduction 
* Functions are a ready to use blocks of code made to facilitate the coding experience 
* example : in order to determine the biggest number in a list you can either do a small block of code that treats over the list and finds the highest number or simply use the function max via the command `max(list)`
* you can learn about a certain function by using a function called `help(function)`
## Methods 
* methods are functions but specific to certain type of object 
* examples : 
	* Lists: 
			1- **`list.index(insert_element)`**
			2- **`list.count(insert_element)`**
			3- **`list.append(insert_element)`** : adds an element to the list it is called on
			4- **`list.remove(insert_element)`** :[removes](https://docs.python.org/3/library/stdtypes.html#typesseq-mutable) the first element of a list that matches the input
			5- **`list.reverse()`** : [reverses](https://docs.python.org/3/library/stdtypes.html#typesseq-mutable) the order of the elements in the list it is called on
	* Strings :
			1- string.capitalize(): capitalizing the first letter
			2- string.replace("old_element","new_element")
## Packages 
* There are thousands of functions up to date; this is where **packages** come into play. They organize the functions into so-called **paniers (baskets)**. In order to use them, you first have to **install** them on your computer. Whenever you need them, you **call out the package** via a specific command and then use whatever function you want. 
* In python there is pip, a package maintenance system for python
* **Timeline of using a package** :
	* Note : the following instructions are for the classical off-road coding style , its recommended to just use the anaconda environment 
	* Installing packages: 
		* If pip is not installed : 
			* https://pip.pypa.io/en/stable/installation/
			* download `get-pip.py` : 
			* in terminal : 
				* python3 get-pip.py
		* If pip is allready installed :		
			* pip3 install insert_name_of_package
	* Implementation : 
		* - At the beginning of your code, call out the desired package via:  
		* `import name_of_the_package`
    
		- You can modify the package name by doing:  
		    `import old_name as new_name`
		    
		- To call a function from the package:  
		    `package_name.function_name()`
		    
		- You can import a specific function directly via:  
		    `from package import function`  
		    If you use this, you don’t need to type the package name each time, simply do:  
		    `function()`

## Python pause :
* **Raw shell (terminal)** = Bare metal Python, quick experiments.
- **IDLE (Integrated Development and Learning Environment)** = Polished shell + lightweight editor.
- **IDE (Integrated Development Environment)** = Heavy-duty environment for serious projects. example : pycharm
- When you download python from python.org you are downloading the language , or plutot the language compatabilite with your computer , + an idle , a package manager and some basic packages , in short you are getting the power to do `.py` on the files and you are not getting a ide , thats on you 
* checking for current version : 
	* in terminal do the command : `python --version`
* for pip (pip the package manager):
	* to check the current version do the same command
	* to check if a package is there : pip show insert_name_package
	* to check what are the packages available : `pip list`
	* to pip upgrade : `python.exe -m pip install --upgrade pip`