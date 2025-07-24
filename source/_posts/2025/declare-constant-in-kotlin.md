---
date: 2025-07-25T00:06:00+08:00
updated: 2025-07-25T00:06:00+08:00
title: Declare Constant in Kotlin
tags:
  - Java
  - Kotlin
---

This article will show about how we could declare constant in Kotlin, and how to access them in both Java and Kotlin.

There are 3 ways to declare constant in Kotlin:
1. Top-Level Declaration
2. Companion Object
3. Object

<!-- more -->

## 1. Top-Level Declaration

Declaration

```kotlin Constants.kt
@file:JvmName("Constants")
const val CONSTANT_VALUE = 10
```

The Kotlin code above would compile to following Java code:

```java Constants.java
public final class Constants {
   public static final int CONSTANT_VALUE = 10;
}
```

We access the constant in following ways:

```java Application.java
public class Application {
  public static void main(String[] args) {
    System.out.println("Constant Value: " + Constants.CONSTANT_VALUE + " from Java");
  }
}
```

```kotlin Application.kt
fun main() {
  println("Constant Value: $CONSTANT_VALUE from Kotlin")
}
```

## 2. Companion Object

Declaration

```kotlin Constants.kt
class Constants {
  companion object {
    const val CONSTANT_VALUE = 10
  }
}
```

Compiled Java code:

```java Constants.java
public final class Constants {

  public static final int CONSTANT_VALUE = 10;

  @NotNull
  public static final Companion Companion = new Companion((DefaultConstructorMarker)null);

  public static final class Companion {

    private Companion() {
    }

    // $FF: synthetic method
    public Companion(DefaultConstructorMarker $constructor_marker) {
      this();
    }
  }

}
```

Access the constant in following ways:

```java Application.java
public class Application {
  public static void main(String[] args) {
    System.out.println("Constant Value: " + Constants.CONSTANT_VALUE + " from Java");
  }
}
```

```kotlin Application.kt
fun main() {
  println("Constant Value: ${Constants.CONSTANT_VALUE} from Kotlin")
}
```

## 3. Object

Declaration

```kotlin Constants.kt
object Constants {
  const val CONSTANT_VALUE = 10
}
```

Compiled Java code:

```java Constants.java
public final class Constants {

  public static final int CONSTANT_VALUE = 10;

  @NotNull
  public static final Constants INSTANCE;

  private Constants() {
  }

  static {
    Constants var0 = new Constants();
    INSTANCE = var0;
  }

}
```

Access to the constant are same as using Companion Object:

```java Application.java
public class Application {
  public static void main(String[] args) {
    System.out.println("Constant Value: " + Constants.CONSTANT_VALUE + " from Java");
  }
}
```

```kotlin Application.kt
fun main() {
  println("Constant Value: ${Constants.CONSTANT_VALUE} from Kotlin")
}
```

## Conclusion

Top-Level Declaration is the simplest way to declare constant and the compiled Java code is same with the way I declare constant in Java.
But I can't control the access of the constant since I can't add the public / private modifier to the constant.

I personally preferred using Object to declare constants because the compiled Java is closer with Top-Level Declaration and much simpler than using Companion Object.
In addition, I can add public / private modifier to control the access to the constant.