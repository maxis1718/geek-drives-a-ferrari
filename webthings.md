WebThings
=========

### DOM manipulation

* ### requirement

	* HTML
	* CSS
	* jQuery


* ###Hello web!

	```python

	site/
		index.html
		css/
			style.css
		js/
			script.js
	```
	---
	
	* in `index.html` 
	
		```html
		<!DOCTYPE html>
		<html>
			<head>
				<link type="text/css" rel="stylesheet" href="css/style.css">
				<script type="text/javascript" src="js/script.js"></script>

				<title> my site's title </title>
			</head>
			<body>
				<div id="title"> Hello World </div>
				
				<div class="title"> Division 1 </div>
				<div class="title"> Division 2 </div>
				<div class="title"> Division 3 </div>
				
				<hr>
				
				<button id="show-dom-btn">show <title></button>
				<button id="show-id-btn">show id=title</button>
				<button id="show-class-btn">show class=title</button>				
				
				<hr>
				
				<div id="show"></div>
			</body>
		</html>
		```
	
	* in `style.css`
		```css

		div {
			font-size: 16px;
		}
		
		#title {
			font-size: 1.5em;
			color: red;
			background: yellow;
		}
		
		.title {
			color: blue;
		}
		```

	* in `script.js`
		```javascript
		$(document).ready( function(){

			$('title').text();
			$('#title').text();
			
			
			$('.title').text();
		} );
		
		function events(){
			
			var show_target = '';
			$('button').click( function(e){
				var button_id = $(this).attr('id');
				if ( button_id == 'show-dom-btn' ){
					show_target = 'title';
				}
				else if ( button_id == 'show-id-btn' ){
					show_target = '#title';
				}
				else if ( button_id == 'show-class-btn' ){
					show_target = '.title';
				}
				
				show(show_target)
			} );
			
			
		}
		
		function show(target){
			var objs = $(target);
			
			var print_str = '';
			$.each(objs, function(i, obj){
				print_str += obj.text();
			});
			
			$('#show').text(print_str)
		}
		```
