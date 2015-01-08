## unbxdAutosuggest.js
#####This library depends on jQuery and Handlebars libraries.

###Step 1 - Include scripts
Please include Jquery(> 1.7), Handlebars and unbxdAutosuggest.js in order.  
Default css can be applied by including unbxdAutosuggest.css in your html.

```javascript
<link rel="stylesheet" href="//unbxd.s3.amazonaws.com/unbxdAutosuggest.css">
<script type="text/javascript" src="//cdnjs.cloudflare.com/ajax/libs/handlebars.js/2.0.0/handlebars.min.js"></script>
<script src="//code.jquery.com/jquery-1.10.2.js"></script>
<script src="//unbxd.s3.amazonaws.com/unbxdAutosuggest.js"></script> 
```
###### PS - please include these script tags before the ending `</head>` tag in your html page.

###Step 2 - Configuration
##### Configure our autosuggest plugin by modifying below snippet according to your parameters and include that in your html page. Each of the options used is explained in-detail after the following snippet.

```javascript
// initialize unbxdautocomplete by invoking the unbxdAutoSuggestFunction
// with jquery & handlebars as its parameters. you will need to do this only once.
unbxdAutoSuggestFunction(jQuery, Handlebars);

$(function(){
		//on dom load set autocomplete options
		//Usage: $(<element>).unbxdautocomplete(options);
		$("#input").unbxdautocomplete({
			siteName : 'demosite-u1407617955968' //your site key which can be found on dashboard
			,APIKey : '64a4a2592a648ac8415e13c561e44991' //your api key which is mailed to during account creation or can be found on account section on the dashboard
			,minChars : 2
			,delay : 100
			,loadingClass : 'unbxd-as-loading'
			,width : 0
			,zIndex : 0
			,position : 'absolute'
			,template : "1column" 
			,mainTpl: ['inFields', 'keywordSuggestions', 'topQueries', 'popularProducts']
			,sideTpl: []
			,sideContentOn : "right"
			,showCarts : false
			,cartType : "separate"
			,onSimpleEnter : function(){
			    console.log("Simple enter :: do a form submit")
			    //this.input.form.submit();
			}
			,onItemSelect : function(data,original){
				console.log("onItemSelect",arguments);
			}
			,onCartClick : function(data,original){
				console.log("addtocart", arguments);
				return true;
			}
			,inFields:{
				count: 2
				,fields:{
					'brand':3
					,'category':3
					,'color':3
				}
				,header: ''
				,tpl: ''
			}
			,topQueries:{
				count: 2
				,header: ''
				,tpl: ''
			}
			,keywordSuggestions:{
				count: 2
				,header: ''
				,tpl: ''
			}
			,popularProducts:{
				count: 2
				,price: true
				,priceFunctionOrKey : "price"
				,image: true
				,imageUrlOrFunction: "imageUrl"
				,currency : "$"
				,header: ''
				,tpl: ''
			}
		});
	});
```
####Configuraton Options
- **siteName** : This value can be found in UNBXD dashboard. It is unique for every search site created in the dashboard.
- **APIKey** : This is a unique for every user account. It can also be found in dashboard in the account section.
- **minChars** : Minimum number of characters required to start showing suggestions. The value should be 0 or greater than 0
- **delay** : Number of milliseconds to wait before fetching results from server. This is helpful in waiting till user stops typing. 
- **loadingClass** : This class name will be added to input during data fetching process, so that user can see some loader animation or state change.
- **width** : if set any value (only integer), then it will be used to set the width of suggestions else defaults to input width.
- **position** : either **absoulte** or **fixed**
- **template** : either **1column** or **2column**. On mobile browsers, this value is set to **1column** by default and the functionalities in the **mainTpl** value will be displayed in the autocomplete.
- **mainTpl**: array of functionalities to be present in the main template in the order in which they need to appear. values can be **inFields**, **topQueries**, **keywordSuggestions**, **popularProducts**
- **sideTpl**: array of functionalities to be present in the side template in the order in which they need to appear. Values are same as the previous option.
- **sideContentOn** : either **left** or **right**. Used only when **template** is set to **2column**
- **showCarts** : either **true** or **false**. To show Add-to-cart button and quantity input.
- **cartType** : either **inline** or **separate**. Used only when **showCarts** is set to **true**
- **inFields** : This is an object with 2 properties. The first is **count** which is useful to adjust the number of IN-FIELDS shown to user and the second is **fields** which is useful in adjusting what kind of values are shown in secondary level *in-suggestions*.
```javascript
,inFields:{
//number of in-fields to display
	count: 2,
	//you can add or remove from fields list and also change the respective counts
	fields:{
		'brand':3 //show 3 values from brand
		,'category':3 //show 3 from category
		,'color':3 //show 3 from color
	}
	//update title or header value here
	,header: ''
	//give HBS template here.
	,tpl: ''
},
```
![in fields](/screenshots/infields.png "in fields")
- **topQueries** : This will help in setting the number of top-queries shown to user. This value takes an object with different properties as explained below. 

```javascript
,topQueries:{
	count: 2 //number of top queries to be shown
	//update title or header value here
	,header: ''
	//give HBS template here.
	,tpl: ''
}
```
![top-queries](/screenshots/top-queries.png "top-queries")
- **keywordSuggestions** : This will help in setting the number of keyword-suggests shown to user. This value takes an object with different properties as explained below. 

```javascript
,keywordSuggestions:{
	count: 2 //number of keyword suggestions to be shown
	//update title or header value here
	,header: ''
	//give HBS template here.
	,tpl: ''
}
```
![keyword-suggestions](/screenshots/keyword-suggestions.png "keyword-suggestions")
- **popularProducts** : This value takes an object with different properties as explained below.

```javascript
,popularProducts:{
	count: 2 //number of products to be shown
	,price: true //to show price in case of carts
	,priceFunctionOrKey : "price" //it can also be a function which takes an object as argument and returns a string or number
	,image: true //to show image
	,imageUrlOrFunction: "imageUrl" //it can also be a function which takes an object as argument and returns a image url
	,currency : "$"
	//update title or header value here
	,header: ''
	//give HBS template here.
	,tpl: ''
}
```
![popular-products](/screenshots/popular-products.png "popular-products")
- **onSimpleEnter** : This function will be called if user presses *enter* key without selecting any result.
- **onItemSelect** : This function will be called when a user selects one of the suggestions. It will be passed 2 arguments. The first argument is an object shown below and second value will be the original value from Unbxd.
```javascript
//the first argument
{
value : ""//user selected value
,type : ""//IN_FIELD || KEYWORD_SUGGESTION || TOP_SEARCH_QUERIES || POPULAR_PRODUCTS
,filtername : ""//available only incase of IN_FIELD
,filtervalue : ""//available only incase of IN_FIELD
}
```
- **onCartClick** : this function will be called when a user clicks on Add-to-cart button. The arguments will be same as **onItemSelect** but it includes quantity and uniqueId of the product.
- **hbsHelpers**: needs to be a function. You can register your handlebars helpers here.
- **processResultsStyles** : This option, if set, should be a function, with a single argument which takes an object with top, left and right properties in it. The function should return the object with all the css properties that can be applied to suggestions container. 
	Note: this object is generally used for positioning the suggestions.
- **resultsContainerSelector** : This option, if set, should be jQuery selector for DOM element where suggestions should be appended in Document. If not set, then suggestions will be appended to body.

###### PS - if you want more css changes than given in config file, please override classes in unbxdAutosuggest.css 
