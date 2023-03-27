# openaigo


Yet another API client for `api.openai.com`.

This library is community-maintained, NOT officially supported by OpenAI.

# Usage Example

```go
package main

import (
	"context"
	"fmt"
	"os"

	"github.com/xiao333ma/openaigo"
)

func main() {
	client := openaigo.NewClient(os.Getenv("OPENAI_API_KEY"))
	request := openaigo.ChatCompletionRequestBody{
		Model: "gpt-3.5-turbo",
		Messages: []openaigo.ChatMessage{
			{Role: "user", Content: "Hello!"},
		},
	}
	ctx := context.Background()
	response, err := client.Chat(ctx, request)
	fmt.Println(response, err)
}

```

```go

package main

import (
	"context"
	"fmt"
	"os"

	"github.com/xiao333ma/openaigo"
)

func main() {

	client := openaigo.NewClient(os.Getenv("OPENAI_API_KEY"))
	request := openaigo.ChatCompletionRequestBody{
		Model: "gpt-3.5-turbo",
		Messages: []openaigo.ChatMessage{
			{Role: "user", Content: "Hello!"},
		},
	}

	request := openaigo.ChatCompletionRequestBody{
		Model:    "gpt-3.5-turbo-0301",
		Messages: message,
		Stream:   true,
	}
	
	client.ChatStream(ctx, request, func(info openaigo.ChatCompletionStreamInfo) {
		if info.Err == nil {
			if len(info.Rsp.Choices) > 0 {
				res := info.Rsp.Choices[0].Delta.Content
				lastAnswer += res
				fmt.Printf("%s", res)
			}
		} else {
			if info.Err != io.EOF {
				fmt.Println(info.Err)
			}
			fmt.Println("\n")
		}
	})
}

```

if you just want to try, hit commands below.

```shell
git clone https://github.com/xiao333ma/openaigo.git
cd openaigo
OPENAI_API_KEY=YourAPIKey go run ./testapp/main.go
```

# API Keys?

Visit https://beta.openai.com/account/api-keys and you can create your own API key to get
started [for free](https://openai.com/api/pricing/).

# Endpoint Support

- Models
    - [x] [List models](https://beta.openai.com/docs/api-reference/models/list)
    - [x] [Retrieve model](https://beta.openai.com/docs/api-reference/models/retrieve)
- Text Completions
    - [x] [Create completion](https://beta.openai.com/docs/api-reference/completions/create)
- **Chat Completions** <- NEW!
    - [x] [Create Chat Completions](https://platform.openai.com/docs/api-reference/chat/create)
- Edits
    - [x] [Create edits](https://beta.openai.com/docs/api-reference/edits/create)
- Images
    - [x] [Create image (beta)](https://beta.openai.com/docs/api-reference/images/create)
    - [x] [Create image edit (beta)](https://beta.openai.com/docs/api-reference/images/create-edit)
    - [x] [Create image variation (beta)](https://beta.openai.com/docs/api-reference/images/create-variation)
- Embeddings
    - [x] [Create embeddings](https://beta.openai.com/docs/api-reference/embeddings/create)
- Files
    - [x] [List files](https://beta.openai.com/docs/api-reference/files/list)
    - [x] [Upload file](https://beta.openai.com/docs/api-reference/files/upload)
    - [x] [Delete file](https://beta.openai.com/docs/api-reference/files/delete)
    - [x] [Retrieve file](https://beta.openai.com/docs/api-reference/files/retrieve)
    - [x] [Retrieve file content](https://beta.openai.com/docs/api-reference/files/retrieve-content)
- Fine-tunes
    - [x] [Create fine-tune](https://beta.openai.com/docs/api-reference/fine-tunes/create)
    - [x] [List fine-tunes](https://beta.openai.com/docs/api-reference/fine-tunes/list)
    - [x] [Retrieve fine-tune](https://beta.openai.com/docs/api-reference/fine-tunes/retrieve)
    - [x] [Cancel fine-tune](https://beta.openai.com/docs/api-reference/fine-tunes/cancel)
    - [x] [List fine-tune events](https://beta.openai.com/docs/api-reference/fine-tunes/events)
    - [x] [Delete fine-tune model](https://beta.openai.com/docs/api-reference/fine-tunes/delete-model)
- Moderation
    - [x] [Create moderation](https://beta.openai.com/docs/api-reference/moderations/create)
- ~~Engines~~ *(deprecated)*
    - ~~[List engines](https://beta.openai.com/docs/api-reference/engines/list)~~
    - ~~[Retrieve engine](https://beta.openai.com/docs/api-reference/engines/retrieve)~~

# Need Proxy?

```go
client := openaigo.NewClient(OPENAI_API_KEY)
// You can set whatever you want
transport := &http.Transport{ Proxy: http.ProxyFromEnvironment }
client.HTTPClient = &http.Client{ Transport: transport }
// Done!
```

# Issues

Report any issue here or any feedback is welcomed.

* https://github.com/xiao333ma/openaigo/issues
