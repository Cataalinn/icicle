Icicle
========

[![Build Status](https://travis-ci.org/segunfamisa/Icicle.svg?branch=dev)](https://travis-ci.org/segunfamisa/Icicle)

We all hate boiler plates right? We hate to have to do:

```java
@Override
protected void onSaveInstanceState(Bundle outState) {
    outState.putString(AWESOME_STRING, mAwesomeString);
    outState.putInt(AWESOME_INT, mAwesomeInt);
    super.onSaveInstanceState(outState);
}
```

And then have to do:

```java
@Override
public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);

    if (savedInstanceState != null) {
        mAwesomeString = savedInstanceState.getString(AWESOME_STRING);
        mAwesomeInt = savedInstanceState.getInt(AWESOME_INT);
    }
}
```

This is familiar Right?

Icicle does all the hard work for you. It **automagically** (I love that word too)
saves and restore your instance state.

## Setting up

  *  Add APT to your project-level `build.gradle` file

```groovy
buildscript {
    repositories {
        jcenter() // Also available in maven central
    }
    dependencies {
        ...
        classpath 'com.neenbedankt.gradle.plugins:android-apt:1.8'
    }
}
```
  *

```groovy
apply plugin: 'com.neenbedankt.android-apt'

dependencies {
    apt <icicle-processor>
    compile <icicle>
}

```


## Usage
Using Icicle is simple. Annotate the field variables you wish to persist the state
with `@Freeze`, call `Icicle.freeze()`
when you want to save, and call `Icicle.thaw()` when you wish to restore from the state.

```java
@Freeze
int mAwesomeInt;

@Freeze
String mAwesomeString;

@Override
public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    Icicle.thaw(this, savedInstanceState);
}

@Override
protected void onSaveInstanceState(Bundle outState) {
    Icicle.freeze(this, outState);
    super.onSaveInstanceState(outState);
}
```

Note: Icicle works only with non-private, non-final and non-static fields.


## Contributing
Contributions are welcome. (Still drafting the rules for contributing)

## License

    Copyright 2016 Segun Famisa

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
