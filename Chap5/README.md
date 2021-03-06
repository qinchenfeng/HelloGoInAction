# Chap5

*Definition of static type language*

In compiling compiler needs to know every value's type.

*`struct`*

`struct` can be used to create a user type

```
type user struct{
    name        string
    email       string
    ext         int
    privileged  bool
}
var bill user
```

`struct` is a value type.

*`var`*

By convention, using `var` to init a variable to zero value.

*Create a struct*

Method 1

```
_ = user{
    name:       "Lisa",
    email:      "lisa@email.com",
    ext:        123,
    privileged: true,
}
```

Method 2

```
_ = user{"Lisa", "lisa@email.com", 123, true}
```

*`struct` in `struct`*

Instead of build in type struct also can be embed in struct.

```
type admin struct {
	person user
	level  string
}
```

*Create a type*

Instead of using a struct to create a type, we also can use build in type to create a new type.

```
type Duration int64
```

*Method*

Method is a function that belongs a type. It has 2 kinds of receiver:

1. Value receiver.
2. Pointer receiver.

The type variable no matter is value or pointer can call method with value receiver and pointer receiver. There is
implicit conversion happens, actually.

```
// lisa is pointer type and the notify's receiver is value type
// conversion
(*lisa).notify()

// bill is value type and the changeEmail's receiver is pointer type
// conversion
(&bill).changeEmail("bill@newdomain.com")
```

*Value receiver vs Pointer receiver*

Value receiver use the copy of value to call method, mutation to the value won't update.

Pointer receiver use the actual value to call method, mutation to the value will update.

*Primitive type*

Primitive type is passed by value.

1. Number
2. String
3. Bool

*Reference type*

When create a reference type variable , that variable is called header. The header is copied when pass in function and
methods and the underlying data is shared.

*Interface*

Interface define action , the action is implemented by type.

*Interface value constraint*

If interface implementation is pointer receiver then interface value must be pointer type, here no implicit conversion.
For value receiver , interface value could be both value and pointer type.

*Embedding type*

When declare an embedding type only type without field name, and outer type will inherit all embedding type's field and
method just like they are defined for outer type.

If outer type implements interface for its own type, then will overwrite embedding type's implementation.

*Identifier access control*

Identifier starts with uppercase letter can be accessed by outside package, if starts with lowercase then means its
private in its own package.

*Embedding type with lowercase type name and uppercase field*

In that case, the embedding type can't be accessed but because outer type inherit embedding type's field and method so by
using `outer.embedField` we can init embedding type field.
