<!-- markdownlint-disable MD001 -->

# Protobuf

- [Types](#types)
- [Schema](#schema)

### Types

``` protobuf
// basic types
double
float
int32
int64
uint32
uint64
sint32
sint64
fixed32
fixed64
sfixed32
sfixed64
bool
string
bytes
```

### Schema

`my_schema.proto`:

``` protobuf
// the version of Protobuf
syntax = "proto3";

// an optional package specifier to prevent name clashes
package my_package;

// RPC service
service MyService {
    rpc MyFunction(MyRequest) returns (MyResponse);
    rpc MyOutputStream(MyRequest) returns (stream MyResponse);
    rpc MyInputStream(stream MyRequest) returns (MyResponse);
    rpc MyStream(stream MyRequest) returns (stream MyResponse);
}

// integers are used to identify each field
message MyRequest {
    required int32 my_int = 1;
    optional string my_string = 2;
}

message MyResponse {
    required int32 my_int = 1;
    optional string my_string = 2;
    repeated float my_array = 3;
}
```
