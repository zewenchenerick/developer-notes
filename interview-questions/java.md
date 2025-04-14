# Java Interview Questions

## Object Oriented Foundation


## Object
### Common Methods for Object Class
The Object class is a special class and serves as the parent class for all other classes. It mainly provides the following 11 methods:
```java
/*
native methods
*/
public final native Class<?> getClass()

```


### Difference between == & equals()
`==` has different effects on primitive and references types:
* primitive type: `==` compare the values
* reference type: `==` compare the addresses of the objects

