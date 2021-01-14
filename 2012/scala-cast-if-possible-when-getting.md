---
title: 'Scala cast if possible when getting from Map'
date: 2012-06-22T11:19:00.000-07:00
oldUrl: "http://ciantic.blogspot.com/2012/06/scala-cast-if-possible-when-getting.html"
tags : [scala]
---

```scala
object MyAsDefaultTest extends App {  
  
  implicit def anyDefaultVal(theoption : Option[Any]) = {  
    new {  
      def asDefault[A](default: A) : A =  
        try {  
          default.getClass.cast(theoption.getOrElse(default))  
        } catch {  
          case _ => default  
        }  
    }  
  }  
  
  override def main(args: Array[String]) {  
    val numbers = Map(1 -> 123, 2 -> 321.123, 3 -> "fail")  
  
    println(numbers.get(1).asDefault(-1) * 3) // Returns 123  
    println(numbers.get(2).asDefault(-1) * 3) // Returns -3  
    println(numbers.get(3).asDefault(-1) * 3) // Returns -3  
    println(numbers.get(999).asDefault(-1) * 3) // Returns -3  
  
    println(numbers.get(3).asDefault("") + "test") // Returns "failtest"  
    println(numbers.get(2).asDefault(0.0) + 100) // Returns 421.123  
  }  
}
```