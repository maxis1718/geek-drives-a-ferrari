Git-rebase
===

1. `(master)` Switched to a new branch 'dev/layout'

		git co -b dev/layouts
	
	![](img/rebase-0.png)
	
	
2. `(dev/layout)` made some changes

	![](img/rebase-1.png)


3. `(dev/layout)` need to a js library in `master`

		git co master
		
	![](img/rebase-2.png)

4. `(dev/layout)` Switched back to to 'dev/layout'

	![](img/rebase-3.png)

5. `(dev/layout)` keep modifying files

	![](img/rebase-4.png)

6. `(dev/layout)` All modification done.	Rebase `dev/layout` to master

		git rebase master -i

	![](img/rebase-5.png)
	
7. `(dev/layout)` switch back to master 
	
	![](img/rebase-6.png)
	
	
8. `(master)` and merge `(dev/layout)`

	if we use the following command, would yield a __Fast-Forward__ situation!

		git merge master

	![](img/rebase-7.png)

	We don't want this because of the idea of keeping change logs in `dev/layout` branch
	 
	So what we are gonna do is give the option `--no-ff` to prevent from fast-forwarding.
	
		git merge master --no-ff 

	![](img/rebase-8.png)
