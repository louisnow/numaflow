# Map UDF

Map in a Map vertex takes an input and returns 0, 1, or more outputs. Map is an element wise operator.

## Builtin UDF

There are some [Built-in Functions](builtin-functions/README.md) that can be used directly.

## Build Your Own UDF

You can build your own UDF in multiple languages. A User Defined Function could be as simple as below in Golang.

```golang
package main

import (
	"context"

	functionsdk "github.com/numaproj/numaflow-go/pkg/function"
	"github.com/numaproj/numaflow-go/pkg/function/server"
)

func mapHandle(_ context.Context, keys []string, d functionsdk.Datum) functionsdk.Messages {
	// Directly forward the input to the output
	return functionsdk.MessagesBuilder().Append(functionsdk.NewMessage(d.Value()).WithKeys(keys))
}

func main() {
	server.New().RegisterMapper(functionsdk.MapFunc(mapHandle)).Start(context.Background())
}
```

Check the links below to see the UDF examples for different languages.

- [Python](https://github.com/numaproj/numaflow-python/tree/main/examples/function)
- [Golang](https://github.com/numaproj/numaflow-go/tree/main/pkg/function/examples)
- [Java](https://github.com/numaproj/numaflow-java/tree/main/examples/src/main/java/io/numaproj/numaflow/examples/function)

After building a docker image for the written UDF, specify the image as below in the vertex spec.

```yaml
spec:
  vertices:
    - name: my-vertex
      udf:
        container:
          image: my-python-udf-example:latest
```

### Available Environment Variables

Some environment variables are available in the user defined function Pods, they might be useful in you own UDF implementation.

- `NUMAFLOW_NAMESPACE` - Namespace.
- `NUMAFLOW_POD` - Pod name.
- `NUMAFLOW_REPLICA` - Replica index.
- `NUMAFLOW_PIPELINE_NAME` - Name of the pipeline.
- `NUMAFLOW_VERTEX_NAME` - Name of the vertex.

### Configuration

Configuration data can be provided to the UDF container at runtime multiple ways.

* [`environment variables`](../../reference/configuration/environment-variables.md)
* `args`
* `command`
* [`volumes`](../../reference/configuration/volumes.md)
* [`init containers`](../../reference/configuration/init-containers.md)
