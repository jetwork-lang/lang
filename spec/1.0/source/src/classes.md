# Classes

A class as denoted by the `class` keyword represents an object type.

Classes consist of several internal properties, as described in the following table:

| Internal property | Description |
| ----------------- | ----------- |
| \[\[*Name*\]\] | The unqualified name of the class. |
| \[\[*Visibility*\]\] | The [visibility](visibility.md) of the class. |
| \[\[*ParentDefinition*\]\] | The parent definition of the class. |
| \[\[*SuperClass*\]\] | The super class of the class. It is undefined if the class is the `Object` class. |
| \[\[*Implements*\]\] | Set of interfaces the class implements. |
| \[\[*IsFinal*\]\] | Indicates whether the class is final or not. |
| \[\[*IsStatic*\]\] | Indicates whether the class is static or not. |
| \[\[*IsAbstract*\]\] | Indicates whether the class is abstract or not. |
| \[\[*AllowLiteral*\]\] | Indicates whether the class may be initialized through an object initializer or not; that is, if it has the `[Literal]` meta-data. |
| \[\[*TypeParameters*\]\] | The type parameter sequence of the class. |
| \[\[*StaticProperties*\]\] | Static properties of the class. |
| \[\[*Prototype*\]\] | Properties of the class prototype as a dictionary from string to symbol. |
| \[\[*Proxies*\]\] | Proxies defined by the class as a dictionary from string to function symbol. |
| \[\[*PlainMetadata*\]\] | Plain meta-data attached to the class. |

## Super class

By default, all classes, excluding `Object`, have `Object` as their super class.

It is a verify error if:

* a class attempts to extend itself;
* a class attempts to extend a subclass of itself.

## Parent definition

When the parent definition of a class is a package, the class has a fully package qualified name.

<!--

| Internal property | Description |
| ----------------- | ----------- |
| \[\[*JXMLColor*\]\] | For a JXML base class, indicates the supported color class. |
| \[\[*JXMLVectors*\]\] | For a JXML base class, indicates the supported vector classes. |

## JXML meta-data

A JXML base class may contain a `JXML` meta-data with two optional options `colorClass` and `vectorClass` that specify the fully package qualified name of a support class for the color and vector classes to use throughout XML attribute values in JXML files.

* It is a verify error if the fully package qualified names specified within `JXML` do not resolve to a class.
* It is a verify error if the class specified by `colorClass` does not contain a constructor with the signature `(...arguments: [*]) => void`.
* It is a verify error if the class specified by `vectorClass` does not contain a constructor that takes parameters of a same number type.
* Only one `colorClass` occurrence is allowed, contributing the class to the annotated class \[\[*JXMLColor*\]\] property.
* Multiple `vectorClass` occurrences are allowed, contributing multiple classes to the annotated class \[\[*JXMLVectors*\]\] property.

```
package org.myEngine {
    [JXML(
        colorClass = org.myEngine.Color,
        vectorClass = org.myEngine.Vector,
        vectorClass = org.myEngine.Vector3D
    )]
    public abstract class Node implements JXML {
        /* JXML... */
    }
}
```

-->

## Meta data

A class may contain zero or more plain meta-data:

```
[[N1(n2)]]
class C {}
```