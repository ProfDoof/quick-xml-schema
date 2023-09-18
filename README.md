# xml-schema
[![Build Status]][travis] [![Latest Version]][crates.io] [![Coverage Status]][coveralls]


[Build Status]: https://travis-ci.org/media-io/xml-schema.svg?branch=master
[travis]: https://travis-ci.org/media-io/xml-schema
[Latest Version]: https://img.shields.io/crates/v/xml-schema.svg
[crates.io]: https://crates.io/crates/xml-schema
[Coverage Status]: https://coveralls.io/repos/github/media-io/xml-schema/badge.svg?branch=master
[coveralls]: https://coveralls.io/github/media-io/xml-schema?branch=master
[xml-schema]: https://github.com/media-io/xml-schema/tree/main
[quick-xml]: https://github.com/tafia/quick-xml
[serde]: https://github.com/serde-rs/serde

Generate rust code with [serde][serde] and [quick-xml][quick-xml] derivations 
(structures and enum) from XSD

This is a derivative work from [xml-schema][xml-schema] but built for use with quick-xml 
and serde instead of YaSerde and xml-rs

## Usage

In the entrypoint of your rust project, add these folowing lines:

```rust
use quick_xml_schema_derive::XmlSchema;
```

Then implement the XSD using:

```rust
#[derive(Debug, XmlSchema)]
#[xml_schema(source = "path_to_schema.xsd", target_prefix = "my_prefix")]
struct MySchema;
```

Remark: the `MySchema` don't need to be public. It serves as a source of information.  

### Attributes

**source**: Source of the XSD - XML Schema. It can be local file (related to the root of the project) or an HTTP resource.  
**target_prefix**: The schema not define any prefix. It the `targetNamespace` is declared in the schema, this attribute is required.  
**store_generated_code**: Optional attribute for debug purpose. It store the generated Rust code into the file - the attribute value is the output filename.  
**log_level**: To configure the logger level at the the compile time - usefull if the XSD generate some bugs. Values can be `error`, `warn`, `info`, `debug`, `trace`.  
**module_namespace_mapping**: map a namespace to a Rust module. It can be present many times to map multiple namespaces to different Rust modules.  

