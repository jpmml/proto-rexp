Proto-RExp
==========

Java library for reading and writing RProtoBuf messages

# Compatibility #

* [RProtoBuf] (http://cran.r-project.org/web/packages/RProtoBuf) 0.4.2 or newer.

# Installation #

The current version of Proto-RExp is **1.0.0** (21 June, 2015).

The library JAR file (together with source and javadoc JAR files) is distributed via Maven Central repository:
```xml
<dependency>
	<groupId>org.jpmml</groupId>
	<artifactId>proto-rexp</artifactId>
	<version>1.0.0</version>
</dependency>
```

# Usage #

### The R side of operations

Writing an RExp message:

```
library("RProtoBuf")

writeRExp = function(obj){
  con = file("rexp.pb", open = "wb")
  serialize_pb(obj, con)
  close(con)
}
```

Reading an RExp message:

```
library("RProtoBuf")

readRExp = function(){
  con = file("rexp.pb", open = "rb")
  obj = unserialize_pb(con)
  close(con)

  return (obj)
}
```

### The Java side of operations

Reading an RExp message:

```
public RExp readRExp() throws IOException {
  InputStream is = new FileInputStream("rexp.pb");

  try {
    CodedInputStream cis = CodedInputStream.newInstance(is);

    RExp obj = RExp.parseFrom(cis);

    return obj;
  } finally {
    is.close();
  }
}
```

Writing an RExp message:

```
public void writeRExp(RExp obj) throws IOException {
  OutputStream os = new FileOutputStream("rexp.pb");

  try {
    CodedOutputStream cos = CodedOutputStream.newInstance(os);

    obj.writeTo(cos);
  } finally {
    os.close();
  }
}
```

# License #

Proto-RExp is licensed under the [BSD 3-Clause License] (http://opensource.org/licenses/BSD-3-Clause).

# Additional information #

Please contact [info@openscoring.io] (mailto:info@openscoring.io)