# 3. Installing and using NPM packages
Created Sunday 19 July 2020


* Some useful packages:
	1. ``live-server`` - makes a local server with index.html as the homepage. Browser refreshes automatically when a file is changed.
	2. ``lodash`` - syntactic sugar for JavaScript.
* A package can be installed in two ways:


1. Locally - installed only in the current directory
	* **npm install package_name**
	* Creates a node_modules folder inside the current directory.
2. Global - available from anywhere in the computer
	* **npm install -g package_name**
	* no new folder is created, except in the node default directory


*****


* package.json has all the dependencies stored in it.
* Technically, the ``node_modules`` directory is not a part of the source code, it's more of an SDK. So its never uploaded to a repo. This can be done by including ``/node_modules`` in the ``.gitignore`` file.
* package.json also contains scripts to run the project, one-click to run.


