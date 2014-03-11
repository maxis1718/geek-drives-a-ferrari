#mongoDB - Let's begin



####@ Why mongo?

---

* No SQL
* Fast
* Easy to use
* [Python](http://docs.mongodb.org/ecosystem/drivers/python/), [Java](http://docs.mongodb.org/ecosystem/drivers/java/), node.JS, C++, C#, PHP...

<br>
####@ How's data stored?

---

* <code>KEY-VALUE</code> pairs!

	![image](http://docs.mongodb.org/v2.4/_images/crud-annotated-document.png)

*  different naming scheme between traditional SQL and mongo

	<table>
<tr><td><b>traditional SQL</b></td><td><b>mongo</b></td></tr>
<tr><td>database</td><td>db</td></tr>
<tr><td>table</td><td>collection</td></tr>
<tr><td>entry</td><td>key-value</td></tr>
</table>


####@ Hello world!

---

1. go to the official online demo <a href="http://try.mongodb.org/" target=_blank>here</a>


* find all data in the collection <b>foo</b>
   
   <code>db.foo.find()</code>


* save/insert data into collection <b>foo</b>
	
   <code>db.foo.save({'name': 'hayman', 'score': 100})</code>


* find the entry with name: hayman

	<code>db.foo.find({'name': 'hayman'})</code>


<strong>This is how the key-value working!</strong>

<br>
####@ on <em>Doraemon</em>

---

1. Connect to <b>doraemon</b>

	<code>ssh doraemon</code> or <code> ssh \<username\>@doraemon.iis.sinica.edu.tw -p 2222 </code>
	

2. Enter mongo shell

	<code>mongo</code>
	

3. Switched to db <b>LJ40K</b>

	<code>use LJ40K</code>	
	

4. Select the collection <b>deps</b>

   to select a collection to manipulate, just use <code>db.deps</code> or <code>db['deps']</code>
   

5. Fetch one entry

	<code>db.deps.findOne()</code>
	
	```javascript
	{
		"_id" : ObjectId("52fd987bd4388c3ded3e9a3a"),
		"emotion" : "annoyed",
		"xPos" : "VBD",
		"docID" : 0,
		"xIdx" : 4,
		"yPos" : "RB",
		"rel" : "advmod",
		"sentID" : 0,
		"y" : "hey",
		"x" : "took",
		"yIdx" : 0,
		"udocID" : 3000
	}
	```

5. Find dependency relations labeled as <b>happy</b>

	<code>db.deps.find( {'emotion': 'happy'} )</code>
	
	```javascript
	{ "_id" : ObjectId("52fd9901d4388c3ded835fcd"), "emotion" : "happy", "xPos" : "NN", "docID" : 0, "xIdx" : 0, "yPos" : "NNS", "rel" : "dep", "sentID" : 0, "y" : "guyses", "x" : "hey", "yIdx" : 1, "udocID" : 29000 } <br>
{ "_id" : ObjectId("52fd9901d4388c3ded835fce"), "emotion" : "happy", "xPos" : "NN", "docID" : 0, "xIdx" : 0, "yPos" : "NN", "rel" : "dep", "sentID" : 0, "y" : "nbsp", "x" : "hey", "yIdx" : 3, "udocID" : 29000 } <br> ... 
	```
	
6. Find dependency relations in the docID <b>0</b>, categoried as <b>accomplished</b>

	<code>db.deps.find({'emotion': 'accomplished', 'docID': 0 })</code>
	
	<pre>{ "_id" : ObjectId("52fd995ed4388c3dedb3c1d1"), "emotion" : "accomplished", "xPos" : "VBD", "docID" : 0, "xIdx" : 1, "yPos" : "PRP", "rel" : "nsubj", "sentID" : 0, "y" : "I", "x" : "got", "yIdx" : 0, "udocID" : 0 } <br>
{ "_id" : ObjectId("52fd995ed4388c3dedb3c1d2"), "emotion" : "accomplished", "xPos" : "NN", "docID" : 0, "xIdx" : 3, "yPos" : "JJ", "rel" : "amod", "sentID" : 0, "y" : "new", "x" : "hair", "yIdx" : 2, "udocID" : 0 } <br> ... </pre>

---
<center>

[Document](http://docs.mongodb.org/manual/) &nbsp;&nbsp;|&nbsp;&nbsp;  [Try it out](http://try.mongodb.org/)  &nbsp;&nbsp;|&nbsp;&nbsp;  [Download](http://www.mongodb.org/downloads) &nbsp;&nbsp;|&nbsp;&nbsp; © by [maxis](nlp.cs.nthu.edu.tw/students/~maxis.kao/)

