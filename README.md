# Android Studio Log Templates for Kotlin

Android Studio provides 'Live Templates' for inserting recurring code snippets like loops and log statements. For example, hitting TAB when entering `logd` will produce

```java
    Log.d(TAG, "divide: foo");
 ```
 
Not all templates are available for Kotlin, yet. To spare you the time of creating them, this repo provides the Kotlin version of the log templates.

# Usage

* Download [templates/settings.jar](/templates/settings.jar) and import it in Android Studio via 'File > Import Settings...'

OR

* Download [templates/AndroidLogKotlin.xml](/templates/AndroidLogKotlin.xml) and move it into Android Studio's `templates` directory (on Windows: C:\Users\John\\.AndroidStudio3.1\config\templates)

# Overview

The following subsections show the main differences of Kotlin (below) compared to Java (above):
* No static members
* No trailing semicolon
* Usage of string templates

## logt - A static logtag with your current classname

```java
    private static final String TAG = "MainActivity";
```

```kotlin
    companion object {
        private const val TAG = "MainActivity"
    }
```

## logd - Log.d(TAG, String)

```java
    Log.d(TAG, "divide: foo");
```

```kotlin
    Log.d(TAG, "divide: foo")
```
    
## loge - Log.e(TAG, String, Exception)

```java
    Log.e(TAG, "divide: foo", e);
```

```kotlin
    Log.e(TAG, "divide: foo", e)
```

## logi - Log.i(TAG, String)

```java
    Log.i(TAG, "divide: foo");
```

```kotlin
    Log.i(TAG, "divide: foo")
```

## logm - Log method name and its arguments

```java
    Log.d(TAG, "divide() called with: a = [" + a + "], b = [" + b + "]");
```

```kotlin
    Log.d(TAG, "divide() called with: a = [$a], b = [$b]")
```

## logr - Log result of this method

```java
    Log.d(TAG, "divide() returned: " + result);
```

```kotlin
    Log.d(TAG, "divide() returned: $result")
```
    
## logw - Log.w(TAG, String, Exception)

```java
    Log.w(TAG, "divide: foo", e);
```

```kotlin
    Log.w(TAG, "divide: foo", e)
```
    
## wtf - Log.wtf(TAG, String, Exception)

```java
    Log.wtf(TAG, "divide: foo", e);
```

```kotlin
    Log.wtf(TAG, "divide: foo", e)
```
    
# Extended Log Templates

Personally, I use modified versions of the built-in templates that add the current thread name and an unambigious string ('###') to the log output. Printing the thread name proved to be invaluable when debugging multi-threaded apps. The string allows for easy filtering the log output generated by your app.

For example, for `logd` there is `logdt` that becomes

```kotlin
    Log.d(TAG, Thread.currentThread().name + " ### "
                + "divide: foo")
```

The resulting log entry looks something like this:

    05-11 21:48:30.338 4988-4988/com.example.test D/MainActivity: main ### divide: foo

The string is part of the message instead of the TAG because the latter is omitted from the log occasionally.

## Usage

* Download [extended_templates/settings.jar](/extended_templates/settings.jar) and import it in Android Studio via 'File > Import Settings...'

OR

* Download [extended_templates/AndroidLog.xml](/extended_templates/AndroidLog.xml) and [extended_templates/AndroidLogKotlin](/extended_templates/AndroidLogKotlin.xml) and move them into Android Studio's `templates` directory (on Windows: C:\Users\John\\.AndroidStudio3.1\config\templates)

**Note:** Any changes you've made to the Java log templates will get lost as the 'AndroidLog.xml' file is overwritten. You can prevent this by merging the XML files manually.

# Modify Templates

One can edit these templates and add new ones in Android Studio under 'Settings > Editor > Live Templates'.

Also, you can restore the built-in templates there if any problems occur after the import.
