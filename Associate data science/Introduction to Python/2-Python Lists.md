# Python Lists
## Introduction
* we found ourselves dealing with many values of the same identity , example height or weight , color etc , so instead of asiging each singular one to a distinctive variable , we needed simply a variable that can contains multiple values at the same time without diluting the uniquness of each value --> creation of **list** variable type 
* A list can contain different types of variables , even other lists so we talk about sublist 
* syntax for a list : ``` list=[5,"5",4.2,[7,8,2]]```
***
## Lists Operations
### Introduction
* Each value in a list has a pointer called **index** , that allows for us to extract it or to manipulate the list via it [[]]  ^c2a44c
* Indexing starts from 0 in normal fashion and from 1 in a reversed fashion 
### Subsetting 
* #### Intro : 
	* subsetting , is creating a subset of a set , list , it can be done in many ways:
* #### Indexing :  ^b10872
	* We basically extract a specific element of a list in order to [[#^c2a44c]]
	* **command** : ```list[insert_index]```
	* **example :** 		```
		1- list=[5,9,8,6]
		2- list[0]-->5 et list[-1]-->6 
		3- list1=[[5,54,789],[1,8,74,596]]
		4- list1[0][1]-->54``` 
* #### Slicing :
	* We basically create a multi element subset of the original set , (list)
	* **command** : we basically use ranging : 
		* `list[start(inclusive),end(exlusive)]` : the classical standard method
		* `list[:end(exlusive)]` : assume that we start from index 0
		* `list[start(inclusive):] ` : assume that we'll include all the rest even the last one so its inclusive at the end
	* example/mistake :
		`1- list1=[[5,54,789],[1,8,74,596]]`
		`2- list1[0:2][1]-->[1,8,74,596]`
		My objective in line 5 was to extract the second element from each of the first two sublists in `list1`. I mistakenly assumed that `list1[0:2][1]` would achieve this by first selecting the first two sublists and then applying `[1]` to each of them. In reality, Python evaluates brackets sequentially: the command `list1[0:2]` is not a pointer as i thought but rather creates a new list of the first two sublists, and `[1]` then retrieves only the second sublist `[1,8,74,596]`. update : this is achievable via numpy [[4-Numpy]]
### list manipulations :
* #### Addition :
	* we simply create a new list that contains the old list + the new added elemnts 
	* command : 
		`new_list=old_list+new_elemnts`
	* example : 
		`list2=list1+[1,2,3]`
		`list2-->[[5,54,789],[1,8,74,596],[1,2,3]]`
* #### Deletion :
	* command : `del old_list = [index or range of the thing to delete]`
* #### Substitution : 
	* we use the indexing or slicing technique to "select" the desire sequence to substitue then assign to it the new one 
	* command : `old_list[index or range]=new_elements`
	* example : 
		`list1[1][1]=56`
		`list1=[[5,56,789],[1,8,74,596]]
* #### Cloning 
	* In Python, variables don’t store values directly but act as references, reflectors to the objects in memory `x=[1,2,3]`, you have created the object `[1,2,3]`,stored on your computer , x serves as miror thats it ,
	* Assigning `y = x` copies the reflectors, not the object, the reflectee , 
	* Mutating through one name (`y[1] = 5`) ***CHANGES*** the underlying object, so automatically x is going to be changed 
	* if you want to actually create a physical copy of the object, that is called *clonning* , you can do one of the following commands: 
		* `y= list(x)`
		* `y=x[:]`
