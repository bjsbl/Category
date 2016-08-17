# jasmine
>https://github.com/jasmine/jasmine/

# 分组(Suites)
Suites可以理解为一组测试用例，使用全局的Jasmin函数describe 创建。describe函数接受两个参数，一个字符串和一个函数。字符串是这个Suites的名字或标题，函数是实现Suites的代码块。

# 用例(Specs)
Specs可以理解为一个测试用例，使用全局的Jasmin函数it创建。和describe一样接受两个参数，一个字符串和一个函数，函数就是要执行的测试代码，字符串就是测试用例的名字。一个Spec可以包含多个expectations来测试代码。

# 期望(Expectations)
Expectations由expect 函数创建。接受一个参数。和Matcher一起联用，设置测试的预期值。

# 匹配(Matchers)
Matcher实现一个“期望值”与“实际值”的对比，如果结果为true，则通过测试，反之，则失败。每一个matcher都能通过not执行否定判断。




beforeEach(function)  //在每一个测试用例(it)执行之前都执行一遍beforeEach函数；  
afterEach(function)  //在每一个测试用例(it)执行完成之后都执行一遍afterEach函数；  
beforeAll(function)  //在所有测试用例执行之前执行一遍beforeAll函数；  
afterAll(function)  //在所有测试用例执行完成之后执行一遍afterAll函数；  