angular
.module('testApp', [])
.directive('lists',lists)
.service('getlist',getlist)
.controller('testController',testController);

function testController(getlist,$scope){
	$scope.getListData = getListData;
	$scope.customer = {};
	$scope.addItem = addItem;
	function getListData(){
		getlist.getData().then(function(response){
			$scope.customer = response.data.country;
		})
	}
	getListData();
	function addItem(){
		console.log($scope.customer);
	}
	
}
function getlist($http,$q){
	return{
		getData: function(){
			return $http.get('http://localhost/angular_work/new_project/data.js').
			success(function(resp){				
			}).error(function(resp){
				return $q.reject(resp);
			})
		}
	}
}
function lists(){	
	return{
		scope:{
			datasource: '=',
			action: '&' 
		},
		template: '<ul><li ng-repeat="prop in datasource">{{ prop.name }}</li>'+
		'<button ng-click="addItem()">Add Item</button></ul>',
		controller:testController
	}
}
