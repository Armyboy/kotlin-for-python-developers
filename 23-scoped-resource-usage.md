_This material was written by [Aasmund Eldhuset](https://eldhuset.net/); it is owned by [Khan Academy](https://www.khanacademy.org/) and is licensed for use under [CC BY-NC-SA 3.0 US](https://creativecommons.org/licenses/by-nc-sa/3.0/us/). Please note that this is not a part of Khan Academy's official product offering._

---


Kotlin does not have Python's _resource managers_ or Java's _try-with-resources_, but thanks to extension functions, there's `use`:

```kotlin
File("/home/aasmund/test.txt").inputStream().use {
     val bytes = it.readBytes()
     println(bytes.size)
}
```

`use` can be invoked on anything that implements the `Closeable` interface, and when the `use` block ends (whether normally or due to an exception), `close()` will be called on the object upon which you invoked `use`. If an exception is raised within the block or by `close()`, it will bubble out of `use`. If both the block and `close()` raise, it's the exception from the block that will bubble out.

Thus, you can create something resource manager-like by creating a class that implements `Closeable`, does its setup work in `init`, and does its cleanup work in `close()`.

In case you're wondering about how `use`, which is a function, can just be followed by a block like that, see the section on [DSL support](functional-programming.html#receivers).




---

[← Previous: File I/O](file-io.html) | [Next: Documentation →](documentation.html)
