> THE WORLD'S MOST POPULAR API FRAMEWORK
# http://swagger.io/

## swagger用于定义API文档。

好处：
* 前后端分离开发
* API文档非常明确
* 测试的时候不需要再使用URL输入浏览器的方式来访问Controller
传统的输入URL的测试方式对于post请求的传参比较麻烦（当然，可以使用postman这样的浏览器插件）

# https://github.com/springfox/springfox
# https://springfox.github.io/springfox/docs/snapshot/



## pom.xml
```
<properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <version.spring>4.1.6.RELEASE</version.spring>
        <version.jackson>2.4.4</version.jackson>
    </properties>

    <dependencies>
        <dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-swagger2</artifactId>
            <version>2.5.0</version>
        </dependency>
        <dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-swagger-ui</artifactId>
            <version>2.5.0</version>

        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-annotations</artifactId>
            <version>${version.jackson}</version>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
            <version>${version.jackson}</version>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-core</artifactId>
            <version>${version.jackson}</version>
        </dependency>

        <dependency>
            <groupId>log4j</groupId>
            <artifactId>log4j</artifactId>
            <version>1.2.17</version>
            <type>jar</type>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
            <version>${version.spring}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-web</artifactId>
            <version>${version.spring}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>${version.spring}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-beans</artifactId>
            <version>${version.spring}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>${version.spring}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>${version.spring}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context-support</artifactId>
            <version>${version.spring}</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.1.0</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
            <version>1.7.5</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>1.7.5</version>
        </dependency>
    </dependencies>
```

### java example
```
package org.cg.controller;

import org.cg.doc.Bean;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.ResponseBody;

import io.swagger.annotations.Api;
import io.swagger.annotations.ApiOperation;
import io.swagger.annotations.ApiParam;
import io.swagger.annotations.ApiResponse;

@Api(value = "Test控制器")
@Controller
@RequestMapping("/test")
public class TestController {

	@ApiOperation(value = "根据用户id查询用户信息", httpMethod = "GET", produces = "application/json")
	@ApiResponse(code = 200, message = "success", response = Bean.class)
	@RequestMapping(value = "/t")
	@ResponseBody
	public Bean index(@ApiParam(name = "userId", required = true, value = "用户Id") @RequestParam("userId") String userId) {
		return new Bean();
	}

	@ApiOperation(value = "查询用户信息", httpMethod = "GET", produces = "application/json")
	@RequestMapping(value = "/index")
	public String index2() {
		return "index";
	}
}

...

package org.cg.doc;

import io.swagger.annotations.ApiModel;
import io.swagger.annotations.ApiModelProperty;

@ApiModel(value = "Bean", description = "Sample model for the documentation")
public class Bean {

	@ApiModelProperty(value = "姓名", allowableValues = "available,pending,sold")
	private String name;
	@ApiModelProperty(value = "性别", dataType = "String", required = true)
	private String sex;
	@ApiModelProperty(value = "年龄", dataType = "int", required = true)
	private String age;
	private String email;

	getter/setter....

}

...

@Configuration
@EnableSwagger2
public class SwaggerConfig {

	@Bean
	public Docket customDocket() {
		return new Docket(DocumentationType.SWAGGER_2).apiInfo(apiInfo()).select().apis(RequestHandlerSelectors.basePackage("org.cg.controller"))
				.build();
	}

	private ApiInfo apiInfo() {
		return new ApiInfoBuilder().title("API Test").description("MyAPITest Description").version("3.0.0").build();
	}
}

...
spring.xml

<mvc:annotation-driven>
	</mvc:annotation-driven>

	<context:component-scan base-package="org.cg" />

	<mvc:default-servlet-handler />

	<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
		<property name="prefix" value="/WEB-INF/jsp/" />
		<property name="suffix" value=".jsp" />
	</bean>

```

### 在浏览器输入：http://localhost:<port&gt;/<basePath&gt;/swagger-ui.html


