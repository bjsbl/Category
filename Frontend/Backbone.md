# Backbone

## Events

## Model

```
var Person = Backbone.Model.extend({
        run:function(){
            alert("Person Run");
        }
    },{
        eat:function(){
            alert("Person Eat")
        }
    });

    var Father = Person.extend({
        sleep:function(){
            alert("Father sleep")
        }
    },{
        dance:function(){
            alert("Father Dance")
        }
    });

    var test1 = new Person();
    var test2 = new Father();
    test1.run();
    Person.eat();
    test2.sleep();
    Father.dance();
    Father.eat();
    test2.run();
```

## Collection
## Router

```
var AppRouter = Backbone.Router.extend({
        routes:{
          '':'index'
        },
        index: function () {
            alert("Router Index");
        }
    });

rootRouter = new AppRouter();
Backbone.history.start();

```

## History
## Sync
## View

```
var homeView = Backbone.View.extend({
        el: "body",
        template: _.template("hello world"),
        render: function () {
            this.$el.html(this.template({}));
        }
   });
```