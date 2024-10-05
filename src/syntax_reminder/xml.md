<!-- markdownlint-disable MD001 -->

# XML

- [XML elements and attributes](#xml-elements-and-attributes)
- [XML namespaces](#xml-namespaces)
- [XLink](#xlink)
- [XML Schema Definition (XSD)](#xml-schema-definition-xsd)

### XML elements and attributes

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<root>
    <my_element my-attribute="My attribute value">My element value</my_element>
</root>
```

### XML namespaces

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<root xmlns:ns1="https://my_namespace.org">
    <ns1:book></ns1:book>
</root>
```

### XLink

``` xml
<root xmlns:xlink="http://www.w3.org/1999/xlink">
    <website xlink:type="simple" xlink:href="https://my-website.com">Visit website</website>
</root>
```

### XML Schema Definition (XSD)

XSD schema

``` xsd
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">

    <!-- simple type -->
    <xs:simpleType name="TitleType">
        <xs:restriction base="xs:string">
            <xs:maxLength value="30"/>
        </xs:restriction>
    </xs:simpleType>

    <!-- complex type -->
    <xs:element name="book">
        <xs:complexType>
            <xs:sequence>
                <xs:element name="title" type="TitleType"/>
                <xs:element name="author" type="xs:string"/>
            </xs:sequence>
            <xs:attribute name="category" type="xs:string"/>
        </xs:complexType>
    </xs:element>
    
</xs:schema>
```

XML document

``` xml
<book category="fantasy">
    <title>The Hobbit</title>
    <author>J.R.R. Tolkien</author>
</book>
```
