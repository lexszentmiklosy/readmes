#Angular
 
 
 Directives
 	Custom HTML Tags
 	
 Dependency Injection
 
 Testable
 
 ng-model
 
 Model-View-Controller
 
 	Model-View-Presenter
 	Model-View-ViewModel
 	$scope is the glue between the View and the Controller (ViewModel?)
 	Seperation
 	
DRY 
	Don't Repeat yourself
	


var MainController = function($scope) {
	$scope.val = 5;
};

<div ng-controller="MainController">
	{{ val }}
</div>

Inside a controller scope is assumed, val will display 5.

###Three Ways to Declare a Controller

Not ideal

```
var MainController = function($scope) {
	$scope.val = 'test123';
};
```

Fine for development

```
app.controller('MainController', function($scope) {
    $scope.val = 'test456';
});

```



For Production

```
var app = angular.module('app', ['controllers']);

angular.module('controllers', []).controller('MainController', function($scope){
    $scope.val = "test789";
});
```

###ng-repeat



```
	app.controller('MainController', function($scope) {
    	$scope.myarr = [1, 2, 3, 4, 5];
	    $scope.users = [{name: 'Mike', age: 23},{name: 'Andy', age: 34},{name: 'Reid',age: 45}];
    	$scope.obj = {name: 'Mike', age: 23, job: 'programmer'};
	});

	<div ng-repeat="element in myarr">
    	{{element}}
	</div>

	//Use ng-repeat-start and ng-repeat-end for sibling elements that will be repeated
	
	<div ng-repeat-start="user in users">
		{{user.name}}: {{user.age}}
	</div>
	<hr ng-repeat-end />


	<div ng-repeat="prop in obj">
      {{prop}}
    </div>
    
	<div ng-repeat="(key, value) in obj">
		{{key}}: {{value}}
	</div>    
    
``` 
    
Note: Track by $index if repeated elements with primitave type. eg $scope.myarr =[1,2,2]

$index current position

booleans
$start $middle (not first or last), $last, 
$even, $odd (on the index) 


###$scope.watch


```
	$scope.mydata = {val: 'jake'};
    $scope.$watch('mydata.val', function(newval){
        $scope.mydata.toolong = newval.length > 15;
    });
    
    
    <input ng-model="mydata.val">
    <h1>{{mydata.val}}</h1>

    <span ng-show="mydata.toolong">Name is too long!</span>   
```

###ng-cloak

Hides content to prevent flash of content.

Requires CSS Rule:

```

[ng\:cloak], [ng-cloak], [data-ng-cloak], [x-ng-cloak], .ng-cloak, .x-ng-cloak {
  display: none !important;
}

```


##[Filters](https://docs.angularjs.org/api/ng/filter/filter)


```
	{{name | uppercase }}
```

or

```

$scope.mydata = {arr:['jane', 'jake', 'steven', 'lex']};
    
    
<input ng-model="myfilter.string">
    <div ng-repeat="user in mydata.arr | filter: myfilter.string ">
      {{user}}
    </div>
```


myfilter.name will only filter the name field, pass the whole object into filter:


```
	$scope.mydata = {arr:[{
        name: 'jane',
        age: 24
    },
    {
        name: 'jake',
        age: 22
    }]
    };
    
    
    <input ng-model="myfilter.name">
    <div ng-repeat="user in mydata.arr | filter: myfilter">
      {{user}}
    </div>
    
   Chain Filters
   <div ng-repeat="user in mydata.arr | filter: myfilter | orderBy: 'age' | limitTo: 2 ">
```

Custom Filters

```
app.filter('charlimit', function() {
    'use strict';
    return function(input, length) {
        if (!length) {
            length = 10;
        }
        if (!input) {
            return '';
        }

        if (input.length <= length ) {
            return input;
        } else {
            return input.substring(0, length) + '...';
        }
    };
});
```
    
```
      <div ng-repeat="user in mydata.arr | canDrink: 25">
          {{ user }}
      </div>
      
      
    app.filter('canDrink', function() {
	    return function(data, minage) {
    	    var filtered = [];
        	if (!minage) {
            	minage = 21;
        	}

	        for ( var i = 0; i< data.length; i++ ){
    	        var value = data[i];
        	    if ( value.age >= minage ) {
                	filtered.push(value);
            	}
	        }
    	    return filtered;
	    };
	});

```

###Services

Services are always singletons, they only exist in one place.

Sevice Types: 

**Constants**

+ Constants cannot be modified by a decorator. 
+ Doesn't actually mean constant outside of a decorator.

```
app.constant('constService', {attr: "this is const data!"});
```  
__
	
**Values**

+ Values be modified by a decorator. 

```
app.value('valService', function() {
    return "this is returned from a function";
});
```

* Factories

```
app.controller('MainController', function($scope, myFactory) {
    'use strict';
    console.log(myFactory.getdata()); // correct!
    console.log(myFactory.mydata); //undefined
});


app.factory('myFactory', function(){
    'use strict';
    var mydata = 'this is some other data';
    return {
        getdata: function() {
            return mydata;
        }
    };
});
```


```
Same as service below

app.factory('myFactory', function(){
    'use strict';
    var myString = 'this is some other data';
    var addToString = function(newstr) {
        myString += newstr;
    };
    return {
        getData: function() {
            return 'String contains: ' + myString;
        },
        addData: addToString
    };
});

```


* Services

Service declares a new instance of a class

```
app.service('myService', function(){
    'use strict';
    var myString = 'this is some other data';
    var addToString = function(newstr) {
        myString += newstr;
    };

    this.getData = function() {
        return 'String contains: ' + myString;
    };
    this.addData = addToString;
});

```


* Providers

always returns a $get object. 

```
app.provider('myTest', function(){
    'use strict';
    var myString = 'this is some other data';
    var addToString = function(newstr) {
        myString += newstr;
    };

    return {
        $get: function() {
            return {
                getData: function() {
                    return 'String contains: ' + myString;
                },
                addData: addToString
            };
        }
    };
});

```


* Decorators

Modify a data service without changing the origional code.

```
app.factory('myFactory',function() {
  var myString = "this is some other data"
  var addToString = function(newstr) {
    myString += newstr
  }
  return {
    getData: function() { return myString },
    setData: function(data) { myString = data },
    addData: addToString
  }
})

app.config(function($provide) {
  $provide.decorator('myFactory',function($delegate) {
    $delegate.reverse = function() {
      $delegate.setData($delegate.getData().split('').reverse().join(''))
    }
    return $delegate
  })
})

```


Depency Injections -
Order doens't matter. $scope, myFactory vs myFactory vs $scope
Issues with minification

```
Will Break
app.controller('MainController', function($scope,DataService) {
  $scope.mydata = DataService.data
}])

because DataService sill be minified to A which doesn't match app.factory('DataService')

Angular Solution
app.controller('MainController', ['$scope','DataService',function($scope,DataService) {
  $scope.mydata = DataService.data
}])

```

###Directives

Create a custom HTML element. 


```

	myDirective

	Directives are named camelcase but they are made lowercase with a dash in HTML (weird)

	<my-directive></my-directive>
	restrict: E (Element)
	
	<div my-directive></div>
	A (Attribute, default)
	
	<div class="my-directive"></div>
	C (Class)
	
	<!-- my-directive -->
	M (Comment)


	restrict: 'AECM' (allow multiple types)

	replace: 'true'
	Code will actually be replaced in the HTML, not appended in the element
	
	templateURL: 'photo.html'
	or
	template : "a string of html"


	Isolate Scope
	scope: {
		VariableNameInTemplate: '@';
		
		or
		
		VariableNameInTemplate: '@AttributeInHTML (that will be turned into template)'
	}
	
	
	@ // One way data binding Bounds to string data. Uses {{photo.date}}
	= //two way data binding. Binds to object use photo.date
	& //Pass an expression
	
	app.directive( 'photo', function() {
    'use strict';
    return {
        restrict: 'E',
        template:   '<figure>' +
                        '<img width="500px" ng-src="{{photoSrc}}" />' +
                        '<figcaption>{{caption}}</figcaption>' +
                    '</figure>',
        replace: true,
        scope:  {
            caption: '@',
            photoSrc: '@'
        }
    };
    
 ```
 
 
 In link functions:
 
 Not dependency injected.  
 * Scope= parent scope of the controller
 * Element: jqLite element that is the template 
 (figure)
 * Attributes: html attributes that included in the directive HTML (photo-src and caption)
   
 
 ```    
    link: function(scope, element, attrs) {
    	attrs.$observe('caption', function(value) {
    		element.find('figcaption').text(value);
    	}
    }
    
    <photo photo-src="{{photo.url}}" caption="Taken on: {{ photo.date }}" />

```


ng-click="functionNameInController()"


Directive Initiation:
 
 1. Compile: transforms all instances of directive, DOM Manipulation. All instances that don't require information from the scope
 
 
 2. Link: register DOM Listeners, single instance DOM Manipulation
 
 Most directives don't need/use a compile function, most just use Link. It is up to you to do it properly
 

### Normalization

These are all equivlent (in the view)
 
* ng-model
* ng:model
* ng_model
* data-ng-model
* x-ng-model

turns into Javascipt: ngModel


### Routing

Why use front end routing over backend?

Backend: validation, logins, etc

Front End: Deliver content, single page app.


```
var app = angular.module('app', ['ngRoute']);

app.controller('MainController', function($scope) {
    'use strict';
    $scope.somedata = 'Hello world';
});

app.config(function($routeProvider) {
    'use strict';
    $routeProvider
        .when('/', {templateUrl: 'view.html' })
        .when('/test', {templateUrl: 'view2html'})
        
        .when('/test/', { redirectTo: function(routeParams, path, search) {
            console.log(routeParams, path, search);
            return '/test/' + search.query;
        }})
        
        
        .otherwise({ template: 'Couldn\'t match a template'});
});

	<script type="text/ng-template" id="view.html">
    	<div ng-controller="MainController">This is a view with some data:	 {{ somedata }}</div>
	  </script>
  
  
```

* 38 Promises
* 39 Resolve - Need to rewatch
* 43 Digest/applying





$location.path vs redirectTo


hard page load vs soft page load
html5 push api (change URL in browser, not a hard page load)


### Events

$rootScope = highest level scope. . It is above a Main Controller scope.

* $on

* $broadcast - send to myself and every scope below me.

* $emit - send to myself and every scope above me.


### $Digest

$Apply



### Modules

[Law of Demeters](http://en.wikipedia.org/wiki/Law_of_Demeter)

Each unit should have only limited knowledge about other units: only units "closely" related to the current unit.



http://angular-ui.github.io/

[Firebase](http://www.firebase.com)


