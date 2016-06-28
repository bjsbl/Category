# Restangular(https://github.com/mgonto/restangular)
Restangular.all('users').getList()  // GET: /users
.then(function(users) {
  // returns a list of users
  $scope.user = users[0]; // first Restangular obj in list: { id: 123 }
})


$scope.user.getList('cars');  // GET: /users/123/cars


$scope.user.sendMessage();  // POST: /users/123/sendMessage


# 依赖
Angular and Lodash (or Underscore).

