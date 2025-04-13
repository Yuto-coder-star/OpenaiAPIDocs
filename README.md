# OpenaiAPIDocs
OpenAI Responses API Docs

Developer quickstart
====================

Take your first steps with the OpenAI API.

The OpenAI API provides a simple interface to state-of-the-art AI [models](/docs/models) for text generation, natural language processing, computer vision, and more. This example generates [text output](/docs/guides/text) from a prompt, as you might using [ChatGPT](https://chatgpt.com).

Generate text from a model

```javascript
import OpenAI from "openai";
const client = new OpenAI();

const response = await client.responses.create({
    model: "gpt-4o",
    input: "Write a one-sentence bedtime story about a unicorn."
});

console.log(response.output_text);
```

```python
from openai import OpenAI
client = OpenAI()

response = client.responses.create(
    model="gpt-4o",
    input="Write a one-sentence bedtime story about a unicorn."
)

print(response.output_text)
```

```bash
curl "https://api.openai.com/v1/responses" \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -d '{
        "model": "gpt-4o",
        "input": "Write a one-sentence bedtime story about a unicorn."
    }'
```

Data retention for model responses

Response objects are saved for 30 days by default. They can be viewed in the dashboard [logs](/logs?api=responses) page or [retrieved](/docs/api-reference/responses/get) via the API. You can disable this behavior by setting `store` to `false` when creating a Response.

OpenAI does not use data sent via API to train our models without your explicit consent—[learn more](/docs/guides/your-data).

[

Configure your development environment

Install and configure an official OpenAI SDK to run the code above.

](/docs/libraries)[

Responses starter app

Start building with the Responses API

](https://github.com/openai/openai-responses-starter-app)[

Text generation and prompting

Learn more about prompting, message roles, and building conversational apps.

](/docs/guides/text)  
  

Analyze image inputs
--------------------

You can provide image inputs to the model as well. Scan receipts, analyze screenshots, or find objects in the real world with [computer vision](/docs/guides/images).

Analyze the content of an image

```javascript
import OpenAI from "openai";
const client = new OpenAI();

const response = await client.responses.create({
    model: "gpt-4o",
    input: [
        { role: "user", content: "What two teams are playing in this photo?" },
        {
            role: "user",
            content: [
                {
                    type: "input_image", 
                    image_url: "https://upload.wikimedia.org/wikipedia/commons/3/3b/LeBron_James_Layup_%28Cleveland_vs_Brooklyn_2018%29.jpg",
                }
            ],
        },
    ],
});

console.log(response.output_text);
```

```bash
curl "https://api.openai.com/v1/responses" \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -d '{
        "model": "gpt-4o",
        "input": [
            {
                "role": "user", 
                "content": "What two teams are playing in this photo?"
            },
            {
                "role": "user",
                "content": [
                    {
                        "type": "input_image", 
                        "image_url": "https://upload.wikimedia.org/wikipedia/commons/3/3b/LeBron_James_Layup_%28Cleveland_vs_Brooklyn_2018%29.jpg"
                    }
                ]
            }
        ]
    }'
```

```python
from openai import OpenAI
client = OpenAI()

response = client.responses.create(
    model="gpt-4o",
    input=[
        {"role": "user", "content": "what teams are playing in this image?"},
        {
            "role": "user",
            "content": [
                {
                    "type": "input_image",
                    "image_url": "https://upload.wikimedia.org/wikipedia/commons/3/3b/LeBron_James_Layup_%28Cleveland_vs_Brooklyn_2018%29.jpg"
                }
            ]
        }
    ]
)

print(response.output_text)
```

[

Computer vision guide

Learn to use image inputs to the model and extract meaning from images.

](/docs/guides/images)  
  

Extend the model with tools
---------------------------

Give the model access to new data and capabilities using [tools](/docs/guides/tools). You can either call your own [custom code](/docs/guides/function-calling), or use one of OpenAI's [powerful built-in tools](/docs/guides/tools). This example uses [web search](/docs/guides/tools-web-search) to give the model access to the latest information on the Internet.

Get information for the response from the Internet

```javascript
import OpenAI from "openai";
const client = new OpenAI();

const response = await client.responses.create({
    model: "gpt-4o",
    tools: [ { type: "web_search_preview" } ],
    input: "What was a positive news story from today?",
});

console.log(response.output_text);
```

```python
from openai import OpenAI
client = OpenAI()

response = client.responses.create(
    model="gpt-4o",
    tools=[{"type": "web_search_preview"}],
    input="What was a positive news story from today?"
)

print(response.output_text)
```

```bash
curl "https://api.openai.com/v1/responses" \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -d '{
        "model": "gpt-4o",
        "tools": [{"type": "web_search_preview"}],
        "input": "what was a positive news story from today?"
    }'
```

[

Use built-in tools

Learn about powerful built-in tools like web search and file search.

](/docs/guides/tools)[

Function calling guide

Learn to enable the model to call your own custom code.

](/docs/guides/function-calling)  
  

Deliver blazing fast AI experiences
-----------------------------------

Using either the new [Realtime API](/docs/guides/realtime) or server-sent [streaming events](/docs/guides/streaming-responses), you can build high performance, low-latency experiences for your users.

Stream server-sent events from the API

```javascript
import { OpenAI } from "openai";
const client = new OpenAI();

const stream = await client.responses.create({
    model: "gpt-4o",
    input: [
        {
            role: "user",
            content: "Say 'double bubble bath' ten times fast.",
        },
    ],
    stream: true,
});

for await (const event of stream) {
    console.log(event);
}
```

```python
from openai import OpenAI
client = OpenAI()

stream = client.responses.create(
    model="gpt-4o",
    input=[
        {
            "role": "user",
            "content": "Say 'double bubble bath' ten times fast.",
        },
    ],
    stream=True,
)

for event in stream:
    print(event)
```

[

Use streaming events

Use server-sent events to stream model responses to users fast.

](/docs/guides/streaming-responses)[

Get started with the Realtime API

Use WebRTC or WebSockets for super fast speech-to-speech AI apps.

](/docs/guides/realtime)  
  

Build agents
------------

Use the OpenAI platform to build [agents](/docs/guides/agents) capable of taking action—like [controlling computers](/docs/guides/tools-computer-use)—on behalf of your users. Use the [Agent SDK for Python](/docs/guides/agents-sdk) to create orchestration logic on the backend.

```python
from agents import Agent, Runner
import asyncio

spanish_agent = Agent(
    name="Spanish agent",
    instructions="You only speak Spanish.",
)

english_agent = Agent(
    name="English agent",
    instructions="You only speak English",
)

triage_agent = Agent(
    name="Triage agent",
    instructions="Handoff to the appropriate agent based on the language of the request.",
    handoffs=[spanish_agent, english_agent],
)

async def main():
    result = await Runner.run(triage_agent, input="Hola, ¿cómo estás?")
    print(result.final_output)

if __name__ == "__main__":
    asyncio.run(main())

# ¡Hola! Estoy bien, gracias por preguntar. ¿Y tú, cómo estás?
```

[

Build agents that can take action

Learn how to use the OpenAI platform to build powerful, capable AI agents.

](/docs/guides/agents)  
  

Explore further
---------------

We've barely scratched the surface of what's possible with the OpenAI platform. Here are some resources you might want to explore next.

[

Go deeper with prompting and text generation

Learn more about prompting, message roles, and building conversational apps like chat bots.

](/docs/guides/text)[

Analyze the content of images

Learn to use image inputs to the model and extract meaning from images.

](/docs/guides/images)[

Generate structured JSON data from the model

Generate JSON data from the model that conforms to a JSON schema you specify.

](/docs/guides/structured-outputs)[

Call custom code to help generate a response

Empower the model to invoke your own custom code to help generate a response. Do this to give the model access to data or systems it wouldn't be able to access otherwise.

](/docs/guides/function-calling)[

Search the web or use your own data in responses

Try out powerful built-in tools to extend the capabilities of the models. Search the web or your own data for up-to-date information the model can use to generate responses.

](/docs/guides/tools)[

Responses starter app

Start building with the Responses API

](https://github.com/openai/openai-responses-starter-app)[

Build agents

Explore interfaces to build powerful AI agents that can take action on behalf of users. Control a computer to take action on behalf of a user, or orchestrate multi-agent flows with the Agents SDK.

](/docs/guides/agents)[

Full API Reference

View the full API reference for the OpenAI platform.

](/docs/api-reference)

Was this page useful?	
Libraries
=========

Set up your development environment to use the OpenAI API with an SDK in your preferred language.

This page covers setting up your local development environment to use the [OpenAI API](/docs/api-reference). You can use one of our officially supported SDKs, a community library, or your own preferred HTTP client.

Create and export an API key
----------------------------

Before you begin, [create an API key in the dashboard](/api-keys), which you'll use to securely [access the API](/docs/api-reference/authentication). Store the key in a safe location, like a [`.zshrc` file](https://www.freecodecamp.org/news/how-do-zsh-configuration-files-work/) or another text file on your computer. Once you've generated an API key, export it as an [environment variable](https://en.wikipedia.org/wiki/Environment_variable) in your terminal.

macOS / Linux

Export an environment variable on macOS or Linux systems

```bash
export OPENAI_API_KEY="your_api_key_here"
```

Windows

Export an environment variable in PowerShell

```bash
setx OPENAI_API_KEY "your_api_key_here"
```

OpenAI SDKs are configured to automatically read your API key from the system environment.

Install an official SDK
-----------------------

JavaScript

To use the OpenAI API in server-side JavaScript environments like Node.js, Deno, or Bun, you can use the official [OpenAI SDK for TypeScript and JavaScript](https://github.com/openai/openai-node). Get started by installing the SDK using [npm](https://www.npmjs.com/) or your preferred package manager:

Install the OpenAI SDK with npm

```bash
npm install openai
```

With the OpenAI SDK installed, create a file called `example.mjs` and copy the example code into it:

Test a basic API request

```javascript
import OpenAI from "openai";
const client = new OpenAI();

const response = await client.responses.create({
    model: "gpt-4o",
    input: "Write a one-sentence bedtime story about a unicorn."
});

console.log(response.output_text);
```

Execute the code with `node example.mjs` (or the equivalent command for Deno or Bun). In a few moments, you should see the output of your API request.

[

Learn more on GitHub

Discover more SDK capabilities and options on the library's GitHub README.

](https://github.com/openai/openai-node)

Python

To use the OpenAI API in Python, you can use the official [OpenAI SDK for Python](https://github.com/openai/openai-python). Get started by installing the SDK using [pip](https://pypi.org/project/pip/):

Install the OpenAI SDK with pip

```bash
pip install openai
```

With the OpenAI SDK installed, create a file called `example.py` and copy the example code into it:

Test a basic API request

```python
from openai import OpenAI
client = OpenAI()

response = client.responses.create(
    model="gpt-4o",
    input="Write a one-sentence bedtime story about a unicorn."
)

print(response.output_text)
```

Execute the code with `python example.py`. In a few moments, you should see the output of your API request.

[

Learn more on GitHub

Discover more SDK capabilities and options on the library's GitHub README.

](https://github.com/openai/openai-python)

.NET

In collaboration with Microsoft, OpenAI provides an officially supported API client for C#. You can install it with the .NET CLI from [NuGet](https://www.nuget.org/).

```text
dotnet add package OpenAI
```

A simple API request to [Chat Completions](/docs/api-reference/chat) would look like this:

```csharp
using OpenAI.Chat;

ChatClient client = new(
  model: "gpt-4o", 
  apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

ChatCompletion completion = client.CompleteChat("Say 'this is a test.'");

Console.WriteLine($"[ASSISTANT]: {completion.Content[0].Text}");
```

To learn more about using the OpenAI API in .NET, check out the GitHub repo linked below!

[

Learn more on GitHub

Discover more SDK capabilities and options on the library's GitHub README.

](https://github.com/openai/openai-dotnet)

Java

OpenAI provides an API helper for the Java programming language, currently in beta. You can include the Maven depency using the following configuration:

```xml
<dependency>
    <groupId>com.openai</groupId>
    <artifactId>openai-java</artifactId>
    <version>0.31.0</version>
</dependency>
```

A simple API request to [Chat Completions](/docs/api-reference/chat) would look like this:

```java
import com.openai.client.OpenAIClient;
import com.openai.client.okhttp.OpenAIOkHttpClient;
import com.openai.models.ChatCompletion;
import com.openai.models.ChatCompletionCreateParams;
import com.openai.models.ChatModel;

// Configures using the `OPENAI_API_KEY`, `OPENAI_ORG_ID` and `OPENAI_PROJECT_ID` 
// environment variables
OpenAIClient client = OpenAIOkHttpClient.fromEnv();

ChatCompletionCreateParams params = ChatCompletionCreateParams.builder()
    .addUserMessage("Say this is a test")
    .model(ChatModel.O3_MINI)
    .build();
ChatCompletion chatCompletion = client.chat().completions().create(params);
```

To learn more about using the OpenAI API in Java, check out the GitHub repo linked below!

[

Learn more on GitHub

Discover more SDK capabilities and options on the library's GitHub README.

](https://github.com/openai/openai-java)

Go

OpenAI provides an API helper for the Go programming language, currently in beta. You can import the library using the code below:

```golang
import (
  "github.com/openai/openai-go" // imported as openai
)
```

A simple API request to [Chat Completions](/docs/api-reference/chat) would look like this:

```golang
package main

import (
  "context"
  "fmt"

  "github.com/openai/openai-go"
  "github.com/openai/openai-go/option"
)

func main() {
  client := openai.NewClient(
    option.WithAPIKey("My API Key"), // defaults to os.LookupEnv("OPENAI_API_KEY")
  )
  chatCompletion, err := client.Chat.Completions.New(
    context.TODO(), openai.ChatCompletionNewParams{
      Messages: openai.F(
        []openai.ChatCompletionMessageParamUnion{
          openai.UserMessage("Say this is a test"),
        }
      ),
      Model: openai.F(openai.ChatModelGPT4o),
    }
  )

  if err != nil {
    panic(err.Error())
  }

  println(chatCompletion.Choices[0].Message.Content)
}
```

To learn more about using the OpenAI API in Go, check out the GitHub repo linked below!

[

Learn more on GitHub

Discover more SDK capabilities and options on the library's GitHub README.

](https://github.com/openai/openai-go)

Azure OpenAI libraries
----------------------

Microsoft's Azure team maintains libraries that are compatible with both the OpenAI API and Azure OpenAI services. Read the library documentation below to learn how you can use them with the OpenAI API.

*   [Azure OpenAI client library for .NET](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/openai/Azure.AI.OpenAI)
*   [Azure OpenAI client library for JavaScript](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/openai/openai)
*   [Azure OpenAI client library for Java](https://github.com/Azure/azure-sdk-for-java/tree/main/sdk/openai/azure-ai-openai)
*   [Azure OpenAI client library for Go](https://github.com/Azure/azure-sdk-for-go/tree/main/sdk/ai/azopenai)

* * *

Community libraries
-------------------

The libraries below are built and maintained by the broader developer community. You can also [watch our OpenAPI specification](https://github.com/openai/openai-openapi) repository on GitHub to get timely updates on when we make changes to our API.

Please note that OpenAI does not verify the correctness or security of these projects. **Use them at your own risk!**

### C# / .NET

*   [Betalgo.OpenAI](https://github.com/betalgo/openai) by [Betalgo](https://github.com/betalgo)
*   [OpenAI-API-dotnet](https://github.com/OkGoDoIt/OpenAI-API-dotnet) by [OkGoDoIt](https://github.com/OkGoDoIt)
*   [OpenAI-DotNet](https://github.com/RageAgainstThePixel/OpenAI-DotNet) by [RageAgainstThePixel](https://github.com/RageAgainstThePixel)

### C++

*   [liboai](https://github.com/D7EAD/liboai) by [D7EAD](https://github.com/D7EAD)

### Clojure

*   [openai-clojure](https://github.com/wkok/openai-clojure) by [wkok](https://github.com/wkok)

### Crystal

*   [openai-crystal](https://github.com/sferik/openai-crystal) by [sferik](https://github.com/sferik)

### Dart/Flutter

*   [openai](https://github.com/anasfik/openai) by [anasfik](https://github.com/anasfik)

### Delphi

*   [DelphiOpenAI](https://github.com/HemulGM/DelphiOpenAI) by [HemulGM](https://github.com/HemulGM)

### Elixir

*   [openai.ex](https://github.com/mgallo/openai.ex) by [mgallo](https://github.com/mgallo)

### Go

*   [go-gpt3](https://github.com/sashabaranov/go-gpt3) by [sashabaranov](https://github.com/sashabaranov)

### Java

*   [simple-openai](https://github.com/sashirestela/simple-openai) by [Sashir Estela](https://github.com/sashirestela)
*   [Spring AI](https://spring.io/projects/spring-ai)

### Julia

*   [OpenAI.jl](https://github.com/rory-linehan/OpenAI.jl) by [rory-linehan](https://github.com/rory-linehan)

### Kotlin

*   [openai-kotlin](https://github.com/Aallam/openai-kotlin) by [Mouaad Aallam](https://github.com/Aallam)

### Node.js

*   [openai-api](https://www.npmjs.com/package/openai-api) by [Njerschow](https://github.com/Njerschow)
*   [openai-api-node](https://www.npmjs.com/package/openai-api-node) by [erlapso](https://github.com/erlapso)
*   [gpt-x](https://www.npmjs.com/package/gpt-x) by [ceifa](https://github.com/ceifa)
*   [gpt3](https://www.npmjs.com/package/gpt3) by [poteat](https://github.com/poteat)
*   [gpts](https://www.npmjs.com/package/gpts) by [thencc](https://github.com/thencc)
*   [@dalenguyen/openai](https://www.npmjs.com/package/@dalenguyen/openai) by [dalenguyen](https://github.com/dalenguyen)
*   [tectalic/openai](https://github.com/tectalichq/public-openai-client-js) by [tectalic](https://tectalic.com/)

### PHP

*   [orhanerday/open-ai](https://packagist.org/packages/orhanerday/open-ai) by [orhanerday](https://github.com/orhanerday)
*   [tectalic/openai](https://github.com/tectalichq/public-openai-client-php) by [tectalic](https://tectalic.com/)
*   [openai-php client](https://github.com/openai-php/client) by [openai-php](https://github.com/openai-php)

### Python

*   [chronology](https://github.com/OthersideAI/chronology) by [OthersideAI](https://www.othersideai.com/)

### R

*   [rgpt3](https://github.com/ben-aaron188/rgpt3) by [ben-aaron188](https://github.com/ben-aaron188)

### Ruby

*   [openai](https://github.com/nileshtrivedi/openai/) by [nileshtrivedi](https://github.com/nileshtrivedi)
*   [ruby-openai](https://github.com/alexrudall/ruby-openai) by [alexrudall](https://github.com/alexrudall)

### Rust

*   [async-openai](https://github.com/64bit/async-openai) by [64bit](https://github.com/64bit)
*   [fieri](https://github.com/lbkolev/fieri) by [lbkolev](https://github.com/lbkolev)

### Scala

*   [openai-scala-client](https://github.com/cequence-io/openai-scala-client) by [cequence-io](https://github.com/cequence-io)

### Swift

*   [AIProxySwift](https://github.com/lzell/AIProxySwift) by [Lou Zell](https://github.com/lzell)
*   [OpenAIKit](https://github.com/dylanshine/openai-kit) by [dylanshine](https://github.com/dylanshine)
*   [OpenAI](https://github.com/MacPaw/OpenAI/) by [MacPaw](https://github.com/MacPaw)

### Unity

*   [OpenAi-Api-Unity](https://github.com/hexthedev/OpenAi-Api-Unity) by [hexthedev](https://github.com/hexthedev)
*   [com.openai.unity](https://github.com/RageAgainstThePixel/com.openai.unity) by [RageAgainstThePixel](https://github.com/RageAgainstThePixel)

### Unreal Engine

*   [OpenAI-Api-Unreal](https://github.com/KellanM/OpenAI-Api-Unreal) by [KellanM](https://github.com/KellanM)

Other OpenAI repositories
-------------------------

*   [tiktoken](https://github.com/openai/tiktoken) - counting tokens
*   [simple-evals](https://github.com/openai/simple-evals) - simple evaluation library
*   [mle-bench](https://github.com/openai/mle-bench) - library to evaluate machine learning engineer agents
*   [gym](https://github.com/openai/gym) - reinforcement learning library
*   [swarm](https://github.com/openai/swarm) - educational orchestration repository

Was this page useful?
Text generation and prompting
=============================

Learn how to prompt a model to generate text.

With the OpenAI API, you can use a [large language model](/docs/models) to generate text from a prompt, as you might using [ChatGPT](https://chatgpt.com). Models can generate almost any kind of text response—like code, mathematical equations, structured JSON data, or human-like prose.

Here's a simple example using the [Responses API](/docs/api-reference/responses).

Generate text from a simple prompt

```javascript
import OpenAI from "openai";
const client = new OpenAI();

const response = await client.responses.create({
    model: "gpt-4o",
    input: "Write a one-sentence bedtime story about a unicorn."
});

console.log(response.output_text);
```

```python
from openai import OpenAI
client = OpenAI()

response = client.responses.create(
    model="gpt-4o",
    input="Write a one-sentence bedtime story about a unicorn."
)

print(response.output_text)
```

```bash
curl "https://api.openai.com/v1/responses" \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -d '{
        "model": "gpt-4o",
        "input": "Write a one-sentence bedtime story about a unicorn."
    }'
```

An array of content generated by the model is in the `output` property of the response. In this simple example, we have just one output which looks like this:

```json
[
    {
        "id": "msg_67b73f697ba4819183a15cc17d011509",
        "type": "message",
        "role": "assistant",
        "content": [
            {
                "type": "output_text",
                "text": "Under the soft glow of the moon, Luna the unicorn danced through fields of twinkling stardust, leaving trails of dreams for every child asleep.",
                "annotations": []
            }
        ]
    }
]
```

Note that the output often has more than one item!

**The `output` array often has more than one item in it!** It can contain tool calls, data about reasoning tokens generated by [reasoning models](/docs/guides/reasoning), and other items. It is not safe to assume that the model's text output is present at `output[0].content[0].text`.

Some of our [official SDKs](/docs/libraries) include an `output_text` property on model responses for convenience, which aggregates all text outputs from the model into a single string. This may be useful as a shortcut to access text output from the model.

In addition to plain text, you can also have the model return structured data in JSON format - this feature is called [**Structured Outputs**](/docs/guides/structured-outputs).

Message roles and instruction following
---------------------------------------

You can provide instructions to the model with [differing levels of authority](https://model-spec.openai.com/2025-02-12.html#chain_of_command) using the `instructions` API parameter or **message roles**.

The `instructions` parameter gives the model high-level instructions on how it should behave while generating a response, including tone, goals, and examples of correct responses. Any instructions provided this way will take priority over a prompt in the `input` parameter.

Generate text with instructions

```javascript
import OpenAI from "openai";
const client = new OpenAI();

const response = await client.responses.create({
    model: "gpt-4o",
    instructions: "Talk like a pirate.",
    input: "Are semicolons optional in JavaScript?",
});

console.log(response.output_text);
```

```python
from openai import OpenAI
client = OpenAI()

response = client.responses.create(
    model="gpt-4o",
    instructions="Talk like a pirate.",
    input="Are semicolons optional in JavaScript?",
)

print(response.output_text)
```

```bash
curl "https://api.openai.com/v1/responses" \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -d '{
        "model": "gpt-4o",
        "instructions": "Talk like a pirate.",
        "input": "Are semicolons optional in JavaScript?"
    }'
```

The example above is roughly equivalent to using the following input messages in the `input` array:

Generate text with messages using different roles

```javascript
import OpenAI from "openai";
const client = new OpenAI();

const response = await client.responses.create({
    model: "gpt-4o",
    input: [
        {
            role: "developer",
            content: "Talk like a pirate."
        },
        {
            role: "user",
            content: "Are semicolons optional in JavaScript?",
        },
    ],
});

console.log(response.output_text);
```

```python
from openai import OpenAI
client = OpenAI()

response = client.responses.create(
    model="gpt-4o",
    input=[
        {
            "role": "developer",
            "content": "Talk like a pirate."
        },
        {
            "role": "user",
            "content": "Are semicolons optional in JavaScript?"
        }
    ]
)

print(response.output_text)
```

```bash
curl "https://api.openai.com/v1/responses" \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -d '{
        "model": "gpt-4o",
        "input": [
            {
                "role": "developer",
                "content": "Talk like a pirate."
            },
            {
                "role": "user",
                "content": "Are semicolons optional in JavaScript?"
            }
        ]
    }'
```

Instructions versus developer messages in multi-turn conversations

Note that the `instructions` parameter only applies to the current response generation request. If you are [managing conversation state](/docs/guides/conversation-state) with the `previous_response_id` parameter, the `instructions` used on previous turns will not be present in the context. If you'd like to persist the same model instructions across turns, use a `developer` message instead.

The [OpenAI model spec](https://model-spec.openai.com/2025-02-12.html#chain_of_command) describes how our models give different levels of priority to messages with different roles.

|developer|user|assistant|
|---|---|---|
|developer messages are instructions provided by the application developer, weighted ahead of user messages.|user messages are instructions provided by an end user, weighted behind developer messages.|Messages generated by the model have the assistant role.|

A multi-turn conversation may consist of several messages of these types, along with other content types provided by both you and the model. Learn more about [managing conversation state here](/docs/guides/conversation-state).

Choosing a model
----------------

A key choice to make when generating content through the API is which model you want to use - the `model` parameter of the code samples above. [You can find a full listing of available models here](/docs/models).

### Which model should I choose?

Here are a few factors to consider when choosing a model for text generation.

*   **[Reasoning models](/docs/guides/reasoning)** generate an internal chain of thought to analyze the input prompt, and excel at understanding complex tasks and multi-step planning. They are also generally slower and more expensive to use than GPT models.
*   **GPT models** are fast, cost-efficient, and highly intelligent, but benefit from more explicit instructions around how to accomplish tasks.
*   **Large and small (mini) models** offer trade-offs for speed, cost, and intelligence. Large models are more effective at understanding prompts and solving problems across domains, while small models are generally faster and cheaper to use. Small models like GPT-4o mini can also be trained to excel at a specific task through [fine tuning](/docs/guides/fine-tuning) and [distillation](/docs/guides/distillation) of results from larger models.

When in doubt, `gpt-4o` offers a solid combination of intelligence, speed, and cost effectiveness.

Prompt engineering
------------------

Creating effective instructions for a model to generate content is a process known as **prompt engineering**. Because the content generated from a model is non-deterministic, it is a combination of art and science to build a prompt that will generate the right kind of content from a model. You can find a more complete exploration of [prompt engineering here](/docs/guides/prompt-engineering), but here are some general guidelines:

*   Be detailed in your instructions to the model to eliminate ambiguity in how you want the model to respond.
*   Provide examples to the model of the type of inputs you expect, and the type of outputs you would want for that input - this technique is called **few-shot learning**.
*   When using a [reasoning model](/docs/guides/reasoning), describe the task to be done in terms of goals and desired outcomes, rather than specific step-by-step instructions of how to accomplish a task.
*   Invest in creating [evaluations (evals)](/docs/guides/evals) for your prompts, using test data that looks like the data you expect to see in production. Due to the inherent variable results from different models, using evals to see how your prompts perform is the best way to ensure your prompts work as expected.

Iterating on prompts is often all you need to do to get great results from a model, but you can also explore [fine tuning](/docs/guides/fine-tuning) to customize base models for a particular use case.

Next steps
----------

Now that you known the basics of text inputs and outputs, you might want to check out one of these resources next.

[

Build a prompt in the Playground

Use the Playground to develop and iterate on prompts.

](/playground)[

Generate JSON data with Structured Outputs

Ensure JSON data emitted from a model conforms to a JSON schema.

](/docs/guides/structured-outputs)[

Full API reference

Check out all the options for text generation in the API reference.

](/docs/api-reference/responses)

Was this page useful?
Images and vision
=================

Learn how to use vision capabilities to understand images.

**Vision** is the ability to use images as input prompts to a model, and generate responses based on the data inside those images. Find out which models are capable of vision [on the models page](/docs/models). To generate images as _output_, see our [specialized model for image generation](/docs/guides/image-generation).

You can provide images as input to generation requests either by providing a fully qualified URL to an image file, or providing an image as a Base64-encoded data URL.

Passing a URL

Analyze the content of an image

```javascript
import OpenAI from "openai";

const openai = new OpenAI();

const response = await openai.responses.create({
    model: "gpt-4o-mini",
    input: [{
        role: "user",
        content: [
            { type: "input_text", text: "what's in this image?" },
            {
                type: "input_image",
                image_url: "https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Gfp-wisconsin-madison-the-nature-boardwalk.jpg/2560px-Gfp-wisconsin-madison-the-nature-boardwalk.jpg",
            },
        ],
    }],
});

console.log(response.output_text);
```

```python
from openai import OpenAI

client = OpenAI()

response = client.responses.create(
    model="gpt-4o-mini",
    input=[{
        "role": "user",
        "content": [
            {"type": "input_text", "text": "what's in this image?"},
            {
                "type": "input_image",
                "image_url": "https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Gfp-wisconsin-madison-the-nature-boardwalk.jpg/2560px-Gfp-wisconsin-madison-the-nature-boardwalk.jpg",
            },
        ],
    }],
)

print(response.output_text)
```

```bash
curl https://api.openai.com/v1/responses \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "gpt-4o-mini",
    "input": [
      {
        "role": "user",
        "content": [
          {"type": "input_text", "text": "what is in this image?"},
          {
            "type": "input_image",
            "image_url": "https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Gfp-wisconsin-madison-the-nature-boardwalk.jpg/2560px-Gfp-wisconsin-madison-the-nature-boardwalk.jpg"
          }
        ]
      }
    ]
  }'
```

Passing a Base64 encoded image

Analyze the content of an image

```javascript
import fs from "fs";
import OpenAI from "openai";

const openai = new OpenAI();

const imagePath = "path_to_your_image.jpg";
const base64Image = fs.readFileSync(imagePath, "base64");

const response = await openai.responses.create({
    model: "gpt-4o-mini",
    input: [
        {
            role: "user",
            content: [
                { type: "input_text", text: "what's in this image?" },
                {
                    type: "input_image",
                    image_url: `data:image/jpeg;base64,${base64Image}`,
                },
            ],
        },
    ],
});

console.log(response.output_text);
```

```python
import base64
from openai import OpenAI

client = OpenAI()

# Function to encode the image
def encode_image(image_path):
    with open(image_path, "rb") as image_file:
        return base64.b64encode(image_file.read()).decode("utf-8")

# Path to your image
image_path = "path_to_your_image.jpg"

# Getting the Base64 string
base64_image = encode_image(image_path)

response = client.responses.create(
    model="gpt-4o",
    input=[
        {
            "role": "user",
            "content": [
                { "type": "input_text", "text": "what's in this image?" },
                {
                    "type": "input_image",
                    "image_url": f"data:image/jpeg;base64,{base64_image}",
                },
            ],
        }
    ],
)

print(response.output_text)
```

Image input requirements
------------------------

Input images must meet the following requirements to be used in the API.

||
|PNG (.png)JPEG (.jpeg and .jpg)WEBP (.webp)Non-animated GIF (.gif)|Up to 20MB per imageLow-resolution: 512px x 512pxHigh-resolution: 768px (short side) x 2000px (long side)|No watermarks or logosNo textNo NSFW contentClear enough for a human to understand|

Specify image input detail level
--------------------------------

The `detail` parameter tells the model what level of detail to use when processing and understanding the image (`low`, `high`, or `auto` to let the model decide). If you skip the parameter, the model will use `auto`. Put it right after your `image_url`, like this:

```plain
{
    "type": "input_image",
    "image_url": "https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Gfp-wisconsin-madison-the-nature-boardwalk.jpg/2560px-Gfp-wisconsin-madison-the-nature-boardwalk.jpg",
    "detail": "high",
}
```

You can save tokens and speed up responses by using `"detail": "low"`. This lets the model process the image with a budget of 85 tokens. The model receives a low-resolution 512px x 512px version of the image. This is fine if your use case doesn't require the model to see with high-resolution detail (for example, if you're asking about the dominant shape or color in the image).

Or give the model more detail to generate its understanding by using `"detail": "high"`. This lets the model see the low-resolution image (using 85 tokens) and then creates detailed crops using 170 tokens for each 512px x 512px tile.

Note that the above token budgets for image processing do not currently apply to the GPT-4o mini model, but the image processing cost is comparable to GPT-4o. For the most precise and up-to-date estimates for image processing, please use the image pricing calculator [here](https://openai.com/api/pricing/)

Provide multiple image inputs
-----------------------------

The [Responses API](https://platform.openai.com/docs/api-reference/responses) can take in and process multiple image inputs. The model processes each image and uses information from all images to answer the question.

Multiple image inputs

```javascript
import OpenAI from "openai";

const openai = new OpenAI();

const response = await openai.responses.create({
  model: "gpt-4o-mini",
  input: [
    {
      role: "user",
      content: [
        { type: "input_text", text: "What are in these images? Is there any difference between them?" },
        {
          type: "input_image",
          image_url: "https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Gfp-wisconsin-madison-the-nature-boardwalk.jpg/2560px-Gfp-wisconsin-madison-the-nature-boardwalk.jpg",
        },
        {
          type: "input_image",
          image_url: "https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Gfp-wisconsin-madison-the-nature-boardwalk.jpg/2560px-Gfp-wisconsin-madison-the-nature-boardwalk.jpg",
        }
      ],
    },
  ]
});

console.log(response.output_text);
```

```python
from openai import OpenAI

client = OpenAI()

response = client.responses.create(
    model="gpt-4o-mini",
    input=[
        {
            "role": "user",
            "content": [
                {
                    "type": "input_text",
                    "text": "What are in these images? Is there any difference between them?",
                },
                {
                    "type": "input_image",
                    "image_url": "https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Gfp-wisconsin-madison-the-nature-boardwalk.jpg/2560px-Gfp-wisconsin-madison-the-nature-boardwalk.jpg",
                },
                {
                    "type": "input_image",
                    "image_url": "https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Gfp-wisconsin-madison-the-nature-boardwalk.jpg/2560px-Gfp-wisconsin-madison-the-nature-boardwalk.jpg",
                },
            ],
        }
    ]
)

print(response.output_text)
```

```bash
curl https://api.openai.com/v1/responses \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "gpt-4o-mini",
    "input": [
      {
        "role": "user",
        "content": [
          {
            "type": "input_text",
            "text": "What are in these images? Is there any difference between them?"
          },
          {
            "type": "input_image",
            "image_url": "https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Gfp-wisconsin-madison-the-nature-boardwalk.jpg/2560px-Gfp-wisconsin-madison-the-nature-boardwalk.jpg"
          },
          {
            "type": "input_image",
            "image_url": "https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Gfp-wisconsin-madison-the-nature-boardwalk.jpg/2560px-Gfp-wisconsin-madison-the-nature-boardwalk.jpg"
          }
        ]
      }
    ]
  }'
```

Here, the model is shown two copies of the same image. It can answer questions about both images or each image independently.

Limitations
-----------

While models with vision capabilities are powerful and can be used in many situations, it's important to understand the limitations of these models. Here are some known limitations:

*   **Medical images**: The model is not suitable for interpreting specialized medical images like CT scans and shouldn't be used for medical advice.
*   **Non-English**: The model may not perform optimally when handling images with text of non-Latin alphabets, such as Japanese or Korean.
*   **Small text**: Enlarge text within the image to improve readability, but avoid cropping important details.
*   **Rotation**: The model may misinterpret rotated or upside-down text and images.
*   **Visual elements**: The model may struggle to understand graphs or text where colors or styles—like solid, dashed, or dotted lines—vary.
*   **Spatial reasoning**: The model struggles with tasks requiring precise spatial localization, such as identifying chess positions.
*   **Accuracy**: The model may generate incorrect descriptions or captions in certain scenarios.
*   **Image shape**: The model struggles with panoramic and fisheye images.
*   **Metadata and resizing**: The model doesn't process original file names or metadata, and images are resized before analysis, affecting their original dimensions.
*   **Counting**: The model may give approximate counts for objects in images.
*   **CAPTCHAS**: For safety reasons, our system blocks the submission of CAPTCHAs.

Calculating costs
-----------------

Image inputs are metered and charged in tokens, just as text inputs are. The token cost of an image is determined by two factors: size and detail.

Any image with `"detail": "low"` costs 85 tokens. To calculate the cost of an image with `"detail": "high"`, we do the following:

*   Scale to fit in a 2048px x 2048px square, maintaining original aspect ratio
*   Scale so that the image's shortest side is 768px long
*   Count the number of 512px squares in the image—each square costs **170 tokens**
*   Add **85 tokens** to the total

### Cost calculation examples

*   A 1024 x 1024 square image in `"detail": "high"` mode costs 765 tokens
    *   1024 is less than 2048, so there is no initial resize.
    *   The shortest side is 1024, so we scale the image down to 768 x 768.
    *   4 512px square tiles are needed to represent the image, so the final token cost is `170 * 4 + 85 = 765`.
*   A 2048 x 4096 image in `"detail": "high"` mode costs 1105 tokens
    *   We scale down the image to 1024 x 2048 to fit within the 2048 square.
    *   The shortest side is 1024, so we further scale down to 768 x 1536.
    *   6 512px tiles are needed, so the final token cost is `170 * 6 + 85 = 1105`.
*   A 4096 x 8192 image in `"detail": "low"` most costs 85 tokens
    *   Regardless of input size, low detail images are a fixed cost.

We process images at the token level, so each image we process counts towards your tokens per minute (TPM) limit. See the calculating costs section for details on the formula used to determine token count per image.

Was this page useful?
Audio and speech
================

Explore audio and speech features in the OpenAI API.

The OpenAI API provides a range of audio capabilities. If you know what you want to build, find your use case below to get started. If you're not sure where to start, read this page as an overview.

Build with audio
----------------

[

![Build voice agents](https://cdn.openai.com/API/docs/images/voice-agents-rounded.png)

Build voice agents

Build interactive voice-driven applications.

](/docs/guides/voice-agents)[

![Transcribe audio](https://cdn.openai.com/API/docs/images/stt-rounded.png)

Transcribe audio

Convert speech to text instantly and accurately.

](/docs/guides/speech-to-text)[

![Speak text](https://cdn.openai.com/API/docs/images/tts-rounded.png)

Speak text

Turn text into natural-sounding speech in real time.

](/docs/guides/text-to-speech)

A tour of audio use cases
-------------------------

LLMs can process audio by using sound as input, creating sound as output, or both. OpenAI has several API endpoints that help you build audio applications or voice agents.

### Voice agents

Voice agents understand audio to handle tasks and respond back in natural language. There are two main ways to approach voice agents: either with speech-to-speech models and the [Realtime API](/docs/guides/realtime), or by chaining together a speech-to-text model, a text language model to process the request, and a text-to-speech model to respond. Speech-to-speech is lower latency and more natural, but chaining together a voice agent is a reliable way to extend a text-based agent into a voice agent. If you are already using the [Agents SDK](/docs/guides/agents), you can [extend your existing agents with voice capabilities](https://openai.github.io/openai-agents-python/voice/quickstart/) using the chained approach.

### Streaming audio

Process audio in real time to build voice agents and other low-latency applications, including transcription use cases. You can stream audio in and out of a model with the [Realtime API](/docs/guides/realtime). Our advanced speech models provide automatic speech recognition for improved accuracy, low-latency interactions, and multilingual support.

### Text to speech

For turning text into speech, use the [Audio API](/docs/api-reference/audio/) `audio/speech` endpoint. Models compatible with this endpoint are `gpt-4o-mini-tts`, `tts-1`, and `tts-1-hd`. With `gpt-4o-mini-tts`, you can ask the model to speak a certain way or with a certain tone of voice.

### Speech to text

For speech to text, use the [Audio API](/docs/api-reference/audio/) `audio/transcriptions` endpoint. Models compatible with this endpoint are `gpt-4o-transcribe`, `gpt-4o-mini-transcribe`, and `whisper-1`. With streaming, you can continuously pass in audio and get a continuous stream of text back.

Choosing the right API
----------------------

There are multiple APIs for transcribing or generating audio:

|API|Supported modalities|Streaming support|
|---|---|---|
|Realtime API|Audio and text inputs and outputs|Audio streaming in and out|
|Chat Completions API|Audio and text inputs and outputs|Audio streaming out|
|Transcription API|Audio inputs|Audio streaming out|
|Speech API|Text inputs and audio outputs|Audio streaming out|

### General use APIs vs. specialized APIs

The main distinction is general use APIs vs. specialized APIs. With the Realtime and Chat Completions APIs, you can use our latest models' native audio understanding and generation capabilities and combine them with other features like function calling. These APIs can be used for a wide range of use cases, and you can select the model you want to use.

On the other hand, the Transcription, Translation and Speech APIs are specialized to work with specific models and only meant for one purpose.

### Talking with a model vs. controlling the script

Another way to select the right API is asking yourself how much control you need. To design conversational interactions, where the model thinks and responds in speech, use the Realtime or Chat Completions API, depending if you need low-latency or not.

You won't know exactly what the model will say ahead of time, as it will generate audio responses directly, but the conversation will feel natural.

For more control and predictability, you can use the Speech-to-text / LLM / Text-to-speech pattern, so you know exactly what the model will say and can control the response. Please note that with this method, there will be added latency.

This is what the Audio APIs are for: pair an LLM with the `audio/transcriptions` and `audio/speech` endpoints to take spoken user input, process and generate a text response, and then convert that to speech that the user can hear.

### Recommendations

*   If you need [real-time interactions](/docs/guides/realtime-conversations) or [transcription](/docs/guides/realtime-transcription), use the Realtime API.
*   If realtime is not a requirement but you're looking to build a [voice agent](/docs/guides/voice-agents) or an audio-based application that requires features such as [function calling](/docs/guides/function-calling), use the Chat Completions API.
*   For use cases with one specific purpose, use the Transcription, Translation, or Speech APIs.

Add audio to your existing application
--------------------------------------

Models such as GPT-4o or GPT-4o mini are natively multimodal, meaning they can understand and generate multiple modalities as input and output.

If you already have a text-based LLM application with the [Chat Completions endpoint](/docs/api-reference/chat/), you may want to add audio capabilities. For example, if your chat application supports text input, you can add audio input and output—just include `audio` in the `modalities` array and use an audio model, like `gpt-4o-audio-preview`.

Audio is not yet supported in the [Responses API](/docs/api-reference/chat/completions/responses).

Audio output from model

Create a human-like audio response to a prompt

```javascript
import { writeFileSync } from "node:fs";
import OpenAI from "openai";

const openai = new OpenAI();

// Generate an audio response to the given prompt
const response = await openai.chat.completions.create({
  model: "gpt-4o-audio-preview",
  modalities: ["text", "audio"],
  audio: { voice: "alloy", format: "wav" },
  messages: [
    {
      role: "user",
      content: "Is a golden retriever a good family dog?"
    }
  ],
  store: true,
});

// Inspect returned data
console.log(response.choices[0]);

// Write audio data to a file
writeFileSync(
  "dog.wav",
  Buffer.from(response.choices[0].message.audio.data, 'base64'),
  { encoding: "utf-8" }
);
```

```python
import base64
from openai import OpenAI

client = OpenAI()

completion = client.chat.completions.create(
    model="gpt-4o-audio-preview",
    modalities=["text", "audio"],
    audio={"voice": "alloy", "format": "wav"},
    messages=[
        {
            "role": "user",
            "content": "Is a golden retriever a good family dog?"
        }
    ]
)

print(completion.choices[0])

wav_bytes = base64.b64decode(completion.choices[0].message.audio.data)
with open("dog.wav", "wb") as f:
    f.write(wav_bytes)
```

```bash
curl "https://api.openai.com/v1/chat/completions" \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -d '{
      "model": "gpt-4o-audio-preview",
      "modalities": ["text", "audio"],
      "audio": { "voice": "alloy", "format": "wav" },
      "messages": [
        {
          "role": "user",
          "content": "Is a golden retriever a good family dog?"
        }
      ]
    }'
```

Audio input to model

Use audio inputs for prompting a model

```javascript
import OpenAI from "openai";
const openai = new OpenAI();

// Fetch an audio file and convert it to a base64 string
const url = "https://cdn.openai.com/API/docs/audio/alloy.wav";
const audioResponse = await fetch(url);
const buffer = await audioResponse.arrayBuffer();
const base64str = Buffer.from(buffer).toString("base64");

const response = await openai.chat.completions.create({
  model: "gpt-4o-audio-preview",
  modalities: ["text", "audio"],
  audio: { voice: "alloy", format: "wav" },
  messages: [
    {
      role: "user",
      content: [
        { type: "text", text: "What is in this recording?" },
        { type: "input_audio", input_audio: { data: base64str, format: "wav" }}
      ]
    }
  ],
  store: true,
});

console.log(response.choices[0]);
```

```python
import base64
import requests
from openai import OpenAI

client = OpenAI()

# Fetch the audio file and convert it to a base64 encoded string
url = "https://cdn.openai.com/API/docs/audio/alloy.wav"
response = requests.get(url)
response.raise_for_status()
wav_data = response.content
encoded_string = base64.b64encode(wav_data).decode('utf-8')

completion = client.chat.completions.create(
    model="gpt-4o-audio-preview",
    modalities=["text", "audio"],
    audio={"voice": "alloy", "format": "wav"},
    messages=[
        {
            "role": "user",
            "content": [
                { 
                    "type": "text",
                    "text": "What is in this recording?"
                },
                {
                    "type": "input_audio",
                    "input_audio": {
                        "data": encoded_string,
                        "format": "wav"
                    }
                }
            ]
        },
    ]
)

print(completion.choices[0].message)
```

```bash
curl "https://api.openai.com/v1/chat/completions" \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -d '{
      "model": "gpt-4o-audio-preview",
      "modalities": ["text", "audio"],
      "audio": { "voice": "alloy", "format": "wav" },
      "messages": [
        {
          "role": "user",
          "content": [
            { "type": "text", "text": "What is in this recording?" },
            { 
              "type": "input_audio", 
              "input_audio": { 
                "data": "<base64 bytes here>", 
                "format": "wav" 
              }
            }
          ]
        }
      ]
    }'
```

Was this page useful?
Structured Outputs
==================

Ensure responses adhere to a JSON schema.

Try it out
----------

Try it out in the [Playground](/playground) or generate a ready-to-use schema definition to experiment with structured outputs.

Generate

Introduction
------------

JSON is one of the most widely used formats in the world for applications to exchange data.

Structured Outputs is a feature that ensures the model will always generate responses that adhere to your supplied [JSON Schema](https://json-schema.org/overview/what-is-jsonschema), so you don't need to worry about the model omitting a required key, or hallucinating an invalid enum value.

Some benefits of Structured Outputs include:

1.  **Reliable type-safety:** No need to validate or retry incorrectly formatted responses
2.  **Explicit refusals:** Safety-based model refusals are now programmatically detectable
3.  **Simpler prompting:** No need for strongly worded prompts to achieve consistent formatting

Getting a structured response

```javascript
import OpenAI from "openai";

const openai = new OpenAI();

const response = await openai.responses.create({
  model: "gpt-4o-2024-08-06",
  input: [
    {"role": "system", "content": "Extract the event information."},
    {"role": "user", "content": "Alice and Bob are going to a science fair on Friday."}
  ],
  text: {
    format: {
      type: "json_schema",
      name: "calendar_event",
      schema: {
        type: "object",
        properties: {
          name: { 
            type: "string" 
          },
          date: { 
            type: "string" 
          },
          participants: { 
            type: "array", 
            items: { 
              type: "string" 
            } 
          },
        },
        required: ["name", "date", "participants"],
        additionalProperties: false,
      },
    }
  }
});

const event = JSON.parse(response.output_text);
```

```python
from openai import OpenAI
import json

client = OpenAI()

response = client.responses.create(
    model="gpt-4o-2024-08-06",
    input=[
        {"role": "system", "content": "Extract the event information."},
        {"role": "user", "content": "Alice and Bob are going to a science fair on Friday."}
    ],
    text={
        "format": {
            "type": "json_schema",
            "name": "calendar_event",
            "schema": {
                "type": "object",
                "properties": {
                    "name": {
                        "type": "string"
                    },
                    "date": {
                        "type": "string"
                    },
                    "participants": {
                        "type": "array", 
                        "items": {
                            "type": "string"
                        }
                    },
                },
                "required": ["name", "date", "participants"],
                "additionalProperties": False
            },
            "strict": True
        }
    }
)

event = json.loads(response.output_text)
```

### Supported models

Structured Outputs is available in our [latest large language models](/docs/models), starting with GPT-4o:

*   `gpt-4.5-preview-2025-02-27` and later
*   `o3-mini-2025-1-31` and later
*   `o1-2024-12-17` and later
*   `gpt-4o-mini-2024-07-18` and later
*   `gpt-4o-2024-08-06` and later

Older models like `gpt-4-turbo` and earlier may use [JSON mode](#json-mode) instead.

When to use Structured Outputs via function calling vs via text.format
----------------------------------------------------------------------

Structured Outputs is available in two forms in the OpenAI API:

1.  When using [function calling](/docs/guides/function-calling)
2.  When using a `json_schema` response format

Function calling is useful when you are building an application that bridges the models and functionality of your application.

For example, you can give the model access to functions that query a database in order to build an AI assistant that can help users with their orders, or functions that can interact with the UI.

Conversely, Structured Outputs via `response_format` are more suitable when you want to indicate a structured schema for use when the model responds to the user, rather than when the model calls a tool.

For example, if you are building a math tutoring application, you might want the assistant to respond to your user using a specific JSON Schema so that you can generate a UI that displays different parts of the model's output in distinct ways.

Put simply:

*   If you are connecting the model to tools, functions, data, etc. in your system, then you should use function calling
*   If you want to structure the model's output when it responds to the user, then you should use a structured `text.format`

The remainder of this guide will focus on non-function calling use cases in the Responses API. To learn more about how to use Structured Outputs with function calling, check out the [Function Calling](/docs/guides/function-calling#function-calling-with-structured-outputs) guide.

### Structured Outputs vs JSON mode

Structured Outputs is the evolution of [JSON mode](#json-mode). While both ensure valid JSON is produced, only Structured Outputs ensure schema adherance. Both Structured Outputs and JSON mode are supported in the Responses API,Chat Completions API, Assistants API, Fine-tuning API and Batch API.

We recommend always using Structured Outputs instead of JSON mode when possible.

However, Structured Outputs with `response_format: {type: "json_schema", ...}` is only supported with the `gpt-4o-mini`, `gpt-4o-mini-2024-07-18`, and `gpt-4o-2024-08-06` model snapshots and later.

||Structured Outputs|JSON Mode|
|---|---|---|
|Outputs valid JSON|Yes|Yes|
|Adheres to schema|Yes (see supported schemas)|No|
|Compatible models|gpt-4o-mini, gpt-4o-2024-08-06, and later|gpt-3.5-turbo, gpt-4-* and gpt-4o-* models|
|Enabling|text: { format: { type: "json_schema", "strict": true, "schema": ... } }|text: { format: { type: "json_object" } }|

Examples
--------

Chain of thought

### Chain of thought

You can ask the model to output an answer in a structured, step-by-step way, to guide the user through the solution.

Structured Outputs for chain-of-thought math tutoring

```javascript
import OpenAI from "openai";

const openai = new OpenAI();

const response = await openai.responses.create({
    model: "gpt-4o-2024-08-06",
    input: [
        {
            role: "system",
            content:
                "You are a helpful math tutor. Guide the user through the solution step by step.",
        },
        { role: "user", content: "how can I solve 8x + 7 = -23" },
    ],
    text: {
        format: {
            type: "json_schema",
            name: "math_reasoning",
            schema: {
                type: "object",
                properties: {
                    steps: {
                        type: "array",
                        items: {
                            type: "object",
                            properties: {
                                explanation: { type: "string" },
                                output: { type: "string" },
                            },
                            required: ["explanation", "output"],
                            additionalProperties: false,
                        },
                    },
                    final_answer: { type: "string" },
                },
                required: ["steps", "final_answer"],
                additionalProperties: false,
            },
            strict: true,
        },
    },
});

const math_reasoning = JSON.parse(response.output_text);
```

```python
import json
from openai import OpenAI

client = OpenAI()

response = client.responses.create(
    model="gpt-4o-2024-08-06",
    input=[
        {"role": "system", "content": "You are a helpful math tutor. Guide the user through the solution step by step."},
        {"role": "user", "content": "how can I solve 8x + 7 = -23"}
    ],
    text={
        "format": {
            "type": "json_schema",
            "name": "math_reasoning",
            "schema": {
                "type": "object",
                "properties": {
                    "steps": {
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {
                                "explanation": { "type": "string" },
                                "output": { "type": "string" }
                            },
                            "required": ["explanation", "output"],
                            "additionalProperties": False
                        }
                    },
                    "final_answer": { "type": "string" }
                },
                "required": ["steps", "final_answer"],
                "additionalProperties": False
            },
            "strict": True
        }
    }
)

math_reasoning = json.loads(response.output_text)
```

```bash
curl https://api.openai.com/v1/responses \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-4o-2024-08-06",
    "input": [
      {
        "role": "system",
        "content": "You are a helpful math tutor. Guide the user through the solution step by step."
      },
      {
        "role": "user",
        "content": "how can I solve 8x + 7 = -23"
      }
    ],
    "text": {
      "format": {
        "type": "json_schema",
        "name": "math_reasoning",
        "schema": {
          "type": "object",
          "properties": {
            "steps": {
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "explanation": { "type": "string" },
                  "output": { "type": "string" }
                },
                "required": ["explanation", "output"],
                "additionalProperties": false
              }
            },
            "final_answer": { "type": "string" }
          },
          "required": ["steps", "final_answer"],
          "additionalProperties": false
        },
        "strict": true
      }
    }
  }'
```

#### Example response

```json
{
  "steps": [
    {
      "explanation": "Start with the equation 8x + 7 = -23.",
      "output": "8x + 7 = -23"
    },
    {
      "explanation": "Subtract 7 from both sides to isolate the term with the variable.",
      "output": "8x = -23 - 7"
    },
    {
      "explanation": "Simplify the right side of the equation.",
      "output": "8x = -30"
    },
    {
      "explanation": "Divide both sides by 8 to solve for x.",
      "output": "x = -30 / 8"
    },
    {
      "explanation": "Simplify the fraction.",
      "output": "x = -15 / 4"
    }
  ],
  "final_answer": "x = -15 / 4"
}
```

Structured data extraction

### Structured data extraction

You can define structured fields to extract from unstructured input data, such as research papers.

Extracting data from research papers using Structured Outputs

```javascript
import OpenAI from "openai";

const openai = new OpenAI();

const response = await openai.responses.create({
    model: "gpt-4o-2024-08-06",
    input: [
        {
            role: "system",
            content:
                "You are an expert at structured data extraction. You will be given unstructured text from a research paper and should convert it into the given structure.",
        },
        { role: "user", content: "..." },
    ],
    text: {
        format: {
            type: "json_schema",
            name: "research_paper_extraction",
            schema: {
                type: "object",
                properties: {
                    title: { type: "string" },
                    authors: {
                        type: "array",
                        items: { type: "string" },
                    },
                    abstract: { type: "string" },
                    keywords: {
                        type: "array",
                        items: { type: "string" },
                    },
                },
                required: ["title", "authors", "abstract", "keywords"],
                additionalProperties: false,
            },
            strict: true,
        },
    },
});

const research_paper = JSON.parse(response.output_text);
```

```python
import json
from openai import OpenAI

client = OpenAI()

response = client.responses.create(
    model="gpt-4o-2024-08-06",
    input=[
        {"role": "system", "content": "You are an expert at structured data extraction. You will be given unstructured text from a research paper and should convert it into the given structure."},
        {"role": "user", "content": "..."}
    ],
    text={
        "format": {
              "type": "json_schema",
              "name": "research_paper_extraction",
              "schema": {
                "type": "object",
                "properties": {
                    "title": { "type": "string" },
                    "authors": { 
                        "type": "array",
                        "items": { "type": "string" }
                    },
                    "abstract": { "type": "string" },
                    "keywords": { 
                        "type": "array", 
                        "items": { "type": "string" }
                    }
                },
                "required": ["title", "authors", "abstract", "keywords"],
                "additionalProperties": False
            },
            "strict": True
        },
    },
)

research_paper = json.loads(response.output_text)
```

```bash
curl https://api.openai.com/v1/responses \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-4o-2024-08-06",
    "input": [
      {
        "role": "system",
        "content": "You are an expert at structured data extraction. You will be given unstructured text from a research paper and should convert it into the given structure."
      },
      {
        "role": "user",
        "content": "..."
      }
    ],
    "text": {
      "format": {
        "type": "json_schema",
        "name": "research_paper_extraction",
        "schema": {
          "type": "object",
          "properties": {
            "title": { "type": "string" },
            "authors": {
              "type": "array",
              "items": { "type": "string" }
            },
            "abstract": { "type": "string" },
            "keywords": {
              "type": "array",
              "items": { "type": "string" }
            }
          },
          "required": ["title", "authors", "abstract", "keywords"],
          "additionalProperties": false
        },
        "strict": true
      }
    }
  }'
```

#### Example response

```json
{
  "title": "Application of Quantum Algorithms in Interstellar Navigation: A New Frontier",
  "authors": [
    "Dr. Stella Voyager",
    "Dr. Nova Star",
    "Dr. Lyra Hunter"
  ],
  "abstract": "This paper investigates the utilization of quantum algorithms to improve interstellar navigation systems. By leveraging quantum superposition and entanglement, our proposed navigation system can calculate optimal travel paths through space-time anomalies more efficiently than classical methods. Experimental simulations suggest a significant reduction in travel time and fuel consumption for interstellar missions.",
  "keywords": [
    "Quantum algorithms",
    "interstellar navigation",
    "space-time anomalies",
    "quantum superposition",
    "quantum entanglement",
    "space travel"
  ]
}
```

UI generation

### UI Generation

You can generate valid HTML by representing it as recursive data structures with constraints, like enums.

Generating HTML using Structured Outputs

```javascript
import OpenAI from "openai";

const openai = new OpenAI();

const response = await openai.responses.create({
    model: "gpt-4o-2024-08-06",
    input: [
        {
            role: "system",
            content:
                "You are a UI generator AI. Convert the user input into a UI.",
        },
        {
            role: "user",
            content: "Make a User Profile Form",
        },
    ],
    text: {
        format: {
            type: "json_schema",
            name: "ui",
            description: "Dynamically generated UI",
            schema: {
                type: "object",
                properties: {
                    type: {
                        type: "string",
                        description: "The type of the UI component",
                        enum: [
                            "div",
                            "button",
                            "header",
                            "section",
                            "field",
                            "form",
                        ],
                    },
                    label: {
                        type: "string",
                        description:
                            "The label of the UI component, used for buttons or form fields",
                    },
                    children: {
                        type: "array",
                        description: "Nested UI components",
                        items: { $ref: "#" },
                    },
                    attributes: {
                        type: "array",
                        description:
                            "Arbitrary attributes for the UI component, suitable for any element",
                        items: {
                            type: "object",
                            properties: {
                                name: {
                                    type: "string",
                                    description:
                                        "The name of the attribute, for example onClick or className",
                                },
                                value: {
                                    type: "string",
                                    description: "The value of the attribute",
                                },
                            },
                            required: ["name", "value"],
                            additionalProperties: false,
                        },
                    },
                },
                required: ["type", "label", "children", "attributes"],
                additionalProperties: false,
            },
            strict: true,
        },
    },
});

const ui = JSON.parse(response.output_text);
```

```python
import json
from openai import OpenAI

client = OpenAI()

response = client.responses.create(
    model="gpt-4o-2024-08-06",
    input=[
        {"role": "system", "content": "You are a UI generator AI. Convert the user input into a UI."},
        {"role": "user", "content": "Make a User Profile Form"}
    ],
    text={
        "format": {
            "type": "json_schema",
            "name": "ui",
            "description": "Dynamically generated UI",
            "schema": {
                "type": "object",
                "properties": {
                    "type": {
                        "type": "string",
                        "description": "The type of the UI component",
                        "enum": ["div", "button", "header", "section", "field", "form"]
                    },
                    "label": {
                        "type": "string",
                        "description": "The label of the UI component, used for buttons or form fields"
                    },
                    "children": {
                        "type": "array",
                        "description": "Nested UI components",
                        "items": {"$ref": "#"}
                    },
                    "attributes": {
                        "type": "array",
                        "description": "Arbitrary attributes for the UI component, suitable for any element",
                        "items": {
                            "type": "object",
                            "properties": {
                              "name": {
                                  "type": "string",
                                  "description": "The name of the attribute, for example onClick or className"
                              },
                              "value": {
                                  "type": "string",
                                  "description": "The value of the attribute"
                              }
                          },
                          "required": ["name", "value"],
                          "additionalProperties": False
                      }
                    }
                },
                "required": ["type", "label", "children", "attributes"],
                "additionalProperties": False
            },
            "strict": True,
        },
    },
)

ui = json.loads(response.output_text)
```

```bash
curl https://api.openai.com/v1/responses \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-4o-2024-08-06",
    "input": [
      {
        "role": "system",
        "content": "You are a UI generator AI. Convert the user input into a UI."
      },
      {
        "role": "user",
        "content": "Make a User Profile Form"
      }
    ],
    "text": {
      "format": {
        "type": "json_schema",
        "name": "ui",
        "description": "Dynamically generated UI",
        "schema": {
          "type": "object",
          "properties": {
            "type": {
              "type": "string",
              "description": "The type of the UI component",
              "enum": ["div", "button", "header", "section", "field", "form"]
            },
            "label": {
              "type": "string",
              "description": "The label of the UI component, used for buttons or form fields"
            },
            "children": {
              "type": "array",
              "description": "Nested UI components",
              "items": {"$ref": "#"}
            },
            "attributes": {
              "type": "array",
              "description": "Arbitrary attributes for the UI component, suitable for any element",
              "items": {
                "type": "object",
                "properties": {
                  "name": {
                    "type": "string",
                    "description": "The name of the attribute, for example onClick or className"
                  },
                  "value": {
                    "type": "string",
                    "description": "The value of the attribute"
                  }
                },
                "required": ["name", "value"],
                "additionalProperties": false
              }
            }
          },
          "required": ["type", "label", "children", "attributes"],
          "additionalProperties": false
        },
        "strict": true
      }
    }
  }'
```

#### Example response

```json
{
  "type": "form",
  "label": "User Profile Form",
  "children": [
    {
      "type": "div",
      "label": "",
      "children": [
        {
          "type": "field",
          "label": "First Name",
          "children": [],
          "attributes": [
            {
              "name": "type",
              "value": "text"
            },
            {
              "name": "name",
              "value": "firstName"
            },
            {
              "name": "placeholder",
              "value": "Enter your first name"
            }
          ]
        },
        {
          "type": "field",
          "label": "Last Name",
          "children": [],
          "attributes": [
            {
              "name": "type",
              "value": "text"
            },
            {
              "name": "name",
              "value": "lastName"
            },
            {
              "name": "placeholder",
              "value": "Enter your last name"
            }
          ]
        }
      ],
      "attributes": []
    },
    {
      "type": "button",
      "label": "Submit",
      "children": [],
      "attributes": [
        {
          "name": "type",
          "value": "submit"
        }
      ]
    }
  ],
  "attributes": [
    {
      "name": "method",
      "value": "post"
    },
    {
      "name": "action",
      "value": "/submit-profile"
    }
  ]
}
```

Moderation

### Moderation

You can classify inputs on multiple categories, which is a common way of doing moderation.

Moderation using Structured Outputs

```javascript
import OpenAI from "openai";

const openai = new OpenAI();

const response = await openai.responses.create({
    model: "gpt-4o-2024-08-06",
    input: [
      {
        "role": "system",
        "content": "Determine if the user input violates specific guidelines and explain if they do."
      },
      {
        "role": "user",
        "content": "How do I prepare for a job interview?"
      }
    ],
    text: {
        format: {
          "type": "json_schema",
          "name": "content_compliance",
          "description": "Determines if content is violating specific moderation rules",
          "schema": {
            "type": "object",
            "properties": {
              "is_violating": {
                "type": "boolean",
                "description": "Indicates if the content is violating guidelines"
              },
              "category": {
                "type": ["string", "null"],
                "description": "Type of violation, if the content is violating guidelines. Null otherwise.",
                "enum": ["violence", "sexual", "self_harm"]
              },
              "explanation_if_violating": {
                "type": ["string", "null"],
                "description": "Explanation of why the content is violating"
              }
            },
            "required": ["is_violating", "category", "explanation_if_violating"],
            "additionalProperties": false
          },
          "strict": true
        },
    },
});

const compliance = JSON.parse(response.output_text);
```

```python
import json
from openai import OpenAI

client = OpenAI()

response = client.responses.create(
    model="gpt-4o-2024-08-06",
    input=[
        {"role": "system", "content": "Determine if the user input violates specific guidelines and explain if they do."},
        {"role": "user", "content": "How do I prepare for a job interview?"}
    ],
    text={
        "format": {
            "type": "json_schema",
            "name": "content_compliance",
            "description": "Determines if content is violating specific moderation rules",
            "schema": {
            "type": "object",
            "properties": {
                "is_violating": {
                    "type": "boolean",
                   "description": "Indicates if the content is violating guidelines"
                },
                "category": {
                "type": ["string", "null"],
                    "description": "Type of violation, if the content is violating guidelines. Null otherwise.",
                    "enum": ["violence", "sexual", "self_harm"]
                },
                "explanation_if_violating": {
                    "type": ["string", "null"],
                    "description": "Explanation of why the content is violating"
                }
            },
                "required": ["is_violating", "category", "explanation_if_violating"],
                "additionalProperties": False
            },
            "strict": True
        },
    },
)

compliance = json.loads(response.output_text)
```

```bash
curl https://api.openai.com/v1/responses \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-4o-2024-08-06",
    "input": [
      {
        "role": "system",
        "content": "Determine if the user input violates specific guidelines and explain if they do."
      },
      {
        "role": "user",
        "content": "How do I prepare for a job interview?"
      }
    ],
    "text": {
      "format": {
        "type": "json_schema",
        "name": "content_compliance",
        "description": "Determines if content is violating specific moderation rules",
        "schema": {
          "type": "object",
          "properties": {
            "is_violating": {
              "type": "boolean",
              "description": "Indicates if the content is violating guidelines"
            },
            "category": {
              "type": ["string", "null"],
              "description": "Type of violation, if the content is violating guidelines. Null otherwise.",
              "enum": ["violence", "sexual", "self_harm"]
            },
            "explanation_if_violating": {
              "type": ["string", "null"],
              "description": "Explanation of why the content is violating"
            }
          },
          "required": ["is_violating", "category", "explanation_if_violating"],
          "additionalProperties": false
        },
        "strict": true
      }
    }
  }'
```

#### Example response

```json
{
  "is_violating": false,
  "category": null,
  "explanation_if_violating": null
}
```

How to use Structured Outputs with text.format
----------------------------------------------

Step 1: Define your schema

First you must design the JSON Schema that the model should be constrained to follow. See the [examples](/docs/guides/structured-outputs#examples) at the top of this guide for reference.

While Structured Outputs supports much of JSON Schema, some features are unavailable either for performance or technical reasons. See [here](/docs/guides/structured-outputs#supported-schemas) for more details.

#### Tips for your JSON Schema

To maximize the quality of model generations, we recommend the following:

*   Name keys clearly and intuitively
*   Create clear titles and descriptions for important keys in your structure
*   Create and use evals to determine the structure that works best for your use case

Step 2: Supply your schema in the API call

To use Structured Outputs, simply specify

```json
text: { format: { type: "json_schema", "strict": true, "schema": … } }
```

For example:

```python
response = client.responses.create(
    model="gpt-4o-2024-08-06",
    input=[
        {"role": "system", "content": "You are a helpful math tutor. Guide the user through the solution step by step."},
        {"role": "user", "content": "how can I solve 8x + 7 = -23"}
    ],
    text={
        "format": {
            "type": "json_schema",
            "name": "calendar_event",
            "schema": {
                "type": "object",
                "properties": {
                    "steps": {
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {
                                "explanation": {"type": "string"},
                                "output": {"type": "string"}
                            },
                            "required": ["explanation", "output"],
                            "additionalProperties": False
                        }
                    },
                    "final_answer": {"type": "string"}
                },
                "required": ["steps", "final_answer"],
                "additionalProperties": False
            },
            "strict": True
        }
    }
)

print(response.output_text)
```

```javascript
const response = await openai.responses.create({
    model: "gpt-4o-2024-08-06",
    input: [
        { role: "system", content: "You are a helpful math tutor. Guide the user through the solution step by step." },
        { role: "user", content: "how can I solve 8x + 7 = -23" }
    ],
    text: {
        format: {
            type: "json_schema",
            name: "math_response",
            schema: {
                type: "object",
                properties: {
                    steps: {
                        type: "array",
                        items: {
                            type: "object",
                            properties: {
                                explanation: { type: "string" },
                                output: { type: "string" }
                            },
                            required: ["explanation", "output"],
                            additionalProperties: false
                        }
                    },
                    final_answer: { type: "string" }
                },
                required: ["steps", "final_answer"],
                additionalProperties: false
            },
            strict: true
        }
    }
});

console.log(response.output_text);
```

```bash
curl https://api.openai.com/v1/responses \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-4o-2024-08-06",
    "input": [
      {
        "role": "system",
        "content": "You are a helpful math tutor. Guide the user through the solution step by step."
      },
      {
        "role": "user",
        "content": "how can I solve 8x + 7 = -23"
      }
    ],
    "text": {
      "format": {
        "type": "json_schema",
        "name": "math_response",
        "schema": {
          "type": "object",
          "properties": {
            "steps": {
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "explanation": { "type": "string" },
                  "output": { "type": "string" }
                },
                "required": ["explanation", "output"],
                "additionalProperties": false
              }
            },
            "final_answer": { "type": "string" }
          },
          "required": ["steps", "final_answer"],
          "additionalProperties": false
        },
        "strict": true
      }
    }
  }'
```

**Note:** the first request you make with any schema will have additional latency as our API processes the schema, but subsequent requests with the same schema will not have additional latency.

Step 3: Handle edge cases

In some cases, the model might not generate a valid response that matches the provided JSON schema.

This can happen in the case of a refusal, if the model refuses to answer for safety reasons, or if for example you reach a max tokens limit and the response is incomplete.

```javascript
try {
  const response = await openai.responses.create({
    model: "gpt-4o-2024-08-06",
    input: [{
        role: "system",
        content: "You are a helpful math tutor. Guide the user through the solution step by step.",
      },
      {
        role: "user",
        content: "how can I solve 8x + 7 = -23"
      },
    ],
    max_output_tokens: 50,
    text: {
      format: {
        type: "json_schema",
        name: "math_response",
        schema: {
          type: "object",
          properties: {
            steps: {
              type: "array",
              items: {
                type: "object",
                properties: {
                  explanation: {
                    type: "string"
                  },
                  output: {
                    type: "string"
                  },
                },
                required: ["explanation", "output"],
                additionalProperties: false,
              },
            },
            final_answer: {
              type: "string"
            },
          },
          required: ["steps", "final_answer"],
          additionalProperties: false,
        },
        strict: true,
      },
    }
  });

  if (response.status === "incomplete" && response.incomplete_details.reason === "max_output_tokens") {
    // Handle the case where the model did not return a complete response
    throw new Error("Incomplete response");
  }

  const math_response = response.output[0].content[0];

  if (math_response.type === "refusal") {
    // handle refusal
    console.log(math_response.refusal);
  } else if (math_response.type === "output_text") {
    console.log(math_response.text);
  } else {
    throw new Error("No response content");
  }
} catch (e) {
  // Handle edge cases
  console.error(e);
}
```

```python
try:
    response = client.responses.create(
        model="gpt-4o-2024-08-06",
        input=[
            {
                "role": "system",
                "content": "You are a helpful math tutor. Guide the user through the solution step by step.",
            },
            {"role": "user", "content": "how can I solve 8x + 7 = -23"},
        ],
        text={
            "format": {
                "type": "json_schema",
                "name": "math_response",
                "strict": True,
                "schema": {
                    "type": "object",
                    "properties": {
                        "steps": {
                            "type": "array",
                            "items": {
                                "type": "object",
                                "properties": {
                                    "explanation": {"type": "string"},
                                    "output": {"type": "string"},
                                },
                                "required": ["explanation", "output"],
                                "additionalProperties": False,
                            },
                        },
                        "final_answer": {"type": "string"},
                    },
                    "required": ["steps", "final_answer"],
                    "additionalProperties": False,
                },
                "strict": True,
            },
        },
    )
except Exception as e:
    # handle errors like finish_reason, refusal, content_filter, etc.
    pass
```

### Refusals with Structured Outputs

When using Structured Outputs with user-generated input, OpenAI models may occasionally refuse to fulfill the request for safety reasons. Since a refusal does not necessarily follow the schema you have supplied in `response_format`, the API response will include a new field called `refusal` to indicate that the model refused to fulfill the request.

When the `refusal` property appears in your output object, you might present the refusal in your UI, or include conditional logic in code that consumes the response to handle the case of a refused request.

```python
class Step(BaseModel):
    explanation: str
    output: str

class MathReasoning(BaseModel):
    steps: list[Step]
    final_answer: str

completion = client.beta.chat.completions.parse(
    model="gpt-4o-2024-08-06",
    messages=[
        {"role": "system", "content": "You are a helpful math tutor. Guide the user through the solution step by step."},
        {"role": "user", "content": "how can I solve 8x + 7 = -23"}
    ],
    response_format=MathReasoning,
)

math_reasoning = completion.choices[0].message

# If the model refuses to respond, you will get a refusal message
if (math_reasoning.refusal):
    print(math_reasoning.refusal)
else:
    print(math_reasoning.parsed)
```

```javascript
const Step = z.object({
  explanation: z.string(),
  output: z.string(),
});

const MathReasoning = z.object({
  steps: z.array(Step),
  final_answer: z.string(),
});

const completion = await openai.beta.chat.completions.parse({
  model: "gpt-4o-2024-08-06",
  messages: [
    { role: "system", content: "You are a helpful math tutor. Guide the user through the solution step by step." },
    { role: "user", content: "how can I solve 8x + 7 = -23" },
  ],
  response_format: zodResponseFormat(MathReasoning, "math_reasoning"),
});

const math_reasoning = completion.choices[0].message

// If the model refuses to respond, you will get a refusal message
if (math_reasoning.refusal) {
  console.log(math_reasoning.refusal);
} else {
  console.log(math_reasoning.parsed);
}
```

The API response from a refusal will look something like this:

```json
{
  "id": "resp_1234567890",
  "object": "response",
  "created_at": 1721596428,
  "status": "completed",
  "error": null,
  "incomplete_details": null,
  "input": [],
  "instructions": null,
  "max_output_tokens": null,
  "model": "gpt-4o-2024-08-06",
  "output": [{
    "id": "msg_1234567890",
    "type": "message",
    "role": "assistant",
    "content": [
      {
        "type": "refusal",
        "refusal": "I'm sorry, I cannot assist with that request."
      }
    ]
  }],
  "usage": {
    "input_tokens": 81,
    "output_tokens": 11,
    "total_tokens": 92,
    "output_tokens_details": {
      "reasoning_tokens": 0,
    }
  },
}
```

### Tips and best practices

#### Handling user-generated input

If your application is using user-generated input, make sure your prompt includes instructions on how to handle situations where the input cannot result in a valid response.

The model will always try to adhere to the provided schema, which can result in hallucinations if the input is completely unrelated to the schema.

You could include language in your prompt to specify that you want to return empty parameters, or a specific sentence, if the model detects that the input is incompatible with the task.

#### Handling mistakes

Structured Outputs can still contain mistakes. If you see mistakes, try adjusting your instructions, providing examples in the system instructions, or splitting tasks into simpler subtasks. Refer to the [prompt engineering guide](/docs/guides/prompt-engineering) for more guidance on how to tweak your inputs.

Streaming
---------

You can use streaming to process model responses or function call arguments as they are being generated, and parse them as structured data.

That way, you don't have to wait for the entire response to complete before handling it. This is particularly useful if you would like to display JSON fields one by one, or handle function call arguments as soon as they are available.

We recommend relying on the SDKs to handle streaming with Structured Outputs.

```python
from openai import OpenAI

client = OpenAI()

stream = client.responses.create(
    model="gpt-4o",
    input=[
        {"role": "system", "content": "Extract entities from the input text"},
        {
            "role": "user",
            "content": "The quick brown fox jumps over the lazy dog with piercing blue eyes"
        },
    ],
    text={
        "format": {
            "type": "json_schema",
            "name": "entities",
            "schema": {
                "type": "object",
                "properties": {
                    "attributes": {
                        "type": "array",
                        "items": {"type": "string"}
                    },
                    "colors": {
                        "type": "array",
                        "items": {"type": "string"}
                    },
                    "animals": {
                        "type": "array",
                        "items": {"type": "string"}
                    }
                },
                "required": ["attributes", "colors", "animals"],
                "additionalProperties": False
            },
        }
    },
    stream=True,
)

for event in stream:
    if event.type == 'response.refusal.delta':
        print(event.delta, end="")
    elif event.type == 'response.output_text.delta':
        print(event.delta, end="")
    elif event.type == 'response.error':
        print(event.error, end="")
    elif event.type == 'response.completed':
        print("Completed")
        # print(event.response.output)
```

```javascript
import { OpenAI } from "openai";

const openai = new OpenAI();

const stream = await openai.responses.create({
    model: "gpt-4o",
    input: [{ role: "user", content: "What's the weather like in Paris today?" }],
    stream: true,
    text: {
        "format": {
            "type": "json_schema",
            "name": "entities",
            "schema": {
                "type": "object",
                "properties": {
                    "attributes": {
                        "type": "array",
                        "items": {"type": "string"}
                    },
                    "colors": {
                        "type": "array",
                        "items": {"type": "string"}
                    },
                    "animals": {
                        "type": "array",
                        "items": {"type": "string"}
                    }
                },
                "required": ["attributes", "colors", "animals"],
                "additionalProperties": false
            },
        }
    }
});

for await (const event of stream) {
    if (event.type === 'response.refusal.delta') {
        process.stdout.write(event.delta);
    } else if (event.type === 'response.output_text.delta') {
        process.stdout.write(event.delta);
    } else if (event.type === 'response.error') {
        process.stdout.write(event.error);  
    } else if (event.type === 'response.completed') {
        console.log("Completed")
        // console.log(event.response.output);
    }
}
```

Supported schemas
-----------------

Structured Outputs supports a subset of the [JSON Schema](https://json-schema.org/docs) language.

#### Supported types

The following types are supported for Structured Outputs:

*   String
*   Number
*   Boolean
*   Integer
*   Object
*   Array
*   Enum
*   anyOf

#### Root objects must not be `anyOf`

Note that the root level object of a schema must be an object, and not use `anyOf`. A pattern that appears in Zod (as one example) is using a discriminated union, which produces an `anyOf` at the top level. So code such as the following won't work:

```javascript
import { z } from 'zod';
import { zodResponseFormat } from 'openai/helpers/zod';

const BaseResponseSchema = z.object({ /* ... */ });
const UnsuccessfulResponseSchema = z.object({ /* ... */ });

const finalSchema = z.discriminatedUnion('status', [
    BaseResponseSchema,
    UnsuccessfulResponseSchema,
]);

// Invalid JSON Schema for Structured Outputs
const json = zodResponseFormat(finalSchema, 'final_schema');
```

#### All fields must be `required`

To use Structured Outputs, all fields or function parameters must be specified as `required`.

```json
{
    "name": "get_weather",
    "description": "Fetches the weather in the given location",
    "strict": true,
    "parameters": {
        "type": "object",
        "properties": {
            "location": {
                "type": "string",
                "description": "The location to get the weather for"
            },
            "unit": {
                "type": "string",
                "description": "The unit to return the temperature in",
                "enum": ["F", "C"]
            }
        },
        "additionalProperties": false,
        "required": ["location", "unit"]
    }
}
```

Although all fields must be required (and the model will return a value for each parameter), it is possible to emulate an optional parameter by using a union type with `null`.

```json
{
    "name": "get_weather",
    "description": "Fetches the weather in the given location",
    "strict": true,
    "parameters": {
        "type": "object",
        "properties": {
            "location": {
                "type": "string",
                "description": "The location to get the weather for"
            },
            "unit": {
                "type": ["string", "null"],
                "description": "The unit to return the temperature in",
                "enum": ["F", "C"]
            }
        },
        "additionalProperties": false,
        "required": [
            "location", "unit"
        ]
    }
}
```

#### Objects have limitations on nesting depth and size

A schema may have up to 100 object properties total, with up to 5 levels of nesting.

#### Limitations on total string size

In a schema, total string length of all property names, definition names, enum values, and const values cannot exceed 15,000 characters.

#### Limitations on enum size

A schema may have up to 500 enum values across all enum properties.

For a single enum property with string values, the total string length of all enum values cannot exceed 7,500 characters when there are more than 250 enum values.

#### `additionalProperties: false` must always be set in objects

`additionalProperties` controls whether it is allowable for an object to contain additional keys / values that were not defined in the JSON Schema.

Structured Outputs only supports generating specified keys / values, so we require developers to set `additionalProperties: false` to opt into Structured Outputs.

```json
{
    "name": "get_weather",
    "description": "Fetches the weather in the given location",
    "strict": true,
    "schema": {
        "type": "object",
        "properties": {
            "location": {
                "type": "string",
                "description": "The location to get the weather for"
            },
            "unit": {
                "type": "string",
                "description": "The unit to return the temperature in",
                "enum": ["F", "C"]
            }
        },
        "additionalProperties": false,
        "required": [
            "location", "unit"
        ]
    }
}
```

#### Key ordering

When using Structured Outputs, outputs will be produced in the same order as the ordering of keys in the schema.

#### Some type-specific keywords are not yet supported

Notable keywords not supported include:

*   **For strings:** `minLength`, `maxLength`, `pattern`, `format`
*   **For numbers:** `minimum`, `maximum`, `multipleOf`
*   **For objects:** `patternProperties`, `unevaluatedProperties`, `propertyNames`, `minProperties`, `maxProperties`
*   **For arrays:** `unevaluatedItems`, `contains`, `minContains`, `maxContains`, `minItems`, `maxItems`, `uniqueItems`

If you turn on Structured Outputs by supplying `strict: true` and call the API with an unsupported JSON Schema, you will receive an error.

#### For `anyOf`, the nested schemas must each be a valid JSON Schema per this subset

Here's an example supported anyOf schema:

```json
{
    "type": "object",
    "properties": {
        "item": {
            "anyOf": [
                {
                    "type": "object",
                    "description": "The user object to insert into the database",
                    "properties": {
                        "name": {
                            "type": "string",
                            "description": "The name of the user"
                        },
                        "age": {
                            "type": "number",
                            "description": "The age of the user"
                        }
                    },
                    "additionalProperties": false,
                    "required": [
                        "name",
                        "age"
                    ]
                },
                {
                    "type": "object",
                    "description": "The address object to insert into the database",
                    "properties": {
                        "number": {
                            "type": "string",
                            "description": "The number of the address. Eg. for 123 main st, this would be 123"
                        },
                        "street": {
                            "type": "string",
                            "description": "The street name. Eg. for 123 main st, this would be main st"
                        },
                        "city": {
                            "type": "string",
                            "description": "The city of the address"
                        }
                    },
                    "additionalProperties": false,
                    "required": [
                        "number",
                        "street",
                        "city"
                    ]
                }
            ]
        }
    },
    "additionalProperties": false,
    "required": [
        "item"
    ]
}
```

#### Definitions are supported

You can use definitions to define subschemas which are referenced throughout your schema. The following is a simple example.

```json
{
    "type": "object",
    "properties": {
        "steps": {
            "type": "array",
            "items": {
                "$ref": "#/$defs/step"
            }
        },
        "final_answer": {
            "type": "string"
        }
    },
    "$defs": {
        "step": {
            "type": "object",
            "properties": {
                "explanation": {
                    "type": "string"
                },
                "output": {
                    "type": "string"
                }
            },
            "required": [
                "explanation",
                "output"
            ],
            "additionalProperties": false
        }
    },
    "required": [
        "steps",
        "final_answer"
    ],
    "additionalProperties": false
}
```

#### Recursive schemas are supported

Sample recursive schema using `#` to indicate root recursion.

```json
{
    "name": "ui",
    "description": "Dynamically generated UI",
    "strict": true,
    "schema": {
        "type": "object",
        "properties": {
            "type": {
                "type": "string",
                "description": "The type of the UI component",
                "enum": ["div", "button", "header", "section", "field", "form"]
            },
            "label": {
                "type": "string",
                "description": "The label of the UI component, used for buttons or form fields"
            },
            "children": {
                "type": "array",
                "description": "Nested UI components",
                "items": {
                    "$ref": "#"
                }
            },
            "attributes": {
                "type": "array",
                "description": "Arbitrary attributes for the UI component, suitable for any element",
                "items": {
                    "type": "object",
                    "properties": {
                        "name": {
                            "type": "string",
                            "description": "The name of the attribute, for example onClick or className"
                        },
                        "value": {
                            "type": "string",
                            "description": "The value of the attribute"
                        }
                    },
                    "additionalProperties": false,
                    "required": ["name", "value"]
                }
            }
        },
        "required": ["type", "label", "children", "attributes"],
        "additionalProperties": false
    }
}
```

Sample recursive schema using explicit recursion:

```json
{
    "type": "object",
    "properties": {
        "linked_list": {
            "$ref": "#/$defs/linked_list_node"
        }
    },
    "$defs": {
        "linked_list_node": {
            "type": "object",
            "properties": {
                "value": {
                    "type": "number"
                },
                "next": {
                    "anyOf": [
                        {
                            "$ref": "#/$defs/linked_list_node"
                        },
                        {
                            "type": "null"
                        }
                    ]
                }
            },
            "additionalProperties": false,
            "required": [
                "next",
                "value"
            ]
        }
    },
    "additionalProperties": false,
    "required": [
        "linked_list"
    ]
}
```

JSON mode
---------

JSON mode is a more basic version of the Structured Outputs feature. While JSON mode ensures that model output is valid JSON, Structured Outputs reliably matches the model's output to the schema you specify. We recommend you use Structured Outputs if it is supported for your use case.

When JSON mode is turned on, the model's output is ensured to be valid JSON, except for in some edge cases that you should detect and handle appropriately.

To turn on JSON mode with the Responses API you can set the `text.format` to `{ "type": "json_object" }`. If you are using function calling, JSON mode is always turned on.

Important notes:

*   When using JSON mode, you must always instruct the model to produce JSON via some message in the conversation, for example via your system message. If you don't include an explicit instruction to generate JSON, the model may generate an unending stream of whitespace and the request may run continually until it reaches the token limit. To help ensure you don't forget, the API will throw an error if the string "JSON" does not appear somewhere in the context.
*   JSON mode will not guarantee the output matches any specific schema, only that it is valid and parses without errors. You should use Structured Outputs to ensure it matches your schema, or if that is not possible, you should use a validation library and potentially retries to ensure that the output matches your desired schema.
*   Your application must detect and handle the edge cases that can result in the model output not being a complete JSON object (see below)

Handling edge cases

```javascript
const we_did_not_specify_stop_tokens = true;

try {
  const response = await openai.responses.create({
    model: "gpt-3.5-turbo-0125",
    input: [
      {
        role: "system",
        content: "You are a helpful assistant designed to output JSON.",
      },
      { role: "user", content: "Who won the world series in 2020? Please respond in the format {winner: ...}" },
    ],
    text: { format: { type: "json_object" } },
  });

  // Check if the conversation was too long for the context window, resulting in incomplete JSON 
  if (response.status === "incomplete" && response.incomplete_details.reason === "max_output_tokens") {
    // your code should handle this error case
  }

  // Check if the OpenAI safety system refused the request and generated a refusal instead
  if (response.output[0].content[0].type === "refusal") {
    // your code should handle this error case
    // In this case, the .content field will contain the explanation (if any) that the model generated for why it is refusing
    console.log(response.output[0].content[0].refusal)
  }

  // Check if the model's output included restricted content, so the generation of JSON was halted and may be partial
  if (response.status === "incomplete" && response.incomplete_details.reason === "content_filter") {
    // your code should handle this error case
  }

  if (response.status === "completed") {
    // In this case the model has either successfully finished generating the JSON object according to your schema, or the model generated one of the tokens you provided as a "stop token"

    if (we_did_not_specify_stop_tokens) {
      // If you didn't specify any stop tokens, then the generation is complete and the content key will contain the serialized JSON object
      // This will parse successfully and should now contain  {"winner": "Los Angeles Dodgers"}
      console.log(JSON.parse(response.output_text))
    } else {
      // Check if the response.output_text ends with one of your stop tokens and handle appropriately
    }
  }
} catch (e) {
  // Your code should handle errors here, for example a network error calling the API
  console.error(e)
}
```

```python
we_did_not_specify_stop_tokens = True

try:
    response = client.responses.create(
        model="gpt-3.5-turbo-0125",
        input=[
            {"role": "system", "content": "You are a helpful assistant designed to output JSON."},
            {"role": "user", "content": "Who won the world series in 2020? Please respond in the format {winner: ...}"}
        ],
        text={"format": {"type": "json_object"}}
    )

    # Check if the conversation was too long for the context window, resulting in incomplete JSON 
    if response.status == "incomplete" and response.incomplete_details.reason == "max_output_tokens":
        # your code should handle this error case
        pass

    # Check if the OpenAI safety system refused the request and generated a refusal instead
    if response.output[0].content[0].type == "refusal":
        # your code should handle this error case
        # In this case, the .content field will contain the explanation (if any) that the model generated for why it is refusing
        print(response.output[0].content[0]["refusal"])

    # Check if the model's output included restricted content, so the generation of JSON was halted and may be partial
    if response.status == "incomplete" and response.incomplete_details.reason == "content_filter":
        # your code should handle this error case
        pass

    if response.status == "completed":
        # In this case the model has either successfully finished generating the JSON object according to your schema, or the model generated one of the tokens you provided as a "stop token"

        if we_did_not_specify_stop_tokens:
            # If you didn't specify any stop tokens, then the generation is complete and the content key will contain the serialized JSON object
            # This will parse successfully and should now contain  "{"winner": "Los Angeles Dodgers"}"
            print(response.output_text)
        else:
            # Check if the response.output_text ends with one of your stop tokens and handle appropriately
            pass
except Exception as e:
    # Your code should handle errors here, for example a network error calling the API
    print(e)
```

Resources
---------

To learn more about Structured Outputs, we recommend browsing the following resources:

*   Check out our [introductory cookbook](https://cookbook.openai.com/examples/structured_outputs_intro) on Structured Outputs
*   Learn [how to build multi-agent systems](https://cookbook.openai.com/examples/structured_outputs_multi_agent) with Structured Outputs

Was this page useful?
Function calling
================

Enable models to fetch data and take actions.

**Function calling** provides a powerful and flexible way for OpenAI models to interface with your code or external services. This guide will explain how to connect the models to your own custom code to fetch data or take action.

Get weather

Function calling example with get\_weather function

```python
from openai import OpenAI

client = OpenAI()

tools = [{
    "type": "function",
    "name": "get_weather",
    "description": "Get current temperature for a given location.",
    "parameters": {
        "type": "object",
        "properties": {
            "location": {
                "type": "string",
                "description": "City and country e.g. Bogotá, Colombia"
            }
        },
        "required": [
            "location"
        ],
        "additionalProperties": False
    }
}]

response = client.responses.create(
    model="gpt-4o",
    input=[{"role": "user", "content": "What is the weather like in Paris today?"}],
    tools=tools
)

print(response.output)
```

```javascript
import { OpenAI } from "openai";

const openai = new OpenAI();

const tools = [{
    "type": "function",
    "name": "get_weather",
    "description": "Get current temperature for a given location.",
    "parameters": {
        "type": "object",
        "properties": {
            "location": {
                "type": "string",
                "description": "City and country e.g. Bogotá, Colombia"
            }
        },
        "required": [
            "location"
        ],
        "additionalProperties": false
    }
}];

const response = await openai.responses.create({
    model: "gpt-4o",
    input: [{ role: "user", content: "What is the weather like in Paris today?" }],
    tools,
});

console.log(response.output);
```

```bash
curl https://api.openai.com/v1/responses \
-H "Content-Type: application/json" \
-H "Authorization: Bearer $OPENAI_API_KEY" \
-d '{
    "model": "gpt-4o",
    "input": "What is the weather like in Paris today?",
    "tools": [
        {
            "type": "function",
            "name": "get_weather",
            "description": "Get current temperature for a given location.",
            "parameters": {
                "type": "object",
                "properties": {
                    "location": {
                        "type": "string",
                        "description": "City and country e.g. Bogotá, Colombia"
                    }
                },
                "required": [
                    "location"
                ],
                "additionalProperties": false
            }
        }
    ]
}'
```

Output

```json
[{
    "type": "function_call",
    "id": "fc_12345xyz",
    "call_id": "call_12345xyz",
    "name": "get_weather",
    "arguments": "{\"location\":\"Paris, France\"}"
}]
```

Send email

Function calling example with send\_email function

```python
from openai import OpenAI

client = OpenAI()

tools = [{
    "type": "function",
    "name": "send_email",
    "description": "Send an email to a given recipient with a subject and message.",
    "parameters": {
        "type": "object",
        "properties": {
            "to": {
                "type": "string",
                "description": "The recipient email address."
            },
            "subject": {
                "type": "string",
                "description": "Email subject line."
            },
            "body": {
                "type": "string",
                "description": "Body of the email message."
            }
        },
        "required": [
            "to",
            "subject",
            "body"
        ],
        "additionalProperties": False
    }
}]

response = client.responses.create(
    model="gpt-4o",
    input=[{"role": "user", "content": "Can you send an email to ilan@example.com and katia@example.com saying hi?"}],
    tools=tools
)

print(response.output)
```

```javascript
import { OpenAI } from "openai";

const openai = new OpenAI();

const tools = [{
    "type": "function",
    "name": "send_email",
    "description": "Send an email to a given recipient with a subject and message.",
    "parameters": {
        "type": "object",
        "properties": {
            "to": {
                "type": "string",
                "description": "The recipient email address."
            },
            "subject": {
                "type": "string",
                "description": "Email subject line."
            },
            "body": {
                "type": "string",
                "description": "Body of the email message."
            }
        },
        "required": [
            "to",
            "subject",
            "body"
        ],
        "additionalProperties": false
    }
}];

const response = await openai.responses.create({
    model: "gpt-4o",
    input: [{ role: "user", content: "Can you send an email to ilan@example.com and katia@example.com saying hi?" }],
    tools,
});

console.log(response.output);
```

```bash
curl https://api.openai.com/v1/responses \
-H "Content-Type: application/json" \
-H "Authorization: Bearer $OPENAI_API_KEY" \
-d '{
    "model": "gpt-4o",
    "input": "Can you send an email to ilan@example.com and katia@example.com saying hi?",
    "tools": [
        {
            "type": "function",
            "name": "send_email",
            "description": "Send an email to a given recipient with a subject and message.",
            "parameters": {
                "type": "object",
                "properties": {
                    "to": {
                        "type": "string",
                        "description": "The recipient email address."
                    },
                    "subject": {
                        "type": "string",
                        "description": "Email subject line."
                    },
                    "body": {
                        "type": "string",
                        "description": "Body of the email message."
                    }
                },
                "required": [
                    "to",
                    "subject",
                    "body"
                ],
                "additionalProperties": false
            }
        }
    ]
}'
```

Output

```json
[
    {
        "type": "function_call",
        "id": "fc_12345xyz",
        "call_id": "call_9876abc",
        "name": "send_email",
        "arguments": "{\"to\":\"ilan@example.com\",\"subject\":\"Hello!\",\"body\":\"Just wanted to say hi\"}"
    },
    {
        "type": "function_call",
        "id": "fc_12345xyz",
        "call_id": "call_9876abc",
        "name": "send_email",
        "arguments": "{\"to\":\"katia@example.com\",\"subject\":\"Hello!\",\"body\":\"Just wanted to say hi\"}"
    }
]
```

Search knowledge base

Function calling example with search\_knowledge\_base function

```python
from openai import OpenAI

client = OpenAI()

tools = [{
    "type": "function",
    "name": "search_knowledge_base",
    "description": "Query a knowledge base to retrieve relevant info on a topic.",
    "parameters": {
        "type": "object",
        "properties": {
            "query": {
                "type": "string",
                "description": "The user question or search query."
            },
            "options": {
                "type": "object",
                "properties": {
                    "num_results": {
                        "type": "number",
                        "description": "Number of top results to return."
                    },
                    "domain_filter": {
                        "type": [
                            "string",
                            "null"
                        ],
                        "description": "Optional domain to narrow the search (e.g. 'finance', 'medical'). Pass null if not needed."
                    },
                    "sort_by": {
                        "type": [
                            "string",
                            "null"
                        ],
                        "enum": [
                            "relevance",
                            "date",
                            "popularity",
                            "alphabetical"
                        ],
                        "description": "How to sort results. Pass null if not needed."
                    }
                },
                "required": [
                    "num_results",
                    "domain_filter",
                    "sort_by"
                ],
                "additionalProperties": False
            }
        },
        "required": [
            "query",
            "options"
        ],
        "additionalProperties": False
    }
}]

response = client.responses.create(
    model="gpt-4o",
    input=[{"role": "user", "content": "Can you find information about ChatGPT in the AI knowledge base?"}],
    tools=tools
)

print(response.output)
```

```javascript
import { OpenAI } from "openai";

const openai = new OpenAI();

const tools = [{
    "type": "function",
    "name": "search_knowledge_base",
    "description": "Query a knowledge base to retrieve relevant info on a topic.",
    "parameters": {
        "type": "object",
        "properties": {
            "query": {
                "type": "string",
                "description": "The user question or search query."
            },
            "options": {
                "type": "object",
                "properties": {
                    "num_results": {
                        "type": "number",
                        "description": "Number of top results to return."
                    },
                    "domain_filter": {
                        "type": [
                            "string",
                            "null"
                        ],
                        "description": "Optional domain to narrow the search (e.g. 'finance', 'medical'). Pass null if not needed."
                    },
                    "sort_by": {
                        "type": [
                            "string",
                            "null"
                        ],
                        "enum": [
                            "relevance",
                            "date",
                            "popularity",
                            "alphabetical"
                        ],
                        "description": "How to sort results. Pass null if not needed."
                    }
                },
                "required": [
                    "num_results",
                    "domain_filter",
                    "sort_by"
                ],
                "additionalProperties": false
            }
        },
        "required": [
            "query",
            "options"
        ],
        "additionalProperties": false
    }
}];

const response = await openai.responses.create({
    model: "gpt-4o",
    input: [{ role: "user", content: "Can you find information about ChatGPT in the AI knowledge base?" }],
    tools,
});

console.log(response.output);
```

```bash
curl https://api.openai.com/v1/responses \
-H "Content-Type: application/json" \
-H "Authorization: Bearer $OPENAI_API_KEY" \
-d '{
    "model": "gpt-4o",
    "input": "Can you find information about ChatGPT in the AI knowledge base?",
    "tools": [
        {
            "type": "function",
            "name": "search_knowledge_base",
            "description": "Query a knowledge base to retrieve relevant info on a topic.",
            "parameters": {
                "type": "object",
                "properties": {
                    "query": {
                        "type": "string",
                        "description": "The user question or search query."
                    },
                    "options": {
                        "type": "object",
                        "properties": {
                            "num_results": {
                                "type": "number",
                                "description": "Number of top results to return."
                            },
                            "domain_filter": {
                                "type": [
                                    "string",
                                    "null"
                                ],
                                "description": "Optional domain to narrow the search (e.g. 'finance', 'medical'). Pass null if not needed."
                            },
                            "sort_by": {
                                "type": [
                                    "string",
                                    "null"
                                ],
                                "enum": [
                                    "relevance",
                                    "date",
                                    "popularity",
                                    "alphabetical"
                                ],
                                "description": "How to sort results. Pass null if not needed."
                            }
                        },
                        "required": [
                            "num_results",
                            "domain_filter",
                            "sort_by"
                        ],
                        "additionalProperties": false
                    }
                },
                "required": [
                    "query",
                    "options"
                ],
                "additionalProperties": false
            }
        }
    ]
}'
```

Output

```json
[{
    "type": "function_call",
    "id": "fc_12345xyz",
    "call_id": "call_4567xyz",
    "name": "search_knowledge_base",
    "arguments": "{\"query\":\"What is ChatGPT?\",\"options\":{\"num_results\":3,\"domain_filter\":null,\"sort_by\":\"relevance\"}}"
}]
```

Experiment with function calling and [generate function schemas](/docs/guides/prompt-generation) in the [Playground](/playground)!

Overview
--------

You can give the model access to your own custom code through **function calling**. Based on the system prompt and messages, the model may decide to call these functions — **instead of (or in addition to) generating text or audio**.

You'll then execute the function code, send back the results, and the model will incorporate them into its final response.

![Function Calling Diagram Steps](https://cdn.openai.com/API/docs/images/function-calling-diagram-steps.png)

Function calling has two primary use cases:

|||
|---|---|
|Fetching Data|Retrieve up-to-date information to incorporate into the model's response (RAG). Useful for searching knowledge bases and retrieving specific data from APIs (e.g. current weather data).|
|Taking Action|Perform actions like submitting a form, calling APIs, modifying application state (UI/frontend or backend), or taking agentic workflow actions (like handing off the conversation).|

### Sample function

Let's look at the steps to allow a model to use a real `get_weather` function defined below:

Sample get\_weather function implemented in your codebase

```python
import requests

def get_weather(latitude, longitude):
    response = requests.get(f"https://api.open-meteo.com/v1/forecast?latitude={latitude}&longitude={longitude}&current=temperature_2m,wind_speed_10m&hourly=temperature_2m,relative_humidity_2m,wind_speed_10m")
    data = response.json()
    return data['current']['temperature_2m']
```

```javascript
async function getWeather(latitude, longitude) {
    const response = await fetch(`https://api.open-meteo.com/v1/forecast?latitude=${latitude}&longitude=${longitude}&current=temperature_2m,wind_speed_10m&hourly=temperature_2m,relative_humidity_2m,wind_speed_10m`);
    const data = await response.json();
    return data.current.temperature_2m;
}
```

Unlike the diagram earlier, this function expects precise `latitude` and `longitude` instead of a general `location` parameter. (However, our models can automatically determine the coordinates for many locations!)

### Function calling steps

*   **Call model with [functions defined](#defining-functions)** – along with your system and user messages.
    

Step 1: Call model with get\_weather tool defined

```python
from openai import OpenAI
import json

client = OpenAI()

tools = [{
    "type": "function",
    "name": "get_weather",
    "description": "Get current temperature for provided coordinates in celsius.",
    "parameters": {
        "type": "object",
        "properties": {
            "latitude": {"type": "number"},
            "longitude": {"type": "number"}
        },
        "required": ["latitude", "longitude"],
        "additionalProperties": False
    },
    "strict": True
}]

input_messages = [{"role": "user", "content": "What's the weather like in Paris today?"}]

response = client.responses.create(
    model="gpt-4o",
    input=input_messages,
    tools=tools,
)
```

```javascript
import { OpenAI } from "openai";

const openai = new OpenAI();

const tools = [{
    type: "function",
    name: "get_weather",
    description: "Get current temperature for provided coordinates in celsius.",
    parameters: {
        type: "object",
        properties: {
            latitude: { type: "number" },
            longitude: { type: "number" }
        },
        required: ["latitude", "longitude"],
        additionalProperties: false
    },
    strict: true
}];

const input = [
    {
        role: "user",
        content: "What's the weather like in Paris today?"
    }
];

const response = await openai.responses.create({
    model: "gpt-4o",
    input,
    tools,
});
```

*   **Model decides to call function(s)** – model returns the **name** and **input arguments**.
    

response.output

```json
[{
    "type": "function_call",
    "id": "fc_12345xyz",
    "call_id": "call_12345xyz",
    "name": "get_weather",
    "arguments": "{\"latitude\":48.8566,\"longitude\":2.3522}"
}]
```

*   **Execute function code** – parse the model's response and [handle function calls](#handling-function-calls).
    

Step 3: Execute get\_weather function

```python
tool_call = response.output[0]
args = json.loads(tool_call.arguments)

result = get_weather(args["latitude"], args["longitude"])
```

```javascript
const toolCall = response.output[0];
const args = JSON.parse(toolCall.arguments);

const result = await getWeather(args.latitude, args.longitude);
```

*   **Supply model with results** – so it can incorporate them into its final response.
    

Step 4: Supply result and call model again

```python
input_messages.append(tool_call)  # append model's function call message
input_messages.append({                               # append result message
    "type": "function_call_output",
    "call_id": tool_call.call_id,
    "output": str(result)
})

response_2 = client.responses.create(
    model="gpt-4o",
    input=input_messages,
    tools=tools,
)
print(response_2.output_text)
```

```javascript
input.push(toolCall); // append model's function call message
input.push({                               // append result message
    type: "function_call_output",
    call_id: toolCall.call_id,
    output: result.toString()
});

const response2 = await openai.responses.create({
    model: "gpt-4o",
    input,
    tools,
    store: true,
});

console.log(response2.output_text)
```

*   **Model responds** – incorporating the result in its output.
    

response\_2.output\_text

```json
"The current temperature in Paris is 14°C (57.2°F)."
```

Defining functions
------------------

Functions can be set in the `tools` parameter of each API request.

A function is defined by its schema, which informs the model what it does and what input arguments it expects. It comprises the following fields:

|Field|Description|
|---|---|
|type|This should always be function|
|name|The function's name (e.g. get_weather)|
|description|Details on when and how to use the function|
|parameters|JSON schema defining the function's input arguments|
|strict|Whether to enforce strict mode for the function call|

Take a look at this example or generate your own below (or in our [Playground](/playground)).

Generate

Example function schema

```json
{
    "type": "function",
    "function": {
        "name": "get_weather",
        "description": "Retrieves current weather for the given location.",
        "parameters": {
            "type": "object",
            "properties": {
                "location": {
                    "type": "string",
                    "description": "City and country e.g. Bogotá, Colombia"
                },
                "units": {
                    "type": "string",
                    "enum": [
                        "celsius",
                        "fahrenheit"
                    ],
                    "description": "Units the temperature will be returned in."
                }
            },
            "required": [
                "location",
                "units"
            ],
            "additionalProperties": false
        },
        "strict": true
    }
}
```

Because the `parameters` are defined by a [JSON schema](https://json-schema.org/), you can leverage many of its rich features like property types, enums, descriptions, nested objects, and, recursive objects.

### Best practices for defining functions

1.  **Write clear and detailed function names, parameter descriptions, and instructions.**
    
    *   **Explicitly describe the purpose of the function and each parameter** (and its format), and what the output represents.
    *   **Use the system prompt to describe when (and when not) to use each function.** Generally, tell the model _exactly_ what to do.
    *   **Include examples and edge cases**, especially to rectify any recurring failures. (**Note:** Adding examples may hurt performance for [reasoning models](/docs/guides/reasoning).)
2.  **Apply software engineering best practices.**
    
    *   **Make the functions obvious and intuitive**. ([principle of least surprise](https://en.wikipedia.org/wiki/Principle_of_least_astonishment))
    *   **Use enums** and object structure to make invalid states unrepresentable. (e.g. `toggle_light(on: bool, off: bool)` allows for invalid calls)
    *   **Pass the intern test.** Can an intern/human correctly use the function given nothing but what you gave the model? (If not, what questions do they ask you? Add the answers to the prompt.)
3.  **Offload the burden from the model and use code where possible.**
    
    *   **Don't make the model fill arguments you already know.** For example, if you already have an `order_id` based on a previous menu, don't have an `order_id` param – instead, have no params `submit_refund()` and pass the `order_id` with code.
    *   **Combine functions that are always called in sequence.** For example, if you always call `mark_location()` after `query_location()`, just move the marking logic into the query function call.
4.  **Keep the number of functions small for higher accuracy.**
    
    *   **Evaluate your performance** with different numbers of functions.
    *   **Aim for fewer than 20 functions** at any one time, though this is just a soft suggestion.
5.  **Leverage OpenAI resources.**
    
    *   **Generate and iterate on function schemas** in the [Playground](/playground).
    *   **Consider [fine-tuning](https://platform.openai.com/docs/guides/fine-tuning) to increase function calling accuracy** for large numbers of functions or difficult tasks. ([cookbook](https://cookbook.openai.com/examples/fine_tuning_for_function_calling))

### Token Usage

Under the hood, functions are injected into the system message in a syntax the model has been trained on. This means functions count against the model's context limit and are billed as input tokens. If you run into token limits, we suggest limiting the number of functions or the length of the descriptions you provide for function parameters.

It is also possible to use [fine-tuning](/docs/guides/fine-tuning#fine-tuning-examples) to reduce the number of tokens used if you have many functions defined in your tools specification.

Handling function calls
-----------------------

When the model calls a function, you must execute it and return the result. Since model responses can include zero, one, or multiple calls, it is best practice to assume there are several.

The response `output` array contains an entry with the `type` having a value of `function_call`. Each entry with a `call_id` (used later to submit the function result), `name`, and JSON-encoded `arguments`.

Sample response with multiple function calls

```json
[
    {
        "id": "fc_12345xyz",
        "call_id": "call_12345xyz",
        "type": "function_call",
        "name": "get_weather",
        "arguments": "{\"location\":\"Paris, France\"}"
    },
    {
        "id": "fc_67890abc",
        "call_id": "call_67890abc",
        "type": "function_call",
        "name": "get_weather",
        "arguments": "{\"location\":\"Bogotá, Colombia\"}"
    },
    {
        "id": "fc_99999def",
        "call_id": "call_99999def",
        "type": "function_call",
        "name": "send_email",
        "arguments": "{\"to\":\"bob@email.com\",\"body\":\"Hi bob\"}"
    }
]
```

Execute function calls and append results

```python
for tool_call in response.output:
    if tool_call.type != "function_call":
        continue

    name = tool_call.name
    args = json.loads(tool_call.arguments)

    result = call_function(name, args)
    input_messages.append({
        "type": "function_call_output",
        "call_id": tool_call.call_id,
        "output": str(result)
    })
```

```javascript
for (const toolCall of response.output) {
    if (toolCall.type !== "function_call") {
        continue;
    }

    const name = toolCall.name;
    const args = JSON.parse(toolCall.arguments);

    const result = callFunction(name, args);
    input.push({
        type: "function_call_output",
        call_id: toolCall.call_id,
        output: result.toString()
    });
}
```

In the example above, we have a hypothetical `call_function` to route each call. Here’s a possible implementation:

Execute function calls and append results

```python
def call_function(name, args):
    if name == "get_weather":
        return get_weather(**args)
    if name == "send_email":
        return send_email(**args)
```

```javascript
const callFunction = async (name, args) => {
    if (name === "get_weather") {
        return getWeather(args.latitude, args.longitude);
    }
    if (name === "send_email") {
        return sendEmail(args.to, args.body);
    }
};
```

### Formatting results

A result must be a string, but the format is up to you (JSON, error codes, plain text, etc.). The model will interpret that string as needed.

If your function has no return value (e.g. `send_email`), simply return a string to indicate success or failure. (e.g. `"success"`)

### Incorporating results into response

After appending the results to your `input`, you can send them back to the model to get a final response.

Send results back to model

```python
response = client.responses.create(
    model="gpt-4o",
    input=input_messages,
    tools=tools,
)
```

```javascript
const response = await openai.responses.create({
    model: "gpt-4o",
    input,
    tools,
});
```

Final response

```json
"It's about 15°C in Paris, 18°C in Bogotá, and I've sent that email to Bob."
```

Additional configurations
-------------------------

### Tool choice

By default the model will determine when and how many tools to use. You can force specific behavior with the `tool_choice` parameter.

1.  **Auto:** (_Default_) Call zero, one, or multiple functions. `tool_choice: "auto"`
2.  **Required:** Call one or more functions. `tool_choice: "required"`

3.  **Forced Function:** Call exactly one specific function. `tool_choice: {"type": "function", "name": "get_weather"}`

![Function Calling Diagram Steps](https://cdn.openai.com/API/docs/images/function-calling-diagram-tool-choice.png)

You can also set `tool_choice` to `"none"` to imitate the behavior of passing no functions.

### Parallel function calling

The model may choose to call multiple functions in a single turn. You can prevent this by setting `parallel_tool_calls` to `false`, which ensures exactly zero or one tool is called.

**Note:** Currently, if the model calls multiple functions in one turn then [strict mode](#strict-mode) will be disabled for those calls.

### Strict mode

Setting `strict` to `true` will ensure function calls reliably adhere to the function schema, instead of being best effort. We recommend always enabling strict mode.

Under the hood, strict mode works by leveraging our [structured outputs](/docs/guides/structured-outputs) feature and therefore introduces a couple requirements:

1.  `additionalProperties` must be set to `false` for each object in the `parameters`.
2.  All fields in `properties` must be marked as `required`.

You can denote optional fields by adding `null` as a `type` option (see example below).

Strict mode enabled

```json
{
    "type": "function",
    "name": "get_weather",
    "description": "Retrieves current weather for the given location.",
    "strict": true,
    "parameters": {
        "type": "object",
        "properties": {
            "location": {
                "type": "string",
                "description": "City and country e.g. Bogotá, Colombia"
            },
            "units": {
                "type": ["string", "null"],
                "enum": ["celsius", "fahrenheit"],
                "description": "Units the temperature will be returned in."
            }
        },
        "required": ["location", "units"],
        "additionalProperties": false
    }
}
```

Strict mode disabled

```json
{
    "type": "function",
    "name": "get_weather",
    "description": "Retrieves current weather for the given location.",
    "parameters": {
        "type": "object",
        "properties": {
            "location": {
                "type": "string",
                "description": "City and country e.g. Bogotá, Colombia"
            },
            "units": {
                "type": "string",
                "enum": ["celsius", "fahrenheit"],
                "description": "Units the temperature will be returned in."
            }
        },
        "required": ["location"],
    }
}
```

All schemas generated in the [playground](/playground) have strict mode enabled.

While we recommend you enable strict mode, it has a few limitations:

1.  Some features of JSON schema are not supported. (See [supported schemas](/docs/guides/structured-outputs?context=with_parse#supported-schemas).)
2.  Schemas undergo additional processing on the first request (and are then cached). If your schemas vary from request to request, this may result in higher latencies.
3.  Schemas are cached for performance, and are not eligible for [zero data retention](/docs/models#how-we-use-your-data).

Streaming
---------

Streaming can be used to surface progress by showing which function is called as the model fills its arguments, and even displaying the arguments in real time.

Streaming function calls is very similar to streaming regular responses: you set `stream` to `true` and get different `event` objects.

Streaming function calls

```python
from openai import OpenAI

client = OpenAI()

tools = [{
    "type": "function",
    "name": "get_weather",
    "description": "Get current temperature for a given location.",
    "parameters": {
        "type": "object",
        "properties": {
            "location": {
                "type": "string",
                "description": "City and country e.g. Bogotá, Colombia"
            }
        },
        "required": [
            "location"
        ],
        "additionalProperties": False
    }
}]

stream = client.responses.create(
    model="gpt-4o",
    input=[{"role": "user", "content": "What's the weather like in Paris today?"}],
    tools=tools,
    stream=True
)

for event in stream:
    print(event)
```

```javascript
import { OpenAI } from "openai";

const openai = new OpenAI();

const tools = [{
    type: "function",
    name: "get_weather",
    description: "Get current temperature for provided coordinates in celsius.",
    parameters: {
        type: "object",
        properties: {
            latitude: { type: "number" },
            longitude: { type: "number" }
        },
        required: ["latitude", "longitude"],
        additionalProperties: false
    },
    strict: true
}];

const stream = await openai.responses.create({
    model: "gpt-4o",
    input: [{ role: "user", content: "What's the weather like in Paris today?" }],
    tools,
    stream: true,
    store: true,
});

for await (const event of stream) {
    console.log(event)
}
```

Output events

```json
{"type":"response.output_item.added","response_id":"resp_1234xyz","output_index":0,"item":{"type":"function_call","id":"fc_1234xyz","call_id":"call_1234xyz","name":"get_weather","arguments":""}}
{"type":"response.function_call_arguments.delta","response_id":"resp_1234xyz","item_id":"fc_1234xyz","output_index":0,"delta":"{\""}
{"type":"response.function_call_arguments.delta","response_id":"resp_1234xyz","item_id":"fc_1234xyz","output_index":0,"delta":"location"}
{"type":"response.function_call_arguments.delta","response_id":"resp_1234xyz","item_id":"fc_1234xyz","output_index":0,"delta":"\":\""}
{"type":"response.function_call_arguments.delta","response_id":"resp_1234xyz","item_id":"fc_1234xyz","output_index":0,"delta":"Paris"}
{"type":"response.function_call_arguments.delta","response_id":"resp_1234xyz","item_id":"fc_1234xyz","output_index":0,"delta":","}
{"type":"response.function_call_arguments.delta","response_id":"resp_1234xyz","item_id":"fc_1234xyz","output_index":0,"delta":" France"}
{"type":"response.function_call_arguments.delta","response_id":"resp_1234xyz","item_id":"fc_1234xyz","output_index":0,"delta":"\"}"}
{"type":"response.function_call_arguments.done","response_id":"resp_1234xyz","item_id":"fc_1234xyz","output_index":0,"arguments":"{\"location\":\"Paris, France\"}"}
{"type":"response.output_item.done","response_id":"resp_1234xyz","output_index":0,"item":{"type":"function_call","id":"fc_1234xyz","call_id":"call_2345abc","name":"get_weather","arguments":"{\"location\":\"Paris, France\"}"}}
```

Instead of aggregating chunks into a single `content` string, however, you're aggregating chunks into an encoded `arguments` JSON object.

When the model calls one or more functions an event of type `response.output_item.added` will be emitted for each function call that contains the following fields:

|Field|Description|
|---|---|
|response_id|The id of the response that the function call belongs to|
|output_index|The index of the output item in the response. This respresents the individual function calls in the response.|
|item|The in-progress function call item that includes a name, arguments and id field|

Afterwards you will receive a series of events of type `response.function_call_arguments.delta` which will contain the `delta` of the `arguments` field. These events contain the following fields:

|Field|Description|
|---|---|
|response_id|The id of the response that the function call belongs to|
|item_id|The id of the function call item that the delta belongs to|
|output_index|The index of the output item in the response. This respresents the individual function calls in the response.|
|delta|The delta of the arguments field.|

Below is a code snippet demonstrating how to aggregate the `delta`s into a final `tool_call` object.

Accumulating tool\_call deltas

```python
final_tool_calls = {}

for event in stream:
    if event.type === 'response.output_item.added':
        final_tool_calls[event.output_index] = event.item;
    elif event.type === 'response.function_call_arguments.delta':
        index = event.output_index

        if final_tool_calls[index]:
            final_tool_calls[index].arguments += event.delta
```

```javascript
const finalToolCalls = {};

for await (const event of stream) {
    if (event.type === 'response.output_item.added') {
        finalToolCalls[event.output_index] = event.item;
    } else if (event.type === 'response.function_call_arguments.delta') {
        const index = event.output_index;

        if (finalToolCalls[index]) {
            finalToolCalls[index].arguments += event.delta;
        }
    }
}
```

Accumulated final\_tool\_calls\[0\]

```json
{
    "type": "function_call",
    "id": "fc_1234xyz",
    "call_id": "call_2345abc",
    "name": "get_weather",
    "arguments": "{\"location\":\"Paris, France\"}"
}
```

When the model has finished calling the functions an event of type `response.function_call_arguments.done` will be emitted. This event contains the entire function call including the following fields:

|Field|Description|
|---|---|
|response_id|The id of the response that the function call belongs to|
|output_index|The index of the output item in the response. This respresents the individual function calls in the response.|
|item|The function call item that includes a name, arguments and id field.|

Was this page useful?
Conversation state
==================

Learn how to manage conversation state during a model interaction.

OpenAI provides a few ways to manage conversation state, which is important for preserving information across multiple messages or turns in a conversation.

Manually manage conversation state
----------------------------------

While each text generation request is independent and stateless (unless you're using [the Assistants API](/docs/assistants/overview)), you can still implement **multi-turn conversations** by providing additional messages as parameters to your text generation request. Consider a knock-knock joke:

Manually construct a past conversation

```javascript
import OpenAI from "openai";

const openai = new OpenAI();

const response = await openai.responses.create({
    model: "gpt-4o-mini",
    input: [
        { role: "user", content: "knock knock." },
        { role: "assistant", content: "Who's there?" },
        { role: "user", content: "Orange." },
    ],
});

console.log(response.output_text);
```

```python
from openai import OpenAI

client = OpenAI()

response = client.responses.create(
    model="gpt-4o-mini",
    input=[
        {"role": "user", "content": "knock knock."},
        {"role": "assistant", "content": "Who's there?"},
        {"role": "user", "content": "Orange."},
    ],
)

print(response.output_text)
```

By using alternating `user` and `assistant` messages, you capture the previous state of a conversation in one request to the model.

To manually share context across generated responses, include the model's previous response output as input, and append that input to your next request.

In the following example, we ask the model to tell a joke, followed by a request for another joke. Appending previous responses to new requests in this way helps ensure conversations feel natural and retain the context of previous interactions.

Manually manage conversation state with the Responses API.

```javascript
import OpenAI from "openai";

const openai = new OpenAI();

let history = [
    {
        role: "user",
        content: "tell me a joke",
    },
];

const response = await openai.responses.create({
    model: "gpt-4o-mini",
    input: history,
    store: true,
});

console.log(response.output_text);

// Add the response to the history
history = [
    ...history,
    ...response.output.map((el) => {
        // TODO: Remove this step
        delete el.id;
        return el;
    }),
];

history.push({
    role: "user",
    content: "tell me another",
});

const secondResponse = await openai.responses.create({
    model: "gpt-4o-mini",
    input: history,
    store: true,
});

console.log(secondResponse.output_text);
```

```python
from openai import OpenAI

client = OpenAI()

history = [
    {
        "role": "user",
        "content": "tell me a joke"
    }
]

response = client.responses.create(
    model="gpt-4o-mini",
    input=history,
    store=False
)

print(response.output_text)

# Add the response to the conversation
history += [{"role": el.role, "content": el.content} for el in response.output]

history.append({ "role": "user", "content": "tell me another" })

second_response = client.responses.create(
    model="gpt-4o-mini",
    input=history,
    store=False
)

print(second_response.output_text)
```

OpenAI APIs for conversation state
----------------------------------

Our APIs make it easier to manage conversation state automatically, so you don't have to do pass inputs manually with each turn of a conversation.

Share context across generated responses with the `previous_response_id` parameter. This parameter lets you chain responses and create a threaded conversation.

In the following example, we ask the model to tell a joke. Separately, we ask the model to explain why it's funny, and the model has all necessary context to deliver a good response.

Manually manage conversation state with the Responses API.

```javascript
import OpenAI from "openai";

const openai = new OpenAI();

const response = await openai.responses.create({
    model: "gpt-4o-mini",
    input: "tell me a joke",
    store: true,
});

console.log(response.output_text);

const secondResponse = await openai.responses.create({
    model: "gpt-4o-mini",
    previous_response_id: response.id,
    input: [{"role": "user", "content": "explain why this is funny."}],
    store: true,
});

console.log(secondResponse.output_text);
```

```python
from openai import OpenAI
client = OpenAI()

response = client.responses.create(
    model="gpt-4o-mini",
    input="tell me a joke",
)
print(response.output_text)

second_response = client.responses.create(
    model="gpt-4o-mini",
    previous_response_id=response.id,
    input=[{"role": "user", "content": "explain why this is funny."}],
)
print(second_response.output_text)
```

Even when using `previous_response_id`, all previous input tokens for responses in the chain are billed as input tokens in the API.

Managing the context window
---------------------------

Understanding context windows will help you successfully create threaded conversations and manage state across model interactions.

The **context window** is the maximum number of tokens that can be used in a single request. This max tokens number includes input, output, and reasoning tokens. To learn your model's context window, see [model details](/docs/models).

### Managing context for text generation

As your inputs become more complex, or you include more turns in a conversation, you'll need to consider both **output token** and **context window** limits. Model inputs and outputs are metered in [**tokens**](https://help.openai.com/en/articles/4936856-what-are-tokens-and-how-to-count-them), which are parsed from inputs to analyze their content and intent and assembled to render logical outputs. Models have limits on token usage during the lifecycle of a text generation request.

*   **Output tokens** are the tokens generated by a model in response to a prompt. Each model has different [limits for output tokens](/docs/models). For example, `gpt-4o-2024-08-06` can generate a maximum of 16,384 output tokens.
*   A **context window** describes the total tokens that can be used for both input and output tokens (and for some models, [reasoning tokens](/docs/guides/reasoning)). Compare the [context window limits](/docs/models) of our models. For example, `gpt-4o-2024-08-06` has a total context window of 128k tokens.

If you create a very large prompt—often by including extra context, data, or examples for the model—you run the risk of exceeding the allocated context window for a model, which might result in truncated outputs.

Use the [tokenizer tool](/tokenizer), built with the [tiktoken library](https://github.com/openai/tiktoken), to see how many tokens are in a particular string of text.

For example, when making an API request to the [Responses API](/docs/api-reference/responses) with a reasoning enabled model, like the [o1 model](/docs/guides/reasoning), the following token counts will apply toward the context window total:

*   Input tokens (inputs you include in the `input` array for the [Responses API](/docs/api-reference/responses))
*   Output tokens (tokens generated in response to your prompt)
*   Reasoning tokens (used by the model to plan a response)

Tokens generated in excess of the context window limit may be truncated in API responses.

![context window visualization](https://cdn.openai.com/API/docs/images/context-window.png)

You can estimate the number of tokens your messages will use with the [tokenizer tool](/tokenizer).

Next steps
----------

For more specific examples and use cases, visit the [OpenAI Cookbook](https://cookbook.openai.com), or learn more about using the APIs to extend model capabilities:

*   [Receive JSON responses with Structured Outputs](/docs/guides/structured-outputs)
*   [Extend the models with function calling](/docs/guides/function-calling)
*   [Enable streaming for real-time responses](/docs/guides/streaming-responses)
*   [Build a computer using agent](/docs/guides/tools-computer-use)

Was this page useful?
Streaming API responses
=======================

Learn how to stream model responses from the OpenAI API using server-sent events.

By default, when you make a request to the OpenAI API, we generate the model's entire output before sending it back in a single HTTP response. When generating long outputs, waiting for a response can take time. Streaming responses lets you start printing or processing the beginning of the model's output while it continues generating the full response.

Enable streaming
----------------

To start streaming responses, set `stream=True` in your request to the Responses endpoint:

```javascript
import { OpenAI } from "openai";
const client = new OpenAI();

const stream = await client.responses.create({
    model: "gpt-4o",
    input: [
        {
            role: "user",
            content: "Say 'double bubble bath' ten times fast.",
        },
    ],
    stream: true,
});

for await (const event of stream) {
    console.log(event);
}
```

```python
from openai import OpenAI
client = OpenAI()

stream = client.responses.create(
    model="gpt-4o",
    input=[
        {
            "role": "user",
            "content": "Say 'double bubble bath' ten times fast.",
        },
    ],
    stream=True,
)

for event in stream:
    print(event)
```

The Responses API uses semantic events for streaming. Each event is typed with a predefined schema, so you can listen for events you care about.

For a full list of event types, see the [API reference for streaming](/docs/api-reference/responses-streaming). Here are a few examples:

```python
type StreamingEvent = 
	| ResponseCreatedEvent
	| ResponseInProgressEvent
	| ResponseFailedEvent
	| ResponseCompletedEvent
	| ResponseOutputItemAdded
	| ResponseOutputItemDone
	| ResponseContentPartAdded
	| ResponseContentPartDone
	| ResponseOutputTextDelta
	| ResponseOutputTextAnnotationAdded
	| ResponseTextDone
	| ResponseRefusalDelta
	| ResponseRefusalDone
	| ResponseFunctionCallArgumentsDelta
	| ResponseFunctionCallArgumentsDone
	| ResponseFileSearchCallInProgress
	| ResponseFileSearchCallSearching
	| ResponseFileSearchCallCompleted
	| ResponseCodeInterpreterInProgress
	| ResponseCodeInterpreterCallCodeDelta
	| ResponseCodeInterpreterCallCodeDone
	| ResponseCodeInterpreterCallIntepreting
	| ResponseCodeInterpreterCallCompleted
	| Error
```

Read the responses
------------------

If you're using our SDK, every event is a typed instance. You can also identity individual events using the `type` property of the event.

Some key lifecycle events are emitted only once, while others are emitted multiple times as the response is generated. Common events to listen for when streaming text are:

```text
- `response.created`
- `response.output_text.delta`
- `response.completed`
- `error`
```

For a full list of events you can listen for, see the [API reference for streaming](/docs/api-reference/responses-streaming).

Advanced use cases
------------------

For more advanced use cases, like streaming tool calls, check out the following dedicated guides:

*   [Streaming function calls](/docs/guides/function-calling#streaming)
*   [Streaming structured output](/docs/guides/structured-outputs#streaming)

Moderation risk
---------------

Note that streaming the model's output in a production application makes it more difficult to moderate the content of the completions, as partial completions may be more difficult to evaluate. This may have implications for approved usage.

Was this page useful?
File inputs
===========

Learn how to use PDF files as inputs to the OpenAI API.

OpenAI models with vision capabilities can also accept PDF files as input. Provide PDFs either as Base64-encoded data or as file IDs obtained after uploading files to the `/v1/files` endpoint through the [API](/docs/api-reference/files) or [dashboard](/storage/files/).

How it works
------------

To help models understand PDF content, we put into the model's context both the extracted text and an image of each page. The model can then use both the text and the images to generate a response. This is useful, for example, if diagrams contain key information that isn't in the text.

Uploading files
---------------

In the example below, we first upload a PDF using the [Files API](/docs/api-reference/files), then reference its file ID in an API request to the model.

Upload a file to use in a response

```bash
curl https://api.openai.com/v1/files \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -F purpose="user_data" \
    -F file="@draconomicon.pdf"

curl "https://api.openai.com/v1/responses" \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -d '{
        "model": "gpt-4o",
        "input": [
            {
                "role": "user",
                "content": [
                    {
                        "type": "input_file",
                        "file_id": "file-6F2ksmvXxt4VdoqmHRw6kL"
                    },
                    {
                        "type": "input_text",
                        "text": "What is the first dragon in the book?"
                    }
                ]
            }
        ]
    }'
```

```javascript
import fs from "fs";
import OpenAI from "openai";
const client = new OpenAI();

const file = await client.files.create({
    file: fs.createReadStream("draconomicon.pdf"),
    purpose: "user_data",
});

const response = await client.responses.create({
    model: "gpt-4o",
    input: [
        {
            role: "user",
            content: [
                {
                    type: "input_file",
                    file_id: file.id,
                },
                {
                    type: "input_text",
                    text: "What is the first dragon in the book?",
                },
            ],
        },
    ],
});

console.log(response.output_text);
```

```python
from openai import OpenAI
client = OpenAI()

file = client.files.create(
    file=open("draconomicon.pdf", "rb"),
    purpose="user_data"
)

response = client.responses.create(
    model="gpt-4o",
    input=[
        {
            "role": "user",
            "content": [
                {
                    "type": "input_file",
                    "file_id": file.id,
                },
                {
                    "type": "input_text",
                    "text": "What is the first dragon in the book?",
                },
            ]
        }
    ]
)

print(response.output_text)
```

Base64-encoded files
--------------------

You can send PDF file inputs as Base64-encoded inputs as well.

Base64 encode a file to use in a response

```bash
curl "https://api.openai.com/v1/responses" \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -d '{
        "model": "gpt-4o",
        "input": [
            {
                "role": "user",
                "content": [
                    {
                        "type": "input_file",
                        "filename": "draconomicon.pdf",
                        "file_data": "...base64 encoded PDF bytes here..."
                    },
                    {
                        "type": "input_text",
                        "text": "What is the first dragon in the book?"
                    }
                ]
            }
        ]
    }'
```

```javascript
import fs from "fs";
import OpenAI from "openai";
const client = new OpenAI();

const data = fs.readFileSync("draconomicon.pdf");
const base64String = data.toString("base64");

const response = await client.responses.create({
    model: "gpt-4o",
    input: [
        {
            role: "user",
            content: [
                {
                    type: "input_file",
                    filename: "draconomicon.pdf",
                    file_data: `data:application/pdf;base64,${base64String}`,
                },
                {
                    type: "input_text",
                    text: "What is the first dragon in the book?",
                },
            ],
        },
    ],
});

console.log(response.output_text);
```

```python
import base64
from openai import OpenAI
client = OpenAI()

with open("draconomicon.pdf", "rb") as f:
    data = f.read()

base64_string = base64.b64encode(data).decode("utf-8")

response = client.responses.create(
    model="gpt-4o",
    input=[
        {
            "role": "user",
            "content": [
                {
                    "type": "input_file",
                    "filename": "draconomicon.pdf",
                    "file_data": f"data:application/pdf;base64,{base64_string}",
                },
                {
                    "type": "input_text",
                    "text": "What is the first dragon in the book?",
                },
            ],
        },
    ]
)

print(response.output_text)
```

Usage considerations
--------------------

Below are a few considerations to keep in mind while using PDF inputs.

**Token usage**

To help models understand PDF content, we put into the model's context both extracted text and an image of each page—regardless of whether the page includes images. Before deploying your solution at scale, ensure you understand the pricing and token usage implications of using PDFs as input. [More on pricing](/docs/pricing).

**File size limitations**

You can upload up to 100 pages and 32MB of total content in a single request to the API, across multiple file inputs.

**Supported models**

Only models that support both text and image inputs, such as gpt-4o, gpt-4o-mini, or o1, can accept PDF files as input. [Check model features here](/docs/models).

**File upload purpose**

You can upload these files to the Files API with any [purpose](/docs/api-reference/files/create#files-create-purpose), but we recommend using the `user_data` purpose for files you plan to use as model inputs.

Next steps
----------

Now that you known the basics of text inputs and outputs, you might want to check out one of these resources next.

[

Experiment with PDF inputs in the Playground

Use the Playground to develop and iterate on prompts with PDF inputs.

](/playground)[

Full API reference

Check out the API reference for more options.

](/docs/api-reference/responses)

Was this page useful?
Reasoning models
================

Explore advanced reasoning and problem-solving models.

**Reasoning models**, like OpenAI o1 and o3-mini, are new large language models trained with reinforcement learning to perform complex reasoning. Reasoning models [think before they answer](https://openai.com/index/introducing-openai-o1-preview/), producing a long internal chain of thought before responding to the user. Reasoning models excel in complex problem solving, coding, scientific reasoning, and multi-step planning for agentic workflows.

As with our GPT models, we provide both a smaller, faster model (`o3-mini`) that is less expensive per token, and a larger model (`o1`) that is somewhat slower and more expensive, but can often generate better responses for complex tasks, and generalize better across domains.

The new [o1-pro model](/docs/models/o1-pro) has unique features like making multiple model generation turns before generating a response. To support this and other advanced API features in the future, this model is currently only available in the [Responses API](/docs/api-reference/responses).

Get started with reasoning
--------------------------

Reasoning models can be used through the [Responses API](/docs/api-reference/responses/create) as seen here.

Using a reasoning model in the Responses API

```javascript
import OpenAI from "openai";

const openai = new OpenAI();

const prompt = `
Write a bash script that takes a matrix represented as a string with 
format '[1,2],[3,4],[5,6]' and prints the transpose in the same format.
`;

const response = await openai.responses.create({
    model: "o3-mini",
    reasoning: { effort: "medium" },
    input: [
        {
            role: "user",
            content: prompt,
        },
    ],
});

console.log(response.output_text);
```

```python
from openai import OpenAI

client = OpenAI()

prompt = """
Write a bash script that takes a matrix represented as a string with 
format '[1,2],[3,4],[5,6]' and prints the transpose in the same format.
"""

response = client.responses.create(
    model="o3-mini",
    reasoning={"effort": "medium"},
    input=[
        {
            "role": "user", 
            "content": prompt
        }
    ]
)

print(response.output_text)
```

```bash
curl https://api.openai.com/v1/responses \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "o3-mini",
    "reasoning": {"effort": "medium"},
    "input": [
      {
        "role": "user",
        "content": "Write a bash script that takes a matrix represented as a string with format \"[1,2],[3,4],[5,6]\" and prints the transpose in the same format."
      }
    ]
  }'
```

### Reasoning effort

In the example above, the `reasoning.effort` parameter is used to give the model guidance on how many reasoning tokens it should generate before creating a response to the prompt.

You can specify one of `low`, `medium`, or `high` for this parameter, where `low` will favor speed and economical token usage, and `high` will favor more complete reasoning at the cost of more tokens generated and slower responses. The default value is `medium`, which is a balance between speed and reasoning accuracy.

How reasoning works
-------------------

Reasoning models introduce **reasoning tokens** in addition to input and output tokens. The models use these reasoning tokens to "think", breaking down their understanding of the prompt and considering multiple approaches to generating a response. After generating reasoning tokens, the model produces an answer as visible completion tokens, and discards the reasoning tokens from its context.

Here is an example of a multi-step conversation between a user and an assistant. Input and output tokens from each step are carried over, while reasoning tokens are discarded.

![Reasoning tokens aren't retained in context](https://cdn.openai.com/API/images/guides/reasoning_tokens.png)

While reasoning tokens are not visible via the API, they still occupy space in the model's context window and are billed as [output tokens](https://openai.com/api/pricing).

### Managing the context window

It's important to ensure there's enough space in the context window for reasoning tokens when creating responses. Depending on the problem's complexity, the models may generate anywhere from a few hundred to tens of thousands of reasoning tokens. The exact number of reasoning tokens used is visible in the [usage object of the response object](/docs/api-reference/responses/object), under `output_tokens_details`:

```json
{
  "usage": {
    "input_tokens": 75,
    "input_tokens_details": {
      "cached_tokens": 0
    },
    "output_tokens": 1186,
    "output_tokens_details": {
      "reasoning_tokens": 1024
    },
    "total_tokens": 1261
  }
}
```

Context window lengths are found on the [model reference page](/docs/models), and will differ across model snapshots.

### Controlling costs

To manage costs with reasoning models, you can limit the total number of tokens the model generates (including both reasoning and final output tokens) by using the [`max_output_tokens`](/docs/api-reference/responses/create#responses-create-max_output_tokens) parameter.

### Allocating space for reasoning

If the generated tokens reach the context window limit or the `max_output_tokens` value you've set, you'll receive a response with a `status` of `incomplete` and `incomplete_details` with `reason` set to `max_output_tokens`. This might occur before any visible output tokens are produced, meaning you could incur costs for input and reasoning tokens without receiving a visible response.

To prevent this, ensure there's sufficient space in the context window or adjust the `max_output_tokens` value to a higher number. OpenAI recommends reserving at least 25,000 tokens for reasoning and outputs when you start experimenting with these models. As you become familiar with the number of reasoning tokens your prompts require, you can adjust this buffer accordingly.

Handling incomplete responses

```javascript
import OpenAI from "openai";

const openai = new OpenAI();

const prompt = `
Write a bash script that takes a matrix represented as a string with 
format '[1,2],[3,4],[5,6]' and prints the transpose in the same format.
`;

const response = await openai.responses.create({
    model: "o3-mini",
    reasoning: { effort: "medium" },
    input: [
        {
            role: "user",
            content: prompt,
        },
    ],
    max_output_tokens: 300,
});

if (
    response.status === "incomplete" &&
    response.incomplete_details.reason === "max_output_tokens"
) {
    console.log("Ran out of tokens");
    if (response.output_text?.length > 0) {
        console.log("Partial output:", response.output_text);
    } else {
        console.log("Ran out of tokens during reasoning");
    }
}
```

```python
from openai import OpenAI

client = OpenAI()

prompt = """
Write a bash script that takes a matrix represented as a string with 
format '[1,2],[3,4],[5,6]' and prints the transpose in the same format.
"""

response = client.responses.create(
    model="o3-mini",
    reasoning={"effort": "medium"},
    input=[
        {
            "role": "user", 
            "content": prompt
        }
    ],
    max_output_tokens=300,
)

if response.status == "incomplete" and response.incomplete_details.reason == "max_output_tokens":
    print("Ran out of tokens")
    if response.output_text:
        print("Partial output:", response.output_text)
    else: 
        print("Ran out of tokens during reasoning")
```

Advice on prompting
-------------------

There are some differences to consider when prompting a reasoning model versus prompting a GPT model. Generally speaking, reasoning models will provide better results on tasks with only high-level guidance. This differs somewhat from GPT models, which often benefit from very precise instructions.

*   A reasoning model is like a senior co-worker—you can give them a goal to achieve and trust them to work out the details.
*   A GPT model is like a junior coworker—they'll perform best with explicit instructions to create a specific output.

For more information on best practices when using reasoning models, [refer to this guide](/docs/guides/reasoning-best-practices).

### Prompt examples

Coding (refactoring)

OpenAI o-series models are able to implement complex algorithms and produce code. This prompt asks o1 to refactor a React component based on some specific criteria.

Refactor code

```javascript
import OpenAI from "openai";

const openai = new OpenAI();

const prompt = `
Instructions:
- Given the React component below, change it so that nonfiction books have red
  text. 
- Return only the code in your reply
- Do not include any additional formatting, such as markdown code blocks
- For formatting, use four space tabs, and do not allow any lines of code to 
  exceed 80 columns

const books = [
  { title: 'Dune', category: 'fiction', id: 1 },
  { title: 'Frankenstein', category: 'fiction', id: 2 },
  { title: 'Moneyball', category: 'nonfiction', id: 3 },
];

export default function BookList() {
  const listItems = books.map(book =>
    <li>
      {book.title}
    </li>
  );

  return (
    <ul>{listItems}</ul>
  );
}
`.trim();

const response = await openai.responses.create({
    model: "o3-mini",
    input: [
        {
            role: "user",
            content: prompt,
        },
    ],
});

console.log(response.output_text);
```

```python
from openai import OpenAI

client = OpenAI()

prompt = """
Instructions:
- Given the React component below, change it so that nonfiction books have red
  text. 
- Return only the code in your reply
- Do not include any additional formatting, such as markdown code blocks
- For formatting, use four space tabs, and do not allow any lines of code to 
  exceed 80 columns

const books = [
  { title: 'Dune', category: 'fiction', id: 1 },
  { title: 'Frankenstein', category: 'fiction', id: 2 },
  { title: 'Moneyball', category: 'nonfiction', id: 3 },
];

export default function BookList() {
  const listItems = books.map(book =>
    <li>
      {book.title}
    </li>
  );

  return (
    <ul>{listItems}</ul>
  );
}
"""

response = client.responses.create(
    model="o3-mini",
    input=[
        {
            "role": "user",
            "content": prompt,
        }
    ]
)

print(response.output_text)
```

Coding (planning)

OpenAI o-series models are also adept in creating multi-step plans. This example prompt asks o1 to create a filesystem structure for a full solution, along with Python code that implements the desired use case.

Plan and create a Python project

```javascript
import OpenAI from "openai";

const openai = new OpenAI();

const prompt = `
I want to build a Python app that takes user questions and looks 
them up in a database where they are mapped to answers. If there 
is close match, it retrieves the matched answer. If there isn't, 
it asks the user to provide an answer and stores the 
question/answer pair in the database. Make a plan for the directory 
structure you'll need, then return each file in full. Only supply 
your reasoning at the beginning and end, not throughout the code.
`.trim();

const response = await openai.responses.create({
    model: "o3-mini",
    input: [
        {
            role: "user",
            content: prompt,
        },
    ],
});

console.log(response.output_text);
```

```python
from openai import OpenAI

client = OpenAI()

prompt = """
I want to build a Python app that takes user questions and looks 
them up in a database where they are mapped to answers. If there 
is close match, it retrieves the matched answer. If there isn't, 
it asks the user to provide an answer and stores the 
question/answer pair in the database. Make a plan for the directory 
structure you'll need, then return each file in full. Only supply 
your reasoning at the beginning and end, not throughout the code.
"""

response = client.responses.create(
    model="o3-mini",
    input=[
        {
            "role": "user",
            "content": prompt,
        }
    ]
)

print(response.output_text)
```

STEM Research

OpenAI o-series models have shown excellent performance in STEM research. Prompts asking for support of basic research tasks should show strong results.

Ask questions related to basic scientific research

```javascript
import OpenAI from "openai";

const openai = new OpenAI();

const prompt = `
What are three compounds we should consider investigating to 
advance research into new antibiotics? Why should we consider 
them?
`;

const response = await openai.responses.create({
    model: "o3-mini",
    input: [
        {
            role: "user",
            content: prompt,
        },
    ],
});

console.log(response.output_text);
```

```python
from openai import OpenAI

client = OpenAI()

prompt = """
What are three compounds we should consider investigating to 
advance research into new antibiotics? Why should we consider 
them?
"""

response = client.responses.create(
    model="o3-mini",
    input=[
        {
            "role": "user", 
            "content": prompt
        }
    ]
)

print(response.output_text)
```

Use case examples
-----------------

Some examples of using reasoning models for real-world use cases can be found in [the cookbook](https://cookbook.openai.com).

[](https://cookbook.openai.com/examples/o1/using_reasoning_for_data_validation)

[](https://cookbook.openai.com/examples/o1/using_reasoning_for_data_validation)

[Using reasoning for data validation](https://cookbook.openai.com/examples/o1/using_reasoning_for_data_validation)

[](https://cookbook.openai.com/examples/o1/using_reasoning_for_data_validation)

[Evaluate a synthetic medical data set for discrepancies.](https://cookbook.openai.com/examples/o1/using_reasoning_for_data_validation)

[](https://cookbook.openai.com/examples/o1/using_reasoning_for_routine_generation)

[](https://cookbook.openai.com/examples/o1/using_reasoning_for_routine_generation)

[Using reasoning for routine generation](https://cookbook.openai.com/examples/o1/using_reasoning_for_routine_generation)

[](https://cookbook.openai.com/examples/o1/using_reasoning_for_routine_generation)

[Use help center articles to generate actions that an agent could perform.](https://cookbook.openai.com/examples/o1/using_reasoning_for_routine_generation)

Was this page useful?
Evaluating model performance
============================

Test and improve model outputs through evaluations.

Evaluations (often called **evals**) test model outputs to ensure they meet style and content criteria that you specify. Writing evals to understand how your LLM applications are performing against your expectations, especially when upgrading or trying new models, is an essential component to building reliable applications.

In this guide, we will focus on **configuring evals programmatically using the [Evals API](/docs/api-reference/evals)**. If you prefer, you can also configure evals [in the OpenAI dashboard](/evaluations).

Broadly, there are three steps to build and run evals for your LLM application.

1.  Describe the task to be done as an eval
2.  Run your eval with test inputs (a prompt and input data)
3.  Analyze the results, then iterate and improve on your prompt

This process is somewhat similar to behavior-driven development (BDD), where you begin by specifying how the system should behave before implementing and testing the system. Let's see how we would complete each of the steps above using the [Evals API](/docs/api-reference/evals).

Create an eval for a task
-------------------------

Creating an eval begins by describing a task to be done by a model. Let's say that we would like to use a model to classify the contents of IT support tickets into one of three categories: `Hardware`, `Software`, or `Other`.

To implement this use case with the [Chat Completions API](/docs/api-reference/chat), you might write code like this that combines a [developer message](/docs/guides/text) with a user message containing the text of a support ticket.

Categorize IT support tickets

```bash
curl https://api.openai.com/v1/chat/completions \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -d '{
        "model": "gpt-4o",
        "messages": [
            {
                "role": "developer",
                "content": "Categorize the following support ticket into one of Hardware, Software, or Other."
            },
            {
                "role": "user",
                "content": "My monitor wont turn on - help!"
            }
        ]
    }'
```

```javascript
import OpenAI from "openai";
const client = new OpenAI();

const instructions = `
You are an expert in categorizing IT support tickets. Given the support 
ticket below, categorize the request into one of "Hardware", "Software", 
or "Other". Respond with only one of those words.
`;

const ticket = "My monitor won't turn on - help!";

const completion = await client.chat.completions.create({
    model: "gpt-4o",
    messages: [
        { role: "developer", content: instructions },
        { role: "user", content: ticket },
    ],
});

console.log(completion.choices[0].message.content);
```

```python
from openai import OpenAI
client = OpenAI()

instructions = """
You are an expert in categorizing IT support tickets. Given the support 
ticket below, categorize the request into one of "Hardware", "Software", 
or "Other". Respond with only one of those words.
"""

ticket = "My monitor won't turn on - help!"

completion = client.chat.completions.create(
    model="gpt-4o",
    messages=[
        {"role": "developer", "content": instructions},
        {"role": "user", "content": ticket}
    ]
)

print(completion.choices[0].message.content)
```

Let's set up an eval to test this behavior [via API](\(/docs/api-reference/evals\)). An eval needs two key ingredients:

*   A schema for the test data you will use along with the eval (`data_source_config`)
*   The criteria that determine if the model output is correct (`testing_criteria`)

```bash
curl https://api.openai.com/v1/evals \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -H "Content-Type: application/json" \
    -d '{
        "name": "IT Ticket Categorization",
        "data_source_config": {
            "type": "custom",
            "item_schema": {
                "type": "object",
                "properties": {
                    "ticket_text": { "type": "string" },
                    "correct_label": { "type": "string" }
                },
                "required": ["ticket_text", "correct_label"]
            },
            "include_sample_schema": true
        },
        "testing_criteria": [
            {
                "type": "string_check",
                "name": "Match output to human label",
                "input": "{{ sample.output_text }}",
                "operation": "eq",
                "reference": "{{ item.correct_label }}"
            }
        ]
    }'
```

Explanation: data\_source\_config parameter

Running this eval will require a test data set that represents the type of data you expect your prompt to work with (more on creating the test data set later in this guide). In our `data_source_config` parameter, we specify that each **item** in the data set will conform to a [JSON schema](https://json-schema.org/) with two properties:

*   `ticket_text`: a string of text with the contents of a support ticket
*   `correct_label`: a "ground truth" output that the model should match, provided by a human

Since we will be referencing a **sample** in our test criteria (the output generated by a model given our prompt), we also set `include_sample_schema` to `true`.

```json
{
    "type": "custom",
    "item_schema": {
        "type": "object",
        "properties": {
            "ticket": { "type": "string" },
            "category": { "type": "string" }
        },
        "required": ["ticket", "category"]
    },
    "include_sample_schema": true
}
```

Explanation: testing\_criteria parameter

In our `testing_criteria`, we define how we will conclude if the model output satisfies our requirements for each item in the data set. In this case, we just want the model to output one of three category strings based on the input ticket. The string it outputs should exactly match the human-labeled `correct_label` field in our test data. So in this case, we will want to use a `string_check` grader to evaluate the output.

In the test configuration, we will introduce template syntax, represented by the `{{` and `}}` brackets below. This is how we will insert dynamic content into the test for this eval.

*   `{{ item.correct_label }}` refers to the ground truth value in our test data.
*   `{{ sample.output_text }}` refers to the content we will generate from a model to evaluate our prompt - we'll show how to do that when we actually kick off the eval run.

```json
{
    "type": "string_check",
    "name": "Category string match",
    "input": "{{ sample.output_text }}",
    "operation": "eq",
    "reference": "{{ item.category }}"
}
```

After creating the eval, it will be assigned a UUID that you will need to address it later when kicking off a run.

```json
{
  "object": "eval",
  "id": "eval_67e321d23b54819096e6bfe140161184",
  "data_source_config": {
    "type": "custom",
    "schema": { ... omitted for brevity... }
  },
  "testing_criteria": [
    {
      "name": "Match output to human label",
      "id": "Match output to human label-c4fdf789-2fa5-407f-8a41-a6f4f9afd482",
      "type": "string_check",
      "input": "{{ sample.output_text }}",
      "reference": "{{ item.correct_label }}",
      "operation": "eq"
    }
  ],
  "name": "IT Ticket Categorization",
  "created_at": 1742938578,
  "metadata": {}
}
```

Now that we've created an eval that describes the desired behavior of our application, let's test a prompt with a set of test data.

Test a prompt with your eval
----------------------------

Now that we have defined how we want our app to behave in an eval, let's construct a prompt that reliably generates the correct output for a representative sample of test data.

### Uploading test data

There are several ways to provide test data for eval runs, but it may be convenient to upload a [JSONL](https://jsonlines.org/) file that contains data in the schema we specified when we created our eval. A sample JSONL file that conforms to the schema we set up is below:

```json
{ "item": { "ticket_text": "My monitor won't turn on!", "correct_label:": "Hardware" } }
{ "item": { "ticket_text": "I'm in vim and I can't quit!", "correct_label:": "Software" } }
{ "item": { "ticket_text": "Best restaurants in Cleveland?", "correct_label:": "Other" } }
```

This data set contains both test inputs and ground truth labels to compare model outputs against.

Next, let's upload our test data file to the OpenAI platform so we can reference it later. You can upload files [in the dashboard here](/storage/files), but it's possible to [upload files via API](/docs/api-reference/files/create) as well. The samples below assume you are running the command in a directory where you saved the sample JSON data above to a file called `tickets.jsonl`:

Upload a test data file

```bash
curl https://api.openai.com/v1/files \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -F purpose="evals" \
  -F file="@tickets.jsonl"
```

```javascript
import fs from "fs";
import OpenAI from "openai";

const openai = new OpenAI();

const file = await openai.files.create({
    file: fs.createReadStream("tickets.jsonl"),
    purpose: "evals",
});

console.log(file);
```

```python
from openai import OpenAI
client = OpenAI()

const file = client.files.create(
    file=open("tickets.jsonl", "rb"),
    purpose="evals"
)

print(file)
```

When you upload the file, make note of the unique `id` property in the response payload (also available in the UI if you uploaded via the browser) - we will need to reference that value later:

```json
{
    "object": "file",
    "id": "file-CwHg45Fo7YXwkWRPUkLNHW",
    "purpose": "evals",
    "filename": "tickets.jsonl",
    "bytes": 208,
    "created_at": 1742834798,
    "expires_at": null,
    "status": "processed",
    "status_details": null
}
```

### Creating an eval run

With our test data in place, let's evaluate a prompt and see how it performs against our test criteria. Via API, we can do this by [creating an eval run](/docs/api-reference/evals/createRun).

Make sure to replace `YOUR_EVAL_ID` and `YOUR_FILE_ID` with the unique IDs of the eval configuration and test data files you created in the steps above.

```bash
curl https://api.openai.com/v1/evals/YOUR_EVAL_ID/runs \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -H "Content-Type: application/json" \
    -d '{
        "name": "Categorization text run",
        "data_source": {
            "type": "completions",
            "model": "gpt-4o",
            "input": [
                {
                    "role": "developer",
                    "content": "You are an expert in categorizing IT support tickets. Given the support ticket below, categorize the request into one of \"Hardware\", \"Software\", or \"Other\". Respond with only one of those words."
                },
                {
                    "role": "user",
                    "content": "\{\{ item.ticket_text \}\}"
                }
            ],
            "source": {
                "type": "file_id",
                "id": "YOUR_FILE_ID"
            }
        }
    }'
```

When we create the run, we set up a [Chat Completions](/docs/guides/text?api-mode=chat) messages array with the prompt we would like to test. This prompt is used to generate a model response for every line of test data in your data set. We can use the double curly brace syntax to template in the dynamic variable `item.ticket_text`, which is drawn from the current test data item.

If the eval run is successfully created, you'll receive an API response that looks like this:

```json
{
    "object": "eval.run",
    "id": "evalrun_67e44c73eb6481909f79a457749222c7",
    "eval_id": "eval_67e44c5becec81909704be0318146157",
    "report_url": "https://platform.openai.com/evaluations/abc123",
    "status": "queued",
    "model": "gpt-4o",
    "name": "Categorization text run",
    "created_at": 1743015028,
    "result_counts": { ... },
    "per_model_usage": null,
    "per_testing_criteria_results": null,
    "data_source": {
        "type": "completions",
        "source": {
            "type": "file_id",
            "id": "file-J7MoX9ToHXp2TutMEeYnwj"
        },
        "input_messages": {
            "type": "template",
            "template": [
                {
                    "type": "message",
                    "role": "developer",
                    "content": {
                        "type": "input_text",
                        "text": "You are an expert in...."
                    }
                },
                {
                    "type": "message",
                    "role": "user",
                    "content": {
                        "type": "input_text",
                        "text": "{{item.ticket_text}}"
                    }
                }
            ]
        },
        "model": "gpt-4o",
        "sampling_params": null
    },
    "error": null,
    "metadata": {}
}
```

Your eval run has now been queued, and it will execute asynchronously as it processes every row in your data set. With our configuration, it will generate completions for testing with the prompt and model we specified.

Analyze the results
-------------------

Depending on the size of your dataset, the eval run may take some time to complete. You can view current status in the dashboard, but you can also [fetch the current status of an eval run via API](/docs/api-reference/evals/getRun):

```bash
curl https://api.openai.com/v1/evals/eval_abc123/runs/evalrun_abc123 \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -H "Content-Type: application/json"
```

You'll need the UUID of both your eval and eval run to fetch its status. When you do, you'll see eval run data that looks like this:

```json
{
  "object": "eval.run",
  "id": "evalrun_67e44c73eb6481909f79a457749222c7",
  "eval_id": "eval_67e44c5becec81909704be0318146157",
  "report_url": "https://platform.openai.com/evaluations/xxx",
  "status": "completed",
  "model": "gpt-4o",
  "name": "Categorization text run",
  "created_at": 1743015028,
  "result_counts": {
    "total": 3,
    "errored": 0,
    "failed": 0,
    "passed": 3
  },
  "per_model_usage": [
    {
      "model_name": "gpt-4o-2024-08-06",
      "invocation_count": 3,
      "prompt_tokens": 166,
      "completion_tokens": 6,
      "total_tokens": 172,
      "cached_tokens": 0
    }
  ],
  "per_testing_criteria_results": [
    {
      "testing_criteria": "Match output to human label-40d67441-5000-4754-ab8c-181c125803ce",
      "passed": 3,
      "failed": 0
    }
  ],
  "data_source": {
    "type": "completions",
    "source": {
      "type": "file_id",
      "id": "file-J7MoX9ToHXp2TutMEeYnwj"
    },
    "input_messages": {
      "type": "template",
      "template": [
        {
          "type": "message",
          "role": "developer",
          "content": {
            "type": "input_text",
            "text": "You are an expert in categorizing IT support tickets. Given the support ticket below, categorize the request into one of Hardware, Software, or Other. Respond with only one of those words."
          }
        },
        {
          "type": "message",
          "role": "user",
          "content": {
            "type": "input_text",
            "text": "{{item.ticket_text}}"
          }
        }
      ]
    },
    "model": "gpt-4o",
    "sampling_params": null
  },
  "error": null,
  "metadata": {}
}
```

The API response contains granular information about test criteria results, API usage for generating model responses, and a `report_url` property that takes you to a page in the dashboard where you can explore the results visually.

In our simple test, the model reliably generated the content we wanted for a small test case sample. In reality, you will often have to run your eval with more criteria, different prompts, and different data sets. But the process above gives you all the tools you need to build robust evals for your LLM apps!

Video: evals in the dashboard
-----------------------------

The Evaulations tooling [in the OpenAI dashboard](/evaluations) evolves quickly and may not match exactly the UI shown below, but this video will give you a quick overview of how to set up and run evals using the browser-based UI.

Next steps
----------

Now you know how to create and run evals via API, and using the dashboard! Here are a few other resources that may be useful to you as you continue to improve your model results.

[

Cookbook: Detecting prompt regressions

Keep tabs on the performance of your prompts as you iterate on them.

](https://cookbook.openai.com/examples/evaluation/use-cases/regression)[

Cookbook: Bulk model and prompt experimentation

Compare the results of many different prompts and models at once.

](https://cookbook.openai.com/examples/evaluation/use-cases/bulk-experimentation)[

Cookbook: Monitoring stored completions

Examine stored completions to test for prompt regressions.

](https://cookbook.openai.com/examples/evaluation/use-cases/completion-monitoring)[

Fine-tuning

Improve a model's ability to generate responses tailored to your use case.

](/docs/guides/fine-tuning)[

Model distillation

Learn how to distill large model results to smaller, cheaper, and faster models.

](/docs/guides/distillation)

Was this page useful?
Built-in tools
==============

Use built-in tools like web search and file search to extend the model's capabilities.

When generating model responses, you can extend model capabilities using built-in **tools**. These tools help models access additional context and information from the web or your files. The example below uses the [web search tool](/docs/guides/tools-web-search) to use the latest information from the web to generate a model response.

Include web search results for the model response

```javascript
import OpenAI from "openai";
const client = new OpenAI();

const response = await client.responses.create({
    model: "gpt-4o",
    tools: [ { type: "web_search_preview" } ],
    input: "What was a positive news story from today?",
});

console.log(response.output_text);
```

```python
from openai import OpenAI
client = OpenAI()

response = client.responses.create(
    model="gpt-4o",
    tools=[{"type": "web_search_preview"}],
    input="What was a positive news story from today?"
)

print(response.output_text)
```

```bash
curl "https://api.openai.com/v1/responses" \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -d '{
        "model": "gpt-4o",
        "tools": [{"type": "web_search_preview"}],
        "input": "what was a positive news story from today?"
    }'
```

Available tools
---------------

Here's an overview of the tools available in the OpenAI platform—select one of them for further guidance on usage.

[

Web search

Include data from the Internet in model response generation.

](/docs/guides/tools-web-search)[

File search

Search the contents of uploaded files for context when generating a response.

](/docs/guides/tools-file-search)[

Computer use

Create agentic workflows that enable a model to control a computer interface.

](/docs/guides/tools-computer-use)[

Function calling

Enable the model to call custom code that you define, giving it access to additional data and capabilities.

](/docs/guides/function-calling)

Usage in the API
----------------

When making a request to generate a [model response](/docs/api-reference/responses/create), you can enable tool access by specifying configurations in the `tools` parameter. Each tool has its own unique configuration requirements—see the [Available tools](#available-tools) section for detailed instructions.

Based on the provided [prompt](/docs/guides/text), the model automatically decides whether to use a configured tool. For instance, if your prompt requests information beyond the model's training cutoff date and web search is enabled, the model will typically invoke the web search tool to retrieve relevant, up-to-date information.

You can explicitly control or guide this behavior by setting the `tool_choice` parameter [in the API request](/docs/api-reference/responses/create).

### Function calling

In addition to built-in tools, you can define custom functions using the `tools` array. These custom functions allow the model to call your application's code, enabling access to specific data or capabilities not directly available within the model.

Learn more in the [function calling guide](/docs/guides/function-calling).

Was this page useful?
Web search
==========

Allow models to search the web for the latest information before generating a response.

Using the [Responses API](/docs/api-reference/responses), you can enable web search by configuring it in the `tools` array in an API request to generate content. Like any other tool, the model can choose to search the web or not based on the content of the input prompt.

Web search tool example

```javascript
import OpenAI from "openai";
const client = new OpenAI();

const response = await client.responses.create({
    model: "gpt-4o",
    tools: [ { type: "web_search_preview" } ],
    input: "What was a positive news story from today?",
});

console.log(response.output_text);
```

```python
from openai import OpenAI
client = OpenAI()

response = client.responses.create(
    model="gpt-4o",
    tools=[{"type": "web_search_preview"}],
    input="What was a positive news story from today?"
)

print(response.output_text)
```

```bash
curl "https://api.openai.com/v1/responses" \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -d '{
        "model": "gpt-4o",
        "tools": [{"type": "web_search_preview"}],
        "input": "what was a positive news story from today?"
    }'
```

Web search tool versions

The current default version of the web search tool is:

`web_search_preview`

Which points to a dated version:

`web_search_preview_2025_03_11`

As the tool evolves, future dated snapshot versions will be documented in the [API reference](/docs/api-reference/responses/create).

You can also force the use of the `web_search_preview` tool by using the `tool_choice` parameter, and setting it to `{type: "web_search_preview"}` - this can help ensure lower latency and more consistent results.

Output and citations
--------------------

Model responses that use the web search tool will include two parts:

*   A `web_search_call` output item with the ID of the search call.
*   A `message` output item containing:
    *   The text result in `message.content[0].text`
    *   Annotations `message.content[0].annotations` for the cited URLs

By default, the model's response will include inline citations for URLs found in the web search results. In addition to this, the `url_citation` annotation object will contain the URL, title and location of the cited source.

When displaying web results or information contained in web results to end users, inline citations must be made clearly visible and clickable in your user interface.

```json
[
  {
    "type": "web_search_call",
    "id": "ws_67c9fa0502748190b7dd390736892e100be649c1a5ff9609",
    "status": "completed"
  },
  {
    "id": "msg_67c9fa077e288190af08fdffda2e34f20be649c1a5ff9609",
    "type": "message",
    "status": "completed",
    "role": "assistant",
    "content": [
      {
        "type": "output_text",
        "text": "On March 6, 2025, several news...",
        "annotations": [
          {
            "type": "url_citation",
            "start_index": 2606,
            "end_index": 2758,
            "url": "https://...",
            "title": "Title..."
          }
        ]
      }
    ]
  }
]
```

User location
-------------

To refine search results based on geography, you can specify an approximate user location using country, city, region, and/or timezone.

*   The `city` and `region` fields are free text strings, like `Minneapolis` and `Minnesota` respectively.
*   The `country` field is a two-letter [ISO country code](https://en.wikipedia.org/wiki/ISO_3166-1), like `US`.
*   The `timezone` field is an [IANA timezone](https://timeapi.io/documentation/iana-timezones) like `America/Chicago`.

Customizing user location

```python
from openai import OpenAI
client = OpenAI()

response = client.responses.create(
    model="gpt-4o",
    tools=[{
        "type": "web_search_preview",
        "user_location": {
            "type": "approximate",
            "country": "GB",
            "city": "London",
            "region": "London",
        }
    }],
    input="What are the best restaurants around Granary Square?",
)

print(response.output_text)
```

```javascript
import OpenAI from "openai";
const openai = new OpenAI();

const response = await openai.responses.create({
    model: "gpt-4o",
    tools: [{
        type: "web_search_preview",
        user_location: {
            type: "approximate",
            country: "GB",
            city: "London",
            region: "London"
        }
    }],
    input: "What are the best restaurants around Granary Square?",
});
console.log(response.output_text);
```

```bash
curl "https://api.openai.com/v1/responses" \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -d '{
        "model": "gpt-4o",
        "tools": [{
            "type": "web_search_preview",
            "user_location": {
                "type": "approximate",
                "country": "GB",
                "city": "London",
                "region": "London"
            }
        }],
        "input": "What are the best restaurants around Granary Square?"
    }'
```

Search context size
-------------------

When using this tool, the `search_context_size` parameter controls how much context is retrieved from the web to help the tool formulate a response. The tokens used by the search tool do **not** affect the context window of the main model specified in the `model` parameter in your response creation request. These tokens are also **not** carried over from one turn to another — they're simply used to formulate the tool response and then discarded.

Choosing a context size impacts:

*   **Cost**: Pricing of our search tool varies based on the value of this parameter. Higher context sizes are more expensive. See tool pricing [here](/docs/pricing).
*   **Quality**: Higher search context sizes generally provide richer context, resulting in more accurate, comprehensive answers.
*   **Latency**: Higher context sizes require processing more tokens, which can slow down the tool's response time.

Available values:

*   **`high`**: Most comprehensive context, highest cost, slower response.
*   **`medium`** (default): Balanced context, cost, and latency.
*   **`low`**: Least context, lowest cost, fastest response, but potentially lower answer quality.

Again, tokens used by the search tool do **not** impact main model's token usage and are not carried over from turn to turn. Check the [pricing page](/docs/pricing) for details on costs associated with each context size.

Customizing search context size

```python
from openai import OpenAI
client = OpenAI()

response = client.responses.create(
    model="gpt-4o",
    tools=[{
        "type": "web_search_preview",
        "search_context_size": "low",
    }],
    input="What movie won best picture in 2025?",
)

print(response.output_text)
```

```javascript
import OpenAI from "openai";
const openai = new OpenAI();

const response = await openai.responses.create({
    model: "gpt-4o",
    tools: [{
        type: "web_search_preview",
        search_context_size: "low",
    }],
    input: "What movie won best picture in 2025?",
});
console.log(response.output_text);
```

```bash
curl "https://api.openai.com/v1/responses" \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -d '{
        "model": "gpt-4o",
        "tools": [{
            "type": "web_search_preview",
            "search_context_size": "low"
        }],
        "input": "What movie won best picture in 2025?"
    }'
```

Limitations
-----------

Below are a few notable implementation considerations when using web search.

*   The [`gpt-4o-search-preview`](/docs/models/gpt-4o-search-preview) and [`gpt-4o-mini-search-preview`](/docs/models/gpt-4o-mini-search-preview) models used in Chat Completions only support a subset of API parameters - view their model data pages for specific information on rate limits and feature support.
*   When used as a tool in the [Responses API](/docs/api-reference/responses), web search has the same tiered rate limits as the models above.
*   [Refer to this guide](/docs/guides/your-data) for data handling, residency, and retention information.

Was this page useful?
File search
===========

Allow models to search your files for relevant information before generating a response.

Overview
--------

File search is a tool available in the [Responses API](/docs/api-reference/responses). It enables models to retrieve information in a knowledge base of previously uploaded files through semantic and keyword search. By creating vector stores and uploading files to them, you can augment the models' inherent knowledge by giving them access to these knowledge bases or `vector_stores`.

To learn more about how vector stores and semantic search work, refer to our [retrieval guide](/docs/guides/retrieval).

This is a hosted tool managed by OpenAI, meaning you don't have to implement code on your end to handle its execution. When the model decides to use it, it will automatically call the tool, retrieve information from your files, and return an output.

How to use
----------

Prior to using file search with the Responses API, you need to have set up a knowledge base in a vector store and uploaded files to it.

Create a vector store and upload a file

Follow these steps to create a vector store and upload a file to it. You can use [this example file](https://cdn.openai.com/API/docs/deep_research_blog.pdf) or upload your own.

#### Upload the file to the File API

Upload a file

```python
import requests
from io import BytesIO
from openai import OpenAI

client = OpenAI()

def create_file(client, file_path):
    if file_path.startswith("http://") or file_path.startswith("https://"):
        # Download the file content from the URL
        response = requests.get(file_path)
        file_content = BytesIO(response.content)
        file_name = file_path.split("/")[-1]
        file_tuple = (file_name, file_content)
        result = client.files.create(
            file=file_tuple,
            purpose="assistants"
        )
    else:
        # Handle local file path
        with open(file_path, "rb") as file_content:
            result = client.files.create(
                file=file_content,
                purpose="assistants"
            )
    print(result.id)
    return result.id

# Replace with your own file path or URL
file_id = create_file(client, "https://cdn.openai.com/API/docs/deep_research_blog.pdf")
```

```javascript
import fs from "fs";
import OpenAI from "openai";
const openai = new OpenAI();

async function createFile(filePath) {
  let result;
  if (filePath.startsWith("http://") || filePath.startsWith("https://")) {
    // Download the file content from the URL
    const res = await fetch(filePath);
    const buffer = await res.arrayBuffer();
    const urlParts = filePath.split("/");
    const fileName = urlParts[urlParts.length - 1];
    const file = new File([buffer], fileName);
    result = await openai.files.create({
      file: file,
      purpose: "assistants",
    });
  } else {
    // Handle local file path
    const fileContent = fs.createReadStream(filePath);
    result = await openai.files.create({
      file: fileContent,
      purpose: "assistants",
    });
  }
  return result.id;
}

// Replace with your own file path or URL
const fileId = await createFile(
  "https://cdn.openai.com/API/docs/deep_research_blog.pdf"
);

console.log(fileId);
```

#### Create a vector store

Create a vector store

```python
vector_store = client.vector_stores.create(
    name="knowledge_base"
)
print(vector_store.id)
```

```javascript
const vectorStore = await openai.vectorStores.create({
    name: "knowledge_base",
});
console.log(vectorStore.id);
```

#### Add the file to the vector store

Add a file to a vector store

```python
client.vector_stores.files.create(
    vector_store_id=vector_store.id,
    file_id=file_id
)
print(result)
```

```javascript
await openai.vectorStores.files.create(
    vectorStore.id,
    {
        file_id: fileId,
    }
});
```

#### Check status

Run this code until the file is ready to be used (i.e., when the status is `completed`).

Check status

```python
result = client.vector_stores.files.list(
    vector_store_id=vector_store.id
)
print(result)
```

```javascript
const result = await openai.vectorStores.files.list({
    vector_store_id: vectorStore.id,
});
console.log(result);
```

Once your knowledge base is set up, you can include the `file_search` tool in the list of tools available to the model, along with the list of vector stores in which to search.

At the moment, you can search in only one vector store at a time, so you can include only one vector store ID when calling the file search tool.

File search tool

```python
from openai import OpenAI
client = OpenAI()

response = client.responses.create(
    model="gpt-4o-mini",
    input="What is deep research by OpenAI?",
    tools=[{
        "type": "file_search",
        "vector_store_ids": ["<vector_store_id>"]
    }]
)
print(response)
```

```javascript
import OpenAI from "openai";
const openai = new OpenAI();

const response = await openai.responses.create({
    model: "gpt-4o-mini",
    input: "What is deep research by OpenAI?",
    tools: [{
        type: "file_search",
        vector_store_ids: ["<vector_store_id>"],
    }],
});
console.log(response);
```

When this tool is called by the model, you will receive a response with multiple outputs:

1.  A `file_search_call` output item, which contains the id of the file search call.
2.  A `message` output item, which contains the response from the model, along with the file citations.

File search response

```json
{
  "output": [
    {
      "type": "file_search_call",
      "id": "fs_67c09ccea8c48191ade9367e3ba71515",
      "status": "completed",
      "queries": ["What is deep research?"],
      "search_results": null
    },
    {
      "id": "msg_67c09cd3091c819185af2be5d13d87de",
      "type": "message",
      "role": "assistant",
      "content": [
        {
          "type": "output_text",
          "text": "Deep research is a sophisticated capability that allows for extensive inquiry and synthesis of information across various domains. It is designed to conduct multi-step research tasks, gather data from multiple online sources, and provide comprehensive reports similar to what a research analyst would produce. This functionality is particularly useful in fields requiring detailed and accurate information...",
          "annotations": [
            {
              "type": "file_citation",
              "index": 992,
              "file_id": "file-2dtbBZdjtDKS8eqWxqbgDi",
              "filename": "deep_research_blog.pdf"
            },
            {
              "type": "file_citation",
              "index": 992,
              "file_id": "file-2dtbBZdjtDKS8eqWxqbgDi",
              "filename": "deep_research_blog.pdf"
            },
            {
              "type": "file_citation",
              "index": 1176,
              "file_id": "file-2dtbBZdjtDKS8eqWxqbgDi",
              "filename": "deep_research_blog.pdf"
            },
            {
              "type": "file_citation",
              "index": 1176,
              "file_id": "file-2dtbBZdjtDKS8eqWxqbgDi",
              "filename": "deep_research_blog.pdf"
            }
          ]
        }
      ]
    }
  ]
}
```

Retrieval customization
-----------------------

### Limiting the number of results

Using the file search tool with the Responses API, you can customize the number of results you want to retrieve from the vector stores. This can help reduce both token usage and latency, but may come at the cost of reduced answer quality.

Limit the number of results

```python
response = client.responses.create(
    model="gpt-4o-mini",
    input="What is deep research by OpenAI?",
    tools=[{
        "type": "file_search",
        "vector_store_ids": ["<vector_store_id>"],
        "max_num_results": 2
    }]
)
print(response)
```

```javascript
const response = await openai.responses.create({
    model: "gpt-4o-mini",
    input: "What is deep research by OpenAI?",
    tools: [{
        type: "file_search",
        vector_store_ids: ["<vector_store_id>"],
        max_num_results: 2,
    }],
});
console.log(response);
```

### Include search results in the response

While you can see annotations (references to files) in the output text, the file search call will not return search results by default.

To include search results in the response, you can use the `include` parameter when creating the response.

Include search results

```python
response = client.responses.create(
    model="gpt-4o-mini",
    input="What is deep research by OpenAI?",
    tools=[{
        "type": "file_search",
        "vector_store_ids": ["<vector_store_id>"]
    }],
    include=["file_search_call.results"]
)
print(response)
```

```javascript
const response = await openai.responses.create({
    model: "gpt-4o-mini",
    input: "What is deep research by OpenAI?",
    tools: [{
        type: "file_search",
        vector_store_ids: ["<vector_store_id>"],
    }],
    include: ["file_search_call.results"],
});
console.log(response);
```

### Metadata filtering

You can filter the search results based on the metadata of the files. For more details, refer to our [retrieval guide](/docs/guides/retrieval), which covers:

*   How to [set attributes on vector store files](/docs/guides/retrieval#attributes)
*   How to [define filters](/docs/guides/retrieval#attribute-filtering)

Metadata filtering

```python
response = client.responses.create(
    model="gpt-4o-mini",
    input="What is deep research by OpenAI?",
    tools=[{
        "type": "file_search",
        "vector_store_ids": ["<vector_store_id>"],
        "filters": {
            "type": "eq",
            "key": "type",
            "value": "blog"
        }
    }]
)
print(response)
```

```javascript
const response = await openai.responses.create({
    model: "gpt-4o-mini",
    input: "What is deep research by OpenAI?",
    tools: [{
        type: "file_search",
        vector_store_ids: ["<vector_store_id>"],
        filters: {
            type: "eq",
            key: "type",
            value: "blog"
        }
    }]
});
console.log(response);
```

Supported files
---------------

_For `text/` MIME types, the encoding must be one of `utf-8`, `utf-16`, or `ascii`._

|File format|MIME type|
|---|---|
|.c|text/x-c|
|.cpp|text/x-c++|
|.cs|text/x-csharp|
|.css|text/css|
|.doc|application/msword|
|.docx|application/vnd.openxmlformats-officedocument.wordprocessingml.document|
|.go|text/x-golang|
|.html|text/html|
|.java|text/x-java|
|.js|text/javascript|
|.json|application/json|
|.md|text/markdown|
|.pdf|application/pdf|
|.php|text/x-php|
|.pptx|application/vnd.openxmlformats-officedocument.presentationml.presentation|
|.py|text/x-python|
|.py|text/x-script.python|
|.rb|text/x-ruby|
|.sh|application/x-sh|
|.tex|text/x-tex|
|.ts|application/typescript|
|.txt|text/plain|

Limitations
-----------

Below are some usage limitations on file search that implementors should be aware of.

*   Projects are limited to a total size of 100GB for all Files
*   Vector stores are limited to a total of 10k files
*   Individual files can be a max of 512MB (roughly 5M tokens per file)

Was this page useful?
Computer use
============

Build a computer-using agent that can perform tasks on your behalf.

Overview
--------

**Computer use** is a practical application of our [Computer-Using Agent](https://openai.com/index/computer-using-agent/) (CUA) model, `computer-use-preview`, which combines the vision capabilities of [GPT-4o](/docs/models/gpt-4o) with advanced reasoning to simulate controlling computer interfaces and performing tasks.

Computer use is available through the [Responses API](/docs/guides/responses-vs-chat-completions). It is not available on Chat Completions.

Computer use is in beta. Because the model is still in preview and may be susceptible to exploits and inadvertent mistakes, we discourage trusting it in fully authenticated environments or for high-stakes tasks. See [limitations](#limitations) and [risk and safety best practices](#risks-and-safety) below. You must use the Computer Use tool in line with OpenAI's [Usage Policy](https://openai.com/policies/usage-policies/) and [Business Terms](https://openai.com/policies/business-terms/).

How it works
------------

The computer use tool operates in a continuous loop. It sends computer actions, like `click(x,y)` or `type(text)`, which your code executes on a computer or browser environment and then returns screenshots of the outcomes back to the model.

In this way, your code simulates the actions of a human using a computer interface, while our model uses the screenshots to understand the state of the environment and suggest next actions.

This loop lets you automate many tasks requiring clicking, typing, scrolling, and more. For example, booking a flight, searching for a product, or filling out a form.

Refer to the [integration section](#integration) below for more details on how to integrate the computer use tool, or check out our sample app repository to set up an environment and try example integrations.

[

CUA sample app

Examples of how to integrate the computer use tool in different environments

](https://github.com/openai/openai-cua-sample-app)

Setting up your environment
---------------------------

Before integrating the tool, prepare an environment that can capture screenshots and execute the recommended actions. We recommend using a sandboxed environment for safety reasons.

In this guide, we'll show you examples using either a local browsing environment or a local virtual machine, but there are more example computer environments in our sample app.

Set up a local browsing environment

If you want to try out the computer use tool with minimal setup, you can use a browser automation framework such as [Playwright](https://playwright.dev/) or [Selenium](https://www.selenium.dev/).

Running a browser automation framework locally can pose security risks. We recommend the following setup to mitigate them:

*   Use a sandboxed environment
*   Set `env` to an empty object to avoid exposing host environment variables to the browser
*   Set flags to disable extensions and the file system

#### Start a browser instance

You can start browser instances using your preferred language by installing the corresponding SDK.

For example, to start a Playwright browser instance, install the Playwright SDK:

*   Python: `pip install playwright`
*   JavaScript: `npm i playwright` then `npx playwright install`

Then run the following code:

Start a browser instance

```javascript
import { chromium } from "playwright";

const browser = await chromium.launch({
  headless: false,
  chromiumSandbox: true,
  env: {},
  args: ["--disable-extensions", "--disable-file-system"],
});
const page = await browser.newPage();
await page.setViewportSize({ width: 1024, height: 768 });
await page.goto("https://bing.com");

await page.waitForTimeout(10000);

browser.close();
```

```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch(
        headless=False,
        chromium_sandbox=True,
        env={},
        args=[
            "--disable-extensions",
            "--disable-file-system"
        ]
    )
    page = browser.new_page()
    page.set_viewport_size({"width": 1024, "height": 768})
    page.goto("https://bing.com")

    page.wait_for_timeout(10000)
```

Set up a local virtual machine

If you'd like to use the computer use tool beyond just a browser interface, you can set up a local virtual machine instead, using a tool like [Docker](https://www.docker.com/). You can then connect to this local machine to execute computer use actions.

#### Start Docker

If you don't have Docker installed, you can install it from [their website](https://www.docker.com). Once installed, make sure Docker is running on your machine.

#### Create a Dockerfile

Create a Dockerfile to define the configuration of your virtual machine.

Here is an example Dockerfile that starts an Ubuntu virtual machine with a VNC server:

Dockerfile

```json
FROM ubuntu:22.04
ENV DEBIAN_FRONTEND=noninteractive

# 1) Install Xfce, x11vnc, Xvfb, xdotool, etc., but remove any screen lockers or power managers
RUN apt-get update && apt-get install -y     xfce4     xfce4-goodies     x11vnc     xvfb     xdotool     imagemagick     x11-apps     sudo     software-properties-common     imagemagick  && apt-get remove -y light-locker xfce4-screensaver xfce4-power-manager || true  && apt-get clean && rm -rf /var/lib/apt/lists/*

# 2) Add the mozillateam PPA and install Firefox ESR
RUN add-apt-repository ppa:mozillateam/ppa  && apt-get update  && apt-get install -y --no-install-recommends firefox-esr  && update-alternatives --set x-www-browser /usr/bin/firefox-esr  && apt-get clean && rm -rf /var/lib/apt/lists/*

# 3) Create non-root user
RUN useradd -ms /bin/bash myuser     && echo "myuser ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
USER myuser
WORKDIR /home/myuser

# 4) Set x11vnc password ("secret")
RUN x11vnc -storepasswd secret /home/myuser/.vncpass

# 5) Expose port 5900 and run Xvfb, x11vnc, Xfce (no login manager)
EXPOSE 5900
CMD ["/bin/sh", "-c", "    Xvfb :99 -screen 0 1280x800x24 >/dev/null 2>&1 &     x11vnc -display :99 -forever -rfbauth /home/myuser/.vncpass -listen 0.0.0.0 -rfbport 5900 >/dev/null 2>&1 &     export DISPLAY=:99 &&     startxfce4 >/dev/null 2>&1 &     sleep 2 && echo 'Container running!' &&     tail -f /dev/null "]
```

#### Build the Docker image

Build the Docker image by running the following command in the directory containing the Dockerfile:

```bash
docker build -t cua-image .
```

#### Run the Docker container locally

Start the Docker container with the following command:

```bash
docker run --rm -it --name cua-image -p 5900:5900 -e DISPLAY=:99 cua-image
```

#### Execute commands on the container

Now that your container is running, you can execute commands on it. For example, we can define a helper function to execute commands on the container that will be used in the next steps.

Execute commands on the container

```python
def docker_exec(cmd: str, container_name: str, decode=True) -> str:
    safe_cmd = cmd.replace('"', '\"')
    docker_cmd = f'docker exec {container_name} sh -c "{safe_cmd}"'
    output = subprocess.check_output(docker_cmd, shell=True)
    if decode:
        return output.decode("utf-8", errors="ignore")
    return output

class VM:
    def __init__(self, display, container_name):
        self.display = display
        self.container_name = container_name

vm = VM(display=":99", container_name="cua-image")
```

```javascript
async function dockerExec(cmd, containerName, decode = true) {
  const safeCmd = cmd.replace(/"/g, '\"');
  const dockerCmd = `docker exec ${containerName} sh -c "${safeCmd}"`;
  const output = await execAsync(dockerCmd, {
    encoding: decode ? "utf8" : "buffer",
  });
  const result = output && output.stdout ? output.stdout : output;
  if (decode) {
    return result.toString("utf-8");
  }
  return result;
}

const vm = {
    display: ":99",
    containerName: "cua-image",
};
```

Integrating the CUA loop
------------------------

These are the high-level steps you need to follow to integrate the computer use tool in your application:

1.  **Send a request to the model**: Include the `computer` tool as part of the available tools, specifying the display size and environment. You can also include in the first request a screenshot of the initial state of the environment.
    
2.  **Receive a response from the model**: Check if the response has any `computer_call` items. This tool call contains a suggested action to take to progress towards the specified goal. These actions could be clicking at a given position, typing in text, scrolling, or even waiting.
    
3.  **Execute the requested action**: Execute through code the corresponding action on your computer or browser environment.
    
4.  **Capture the updated state**: After executing the action, capture the updated state of the environment as a screenshot.
    
5.  **Repeat**: Send a new request with the updated state as a `computer_call_output`, and repeat this loop until the model stops requesting actions or you decide to stop.
    

![Computer use diagram](https://cdn.openai.com/API/docs/images/cua_diagram.png)

### 1\. Send a request to the model

Send a request to create a Response with the `computer-use-preview` model equipped with the `computer_use_preview` tool. This request should include details about your environment, along with an initial input prompt.

If you want to show a summary of the reasoning performed by the model, you can include the `generate_summary` parameter in the request. This can be helpful if you want to debug or show what's happening behind the scenes in your interface. The summary can either be `concise` or `detailed`.

Optionally, you can include a screenshot of the initial state of the environment.

To be able to use the `computer_use_preview` tool, you need to set the `truncation` parameter to `"auto"` (by default, truncation is disabled).

Send a CUA request

```javascript
import OpenAI from "openai";
const openai = new OpenAI();

const response = await openai.responses.create({
  model: "computer-use-preview",
  tools: [
    {
      type: "computer_use_preview",
      display_width: 1024,
      display_height: 768,
      environment: "browser", // other possible values: "mac", "windows", "ubuntu"
    },
  ],
  input: [
    {
      role: "user",
      content: "Check the latest OpenAI news on bing.com.",
    },
    // Optional: include a screenshot of the initial state of the environment
    // {
    //     type: "input_image",
    //     image_url: `data:image/png;base64,${screenshot_base64}`
    // }
  ],
  reasoning: {
    generate_summary: "concise",
  },
  truncation: "auto",
});

console.log(JSON.stringify(response.output, null, 2));
```

```python
from openai import OpenAI
client = OpenAI()

response = client.responses.create(
    model="computer-use-preview",
    tools=[{
        "type": "computer_use_preview",
        "display_width": 1024,
        "display_height": 768,
        "environment": "browser" # other possible values: "mac", "windows", "ubuntu"
    }],
    input=[
        {
            "role": "user",
            "content": "Check the latest OpenAI news on bing.com."
        }
        # Optional: include a screenshot of the initial state of the environment
        # {
        #     type: "input_image",
        #     image_url: f"data:image/png;base64,{screenshot_base64}"
        # }
    ],
    reasoning={
        "generate_summary": "concise",
    },
    truncation="auto"
)

print(response.output)
```

### 2\. Receive a suggested action

The model returns an output that contains either a `computer_call` item, just text, or other tool calls, depending on the state of the conversation.

Examples of `computer_call` items are a click, a scroll, a key press, or any other event defined in the [API reference](/docs/api-reference/computer-use). In our example, the item is a click action:

CUA suggested action

```json
"output": [
    {
        "type": "reasoning",
        "id": "rs_67cc...",
        "summary": [
            {
                "type": "summary_text",
                "text": "Clicking on the browser address bar."
            }
        ]
    },
    {
        "type": "computer_call",
        "id": "cu_67cc...",
        "call_id": "call_zw3...",
        "action": {
            "type": "click",
            "button": "left",
            "x": 156,
            "y": 50
        },
        "pending_safety_checks": [],
        "status": "completed"
    }
]
```

#### Reasoning items

The model may return a `reasoning` item in the response output for some actions. If you don't use the `previous_response_id` parameter as shown in [Step 5](#5-repeat) and manage the inputs array on your end, make sure to include those reasoning items along with the computer calls when sending the next request to the CUA model–or the request will fail.

The reasoning items are only compatible with the same model that produced them (in this case, `computer-use-preview`). If you implement a flow where you use several models with the same conversation history, you should filter these reasoning items out of the inputs array you send to other models.

#### Safety checks

The model may return safety checks with the `pending_safety_check` parameter. Refer to the section on how to [acknowledge safety checks](#acknowledge-safety-checks) below for more details.

### 3\. Execute the action in your environment

Execute the corresponding actions on your computer or browser. How you map a computer call to actions through code depends on your environment. This code shows example implementations for the most common computer actions.

Playwright

Execute the action

```javascript
async function handleModelAction(page, action) {
  // Given a computer action (e.g., click, double_click, scroll, etc.),
  // execute the corresponding operation on the Playwright page.

  const actionType = action.type;

  try {
    switch (actionType) {
      case "click": {
        const { x, y, button = "left" } = action;
        console.log(`Action: click at (${x}, ${y}) with button '${button}'`);
        await page.mouse.click(x, y, { button });
        break;
      }

      case "scroll": {
        const { x, y, scrollX, scrollY } = action;
        console.log(
          `Action: scroll at (${x}, ${y}) with offsets (scrollX=${scrollX}, scrollY=${scrollY})`
        );
        await page.mouse.move(x, y);
        await page.evaluate(`window.scrollBy(${scrollX}, ${scrollY})`);
        break;
      }

      case "keypress": {
        const { keys } = action;
        for (const k of keys) {
          console.log(`Action: keypress '${k}'`);
          // A simple mapping for common keys; expand as needed.
          if (k.includes("ENTER")) {
            await page.keyboard.press("Enter");
          } else if (k.includes("SPACE")) {
            await page.keyboard.press(" ");
          } else {
            await page.keyboard.press(k);
          }
        }
        break;
      }

      case "type": {
        const { text } = action;
        console.log(`Action: type text '${text}'`);
        await page.keyboard.type(text);
        break;
      }

      case "wait": {
        console.log(`Action: wait`);
        await page.waitForTimeout(2000);
        break;
      }

      case "screenshot": {
        // Nothing to do as screenshot is taken at each turn
        console.log(`Action: screenshot`);
        break;
      }

      // Handle other actions here

      default:
        console.log("Unrecognized action:", action);
    }
  } catch (e) {
    console.error("Error handling action", action, ":", e);
  }
}
```

```python
def handle_model_action(page, action):
    """
    Given a computer action (e.g., click, double_click, scroll, etc.),
    execute the corresponding operation on the Playwright page.
    """
    action_type = action.type
    
    try:
        match action_type:

            case "click":
                x, y = action.x, action.y
                button = action.button
                print(f"Action: click at ({x}, {y}) with button '{button}'")
                # Not handling things like middle click, etc.
                if button != "left" and button != "right":
                    button = "left"
                page.mouse.click(x, y, button=button)

            case "scroll":
                x, y = action.x, action.y
                scroll_x, scroll_y = action.scroll_x, action.scroll_y
                print(f"Action: scroll at ({x}, {y}) with offsets (scroll_x={scroll_x}, scroll_y={scroll_y})")
                page.mouse.move(x, y)
                page.evaluate(f"window.scrollBy({scroll_x}, {scroll_y})")

            case "keypress":
                keys = action.keys
                for k in keys:
                    print(f"Action: keypress '{k}'")
                    # A simple mapping for common keys; expand as needed.
                    if k.lower() == "enter":
                        page.keyboard.press("Enter")
                    elif k.lower() == "space":
                        page.keyboard.press(" ")
                    else:
                        page.keyboard.press(k)
            
            case "type":
                text = action.text
                print(f"Action: type text: {text}")
                page.keyboard.type(text)
            
            case "wait":
                print(f"Action: wait")
                time.sleep(2)

            case "screenshot":
                # Nothing to do as screenshot is taken at each turn
                print(f"Action: screenshot")

            # Handle other actions here

            case _:
                print(f"Unrecognized action: {action}")

    except Exception as e:
        print(f"Error handling action {action}: {e}")
```

Docker

Execute the action

```javascript
async function handleModelAction(vm, action) {
    // Given a computer action (e.g., click, double_click, scroll, etc.),
    // execute the corresponding operation on the Docker environment.
  
    const actionType = action.type;
  
    try {
      switch (actionType) {
        case "click": {
          const { x, y, button = "left" } = action;
          const buttonMap = { left: 1, middle: 2, right: 3 };
          const b = buttonMap[button] || 1;
          console.log(`Action: click at (${x}, ${y}) with button '${button}'`);
          await dockerExec(
            `DISPLAY=${vm.display} xdotool mousemove ${x} ${y} click ${b}`,
            vm.containerName
          );
          break;
        }
  
        case "scroll": {
          const { x, y, scrollX, scrollY } = action;
          console.log(
            `Action: scroll at (${x}, ${y}) with offsets (scrollX=${scrollX}, scrollY=${scrollY})`
          );
          await dockerExec(
            `DISPLAY=${vm.display} xdotool mousemove ${x} ${y}`,
            vm.containerName
          );
          // For vertical scrolling, use button 4 for scroll up and button 5 for scroll down.
          if (scrollY !== 0) {
            const button = scrollY < 0 ? 4 : 5;
            const clicks = Math.abs(scrollY);
            for (let i = 0; i < clicks; i++) {
              await dockerExec(
                `DISPLAY=${vm.display} xdotool click ${button}`,
                vm.containerName
              );
            }
          }
          break;
        }
  
        case "keypress": {
          const { keys } = action;
          for (const k of keys) {
            console.log(`Action: keypress '${k}'`);
            // A simple mapping for common keys; expand as needed.
            if (k.includes("ENTER")) {
              await dockerExec(
                `DISPLAY=${vm.display} xdotool key 'Return'`,
                vm.containerName
              );
            } else if (k.includes("SPACE")) {
              await dockerExec(
                `DISPLAY=${vm.display} xdotool key 'space'`,
                vm.containerName
              );
            } else {
              await dockerExec(
                `DISPLAY=${vm.display} xdotool key '${k}'`,
                vm.containerName
              );
            }
          }
          break;
        }
  
        case "type": {
          const { text } = action;
          console.log(`Action: type text '${text}'`);
          await dockerExec(
            `DISPLAY=${vm.display} xdotool type '${text}'`,
            vm.containerName
          );
          break;
        }
  
        case "wait": {
          console.log(`Action: wait`);
          await new Promise((resolve) => setTimeout(resolve, 2000));
          break;
        }
  
        case "screenshot": {
          // Nothing to do as screenshot is taken at each turn
          console.log(`Action: screenshot`);
          break;
        }
  
        // Handle other actions here
  
        default:
          console.log("Unrecognized action:", action);
      }
    } catch (e) {
      console.error("Error handling action", action, ":", e);
    }
  }
```

```python
def handle_model_action(vm, action):
    """
    Given a computer action (e.g., click, double_click, scroll, etc.),
    execute the corresponding operation on the Docker environment.
    """
    action_type = action.type

    try:
        match action_type:
            
            case "click":
                x, y = int(action.x), int(action.y)
                button_map = {"left": 1, "middle": 2, "right": 3}
                b = button_map.get(action.button, 1)
                print(f"Action: click at ({x}, {y}) with button '{action.button}'")
                docker_exec(f"DISPLAY={vm.display} xdotool mousemove {x} {y} click {b}", vm.container_name)

            case "scroll":
                x, y = int(action.x), int(action.y)
                scroll_x, scroll_y = int(action.scroll_x), int(action.scroll_y)
                print(f"Action: scroll at ({x}, {y}) with offsets (scroll_x={scroll_x}, scroll_y={scroll_y})")
                docker_exec(f"DISPLAY={vm.display} xdotool mousemove {x} {y}", vm.container_name)
                
                # For vertical scrolling, use button 4 (scroll up) or button 5 (scroll down)
                if scroll_y != 0:
                    button = 4 if scroll_y < 0 else 5
                    clicks = abs(scroll_y)
                    for _ in range(clicks):
                        docker_exec(f"DISPLAY={vm.display} xdotool click {button}", vm.container_name)
            
            case "keypress":
                keys = action.keys
                for k in keys:
                    print(f"Action: keypress '{k}'")
                    # A simple mapping for common keys; expand as needed.
                    if k.lower() == "enter":
                        docker_exec(f"DISPLAY={vm.display} xdotool key 'Return'", vm.container_name)
                    elif k.lower() == "space":
                        docker_exec(f"DISPLAY={vm.display} xdotool key 'space'", vm.container_name)
                    else:
                        docker_exec(f"DISPLAY={vm.display} xdotool key '{k}'", vm.container_name)
            
            case "type":
                text = action.text
                print(f"Action: type text: {text}")
                docker_exec(f"DISPLAY={vm.display} xdotool type '{text}'", vm.container_name)
            
            case "wait":
                print(f"Action: wait")
                time.sleep(2)

            case "screenshot":
                # Nothing to do as screenshot is taken at each turn
                print(f"Action: screenshot")
            
            # Handle other actions here

            case _:
                print(f"Unrecognized action: {action}")

    except Exception as e:
        print(f"Error handling action {action}: {e}")
```

### 4\. Capture the updated screenshot

After executing the action, capture the updated state of the environment as a screenshot, which also differs depending on your environment.

Playwright

Capture and send the updated screenshot

```javascript
async function getScreenshot(page) {
    // Take a full-page screenshot using Playwright and return the image bytes.
    return await page.screenshot();
}
```

```python
def get_screenshot(page):
    """
    Take a full-page screenshot using Playwright and return the image bytes.
    """
    return page.screenshot()
```

Docker

Capture and send the updated screenshot

```javascript
async function getScreenshot(vm) {
  // Take a screenshot, returning raw bytes.
  const cmd = `export DISPLAY=${vm.display} && import -window root png:-`;
  const screenshotBuffer = await dockerExec(cmd, vm.containerName, false);
  return screenshotBuffer;
}
```

```python
def get_screenshot(vm):
    """
    Takes a screenshot, returning raw bytes.
    """
    cmd = (
        f"export DISPLAY={vm.display} && "
        "import -window root png:-"
    )
    screenshot_bytes = docker_exec(cmd, vm.container_name, decode=False)
    return screenshot_bytes
```

### 5\. Repeat

Once you have the screenshot, you can send it back to the model as a `computer_call_output` to get the next action. Repeat these steps as long as you get a `computer_call` item in the response.

Repeat steps in a loop

```javascript
import OpenAI from "openai";
const openai = new OpenAI();

async function computerUseLoop(instance, response) {
  /**
   * Run the loop that executes computer actions until no 'computer_call' is found.
   */
  while (true) {
    const computerCalls = response.output.filter(
      (item) => item.type === "computer_call"
    );
    if (computerCalls.length === 0) {
      console.log("No computer call found. Output from model:");
      response.output.forEach((item) => {
        console.log(JSON.stringify(item, null, 2));
      });
      break; // Exit when no computer calls are issued.
    }

    // We expect at most one computer call per response.
    const computerCall = computerCalls[0];
    const lastCallId = computerCall.call_id;
    const action = computerCall.action;

    // Execute the action (function defined in step 3)
    handleModelAction(instance, action);
    await new Promise((resolve) => setTimeout(resolve, 1000)); // Allow time for changes to take effect.

    // Take a screenshot after the action (function defined in step 4)
    const screenshotBytes = await getScreenshot(instance);
    const screenshotBase64 = Buffer.from(screenshotBytes).toString("base64");

    // Send the screenshot back as a computer_call_output
    response = await openai.responses.create({
      model: "computer-use-preview",
      previous_response_id: response.id,
      tools: [
        {
          type: "computer_use_preview",
          display_width: 1024,
          display_height: 768,
          environment: "browser",
        },
      ],
      input: [
        {
          call_id: lastCallId,
          type: "computer_call_output",
          output: {
            type: "input_image",
            image_url: `data:image/png;base64,${screenshotBase64}`,
          },
        },
      ],
      truncation: "auto",
    });
  }

  return response;
}
```

```python
import time
import base64
from openai import OpenAI
client = OpenAI()

def computer_use_loop(instance, response):
    """
    Run the loop that executes computer actions until no 'computer_call' is found.
    """
    while True:
        computer_calls = [item for item in response.output if item.type == "computer_call"]
        if not computer_calls:
            print("No computer call found. Output from model:")
            for item in response.output:
                print(item)
            break  # Exit when no computer calls are issued.

        # We expect at most one computer call per response.
        computer_call = computer_calls[0]
        last_call_id = computer_call.call_id
        action = computer_call.action

        # Execute the action (function defined in step 3)
        handle_model_action(instance, action)
        time.sleep(1)  # Allow time for changes to take effect.

        # Take a screenshot after the action (function defined in step 4)
        screenshot_bytes = get_screenshot(instance)
        screenshot_base64 = base64.b64encode(screenshot_bytes).decode("utf-8")

        # Send the screenshot back as a computer_call_output
        response = client.responses.create(
            model="computer-use-preview",
            previous_response_id=response.id,
            tools=[
                {
                    "type": "computer_use_preview",
                    "display_width": 1024,
                    "display_height": 768,
                    "environment": "browser"
                }
            ],
            input=[
                {
                    "call_id": last_call_id,
                    "type": "computer_call_output",
                    "output": {
                        "type": "input_image",
                        "image_url": f"data:image/png;base64,{screenshot_base64}"
                    }
                }
            ],
            truncation="auto"
        )

    return response
```

#### Handling conversation history

You can use the `previous_response_id` parameter to link the current request to the previous response. We recommend using this method if you don't want to manage the conversation history on your side.

If you do not want to use this parameter, you should make sure to include in your inputs array all the items returned in the response output of the previous request, including reasoning items if present.

### Acknowledge safety checks

We have implemented safety checks in the API to help protect against prompt injection and model mistakes. These checks include:

*   Malicious instruction detection: we evaluate the screenshot image and check if it contains adversarial content that may change the model's behavior.
*   Irrelevant domain detection: we evaluate the `current_url` (if provided) and check if the current domain is considered relevant given the conversation history.
*   Sensitive domain detection: we check the `current_url` (if provided) and raise a warning when we detect the user is on a sensitive domain.

If one or multiple of the above checks is triggered, a safety check is raised when the model returns the next `computer_call`, with the `pending_safety_checks` parameter.

Pending safety checks

```json
"output": [
    {
        "type": "reasoning",
        "id": "rs_67cb...",
        "summary": [
            {
                "type": "summary_text",
                "text": "Exploring 'File' menu option."
            }
        ]
    },
    {
        "type": "computer_call",
        "id": "cu_67cb...",
        "call_id": "call_nEJ...",
        "action": {
            "type": "click",
            "button": "left",
            "x": 135,
            "y": 193
        },
        "pending_safety_checks": [
            {
                "id": "cu_sc_67cb...",
                "code": "malicious_instructions",
                "message": "We've detected instructions that may cause your application to perform malicious or unauthorized actions. Please acknowledge this warning if you'd like to proceed."
            }
        ],
        "status": "completed"
    }
]
```

You need to pass the safety checks back as `acknowledged_safety_checks` in the next request in order to proceed. In all cases where `pending_safety_checks` are returned, actions should be handed over to the end user to confirm model behavior and accuracy.

*   `malicious_instructions` and `irrelevant_domain`: end users should review model actions and confirm that the model is behaving as intended.
*   `sensitive_domain`: ensure an end user is actively monitoring the model actions on these sites. Exact implementation of this "watch mode" may vary by application, but a potential example could be collecting user impression data on the site to make sure there is active end user engagement with the application.

Acknowledge safety checks

```python
from openai import OpenAI
client = OpenAI()

response = client.responses.create(
    model="computer-use-preview",
    previous_response_id="<previous_response_id>",
    tools=[{
        "type": "computer_use_preview",
        "display_width": 1024,
        "display_height": 768,
        "environment": "browser"
    }],
    input=[
        {
            "type": "computer_call_output",
            "call_id": "<call_id>",
            "acknowledged_safety_checks": [
                {
                    "id": "<safety_check_id>",
                    "code": "malicious_instructions",
                    "message": "We've detected instructions that may cause your application to perform malicious or unauthorized actions. Please acknowledge this warning if you'd like to proceed."
                }
            ],
            "output": {
                "type": "computer_screenshot",
                "image_url": "<image_url>"
            }
        }
    ],
    truncation="auto"
)
```

```javascript
import OpenAI from "openai";
const openai = new OpenAI();

const response = await openai.responses.create({
    model: "computer-use-preview",
    previous_response_id: "<previous_response_id>",
    tools: [{
        type: "computer_use_preview",
        display_width: 1024,
        display_height: 768,
        environment: "browser"
    }],
    input: [
        {
            "type": "computer_call_output",
            "call_id": "<call_id>",
            "acknowledged_safety_checks": [
                {
                    "id": "<safety_check_id>",
                    "code": "malicious_instructions",
                    "message": "We've detected instructions that may cause your application to perform malicious or unauthorized actions. Please acknowledge this warning if you'd like to proceed."
                }
            ],
            "output": {
                "type": "computer_screenshot",
                "image_url": "<image_url>"
            }
        }
    ],
    truncation: "auto",
});
```

### Final code

Putting it all together, the final code should include:

1.  The initialization of the environment
2.  A first request to the model with the `computer` tool
3.  A loop that executes the suggested action in your environment
4.  A way to acknowledge safety checks and give end users a chance to confirm actions

To see end-to-end example integrations, refer to our CUA sample app repository.

[

CUA sample app

Examples of how to integrate the computer use tool in different environments

](https://github.com/openai/openai-cua-sample-app)

Limitations
-----------

We recommend using the `computer-use-preview` model for browser-based tasks. The model may be susceptible to inadvertent model mistakes, especially in non-browser environments that it is less used to.

For example, `computer-use-preview`'s performance on OSWorld is currently 38.1%, indicating that the model is not yet highly reliable for automating tasks on an OS. More details about the model and related safety work can be found in our updated [system card](https://openai.com/index/operator-system-card/).

Some other behavior limitations to be aware of:

*   The [`computer-use-preview` model](/docs/models/computer-use-preview) has constrained rate limits and feature support, described on its model detail page.
*   [Refer to this guide](/docs/guides/your-data) for data retention, residency, and handling policies.

Risks and safety
----------------

Computer use presents unique risks that differ from those in standard API features or chat interfaces, especially when interacting with the internet.

There are a number of best practices listed below that you should follow to mitigate these risks.

#### Human in the loop for high-stakes tasks

Avoid tasks that are high-stakes or require high levels of accuracy. The model may make mistakes that are challenging to reverse. As mentioned above, the model is still prone to mistakes, especially on non-browser surfaces. While we expect the model to request user confirmation before proceeding with certain higher-impact decisions, this is not fully reliable. Ensure a human is in the loop to confirm model actions with real-world consequences.

#### Beware of prompt injections

A prompt injection occurs when an AI model mistakenly follows untrusted instructions appearing in its input. For the `computer-use-preview` model, this may manifest as it seeing something in the provided screenshot, like a malicious website or email, that instructs it to do something that the user does not want, and it complies. To avoid prompt injection risk, limit computer use access to trusted, isolated environments like a sandboxed browser or container.

#### Use blocklists and allowlists

Implement a blocklist or an allowlist of websites, actions, and users. For example, if you're using the computer use tool to book tickets on a website, create an allowlist of only the websites you expect to use in that workflow.

#### Send user IDs

Send end-user IDs (optional param) to help OpenAI monitor and detect abuse.

#### Use our safety checks

The following safety checks are available to protect against prompt injection and model mistakes:

*   Malicious instruction detection
*   Irrelevant domain detection
*   Sensitive domain detection

When you receive a `pending_safety_check`, you should increase oversight into model actions, for example by handing over to an end user to explicitly acknowledge the desire to proceed with the task and ensure that the user is actively monitoring the agent's actions (e.g., by implementing something like a watch mode similar to [Operator](https://operator.chatgpt.com/)). Essentially, when safety checks fire, a human should come into the loop.

Read the [acknowledge safety checks](#acknowledge-safety-checks) section above for more details on how to proceed when you receive a `pending_safety_check`.

Where possible, it is highly recommended to pass in the optional parameter `current_url` as part of the `computer_call_output`, as it can help increase the accuracy of our safety checks.

Using current URL

```json
{
    "type": "computer_call_output",
    "call_id": "call_7OU...",
    "acknowledged_safety_checks": [],
    "output": {
        "type": "computer_screenshot",
        "image_url": "..."
    },
    "current_url": "https://openai.com"
}
```

#### Additional safety precautions

Implement additional safety precautions as best suited for your application, such as implementing guardrails that run in parallel of the computer use loop.

#### Comply with our Usage Policy

Remember, you are responsible for using our services in compliance with the [OpenAI Usage Policy](https://openai.com/policies/usage-policies/) and [Business Terms](https://openai.com/policies/business-terms/), and we encourage you to employ our safety features and tools to help ensure this compliance.

Was this page useful?
Agents
======

Learn how to build agents with the OpenAI API.

Agents represent **systems that intelligently accomplish tasks**, ranging from executing simple workflows to pursuing complex, open-ended objectives.

OpenAI provides a **rich set of composable primitives that enable you to build agents**. This guide walks through those primitives, and how they come together to form a robust agentic platform.

Overview
--------

Building agents involves assembling components across several domains—such as **models, tools, knowledge and memory, audio and speech, guardrails, and orchestration**—and OpenAI provides composable primitives for each.

|Domain|Description|OpenAI Primitives|
|---|---|---|
|Models|Core intelligence capable of reasoning, making decisions, and processing different modalities.|o1, o3-mini, GPT-4.5, GPT-4o, GPT-4o-mini|
|Tools|Interface to the world, interact with environment, function calling, built-in tools, etc.|Function calling, Web search, File search, Computer use|
|Knowledge and memory|Augment agents with external and persistent knowledge.|Vector stores, File search, Embeddings|
|Audio and speech|Create agents that can understand audio and respond back in natural language.|Audio generation, realtime, Audio agents|
|Guardrails|Prevent irrelevant, harmful, or undesirable behavior.|Moderation, Instruction hierarchy|
|Orchestration|Develop, deploy, monitor, and improve agents.|Agents SDK, Tracing, Evaluations, Fine-tuning|
|Voice agents|Create agents that can understand audio and respond back in natural language.|Realtime API, Voice support in the Agents SDK|

Models
------

|Model|Agentic Strengths|
|---|---|
|o1 and o3-mini|Best for long-term planning, hard tasks, and reasoning.|
|GPT-4.5|Best for agentic execution.|
|GPT-4o|Good balance of agentic capability and latency.|
|GPT-4o-mini|Best for low-latency.|

Large language models (LLMs) are at the core of many agentic systems, responsible for making decisions and interacting with the world. OpenAI’s models support a wide range of capabilities:

*   **High intelligence:** Capable of [reasoning](/docs/guides/reasoning) and planning to tackle the most difficult tasks.
*   **Tools:** [Call your functions](/docs/guides/function-calling) and leverage OpenAI's [built-in tools](/docs/guides/tools).
*   **Multimodality:** Natively understand text, images, audio, code, and documents.
*   **Low-latency:** Support for [real-time audio](/docs/guides/realtime) conversations and smaller, faster models.

For detailed model comparisons, visit the [models](/docs/models) page.

Tools
-----

Tools enable agents to interact with the world. OpenAI supports [**function calling**](/docs/guides/function-calling) to connect with your code, and [**built-in tools**](/docs/guides/tools) for common tasks like web searches and data retrieval.

|Tool|Description|
|---|---|
|Function calling|Interact with developer-defined code.|
|Web search|Fetch up-to-date information from the web.|
|File search|Perform semantic search across your documents.|
|Computer use|Understand and control a computer or browser.|

Knowledge and memory
--------------------

Knowledge and memory help agents store, retrieve, and utilize information beyond their initial training data. **Vector stores** enable agents to search your documents semantically and retrieve relevant information at runtime. Meanwhile, **embeddings** represent data efficiently for quick retrieval, powering dynamic knowledge solutions and long-term agent memory. You can integrate your data using OpenAI’s [vector stores](/docs/guides/retrieval#vector-stores) and [Embeddings API](/docs/guides/embeddings).

Guardrails
----------

Guardrails ensure your agents behave safely, consistently, and within your intended boundaries—critical for production deployments. Use OpenAI’s free [Moderation API](/docs/guides/moderation) to automatically filter unsafe content. Further control your agent’s behavior by leveraging the [instruction hierarchy](https://openai.github.io/openai-agents-python/guardrails/), which prioritizes developer-defined prompts and mitigates unwanted agent behaviors.

Orchestration
-------------

Building agents is a process. OpenAI provides tools to effectively build, deploy, monitor, evaluate, and improve agentic systems.

![Agent Traces UI in OpenAI Dashboard](https://cdn.openai.com/API/docs/images/orchestration.png)

|Phase|Description|OpenAI Primitives|
|---|---|---|
|Build and deploy|Rapidly build agents, enforce guardrails, and handle conversational flows using the Agents SDK.|Agents SDK|
|Monitor|Observe agent behavior in real-time, debug issues, and gain insights through tracing.|Tracing|
|Evaluate and improve|Measure agent performance, identify areas for improvement, and refine your agents.|EvaluationsFine-tuning|

Get started
-----------

Get started by installing the [OpenAI Agents SDK for Python](https://github.com/openai/openai-agents-python) via:

```text
pip install openai-agents
```

Explore the [repository](https://github.com/openai/openai-agents-python) and [documentation](https://openai.github.io/openai-agents-python/) for more details.

Was this page useful?
Voice agents
============

Learn how to build voice agents that can understand audio and respond back in natural language.

Use the OpenAI API and Agents SDK to create powerful, context-aware voice agents for applications like customer support and language tutoring. This guide helps you design and build a voice agent.

Choose the right architecture
-----------------------------

OpenAI provides two primary architectures for building voice agents:

1.  Speech-to-speech (multimodal)
2.  Chained (speech-to-text → LLM → text-to-speech)

### Speech-to-speech (multimodal) architecture

The multimodal speech-to-speech (S2S) architecture directly processes audio inputs and outputs, handling speech in real time in a single multimodal model, `gpt-4o-realtime-preview`. The model thinks and responds in speech. It doesn't rely on a transcript of the user's input—it hears emotion and intent, filters out noise, and responds directly in speech. Use this approach for highly interactive, low-latency, conversational use cases.

|Strengths|Best for|
|---|---|
|Low latency interactions|Interactive and unstructured conversations|
|Rich multimodal understanding (audio and text simultaneously)|Language tutoring and interactive learning experiences|
|Natural, fluid conversational flow|Conversational search and discovery|
|Enhanced user experience through vocal context understanding|Interactive customer service scenarios|

### Chained architecture

A chained architecture processes audio sequentially, converting audio to text, generating intelligent responses using large language models (LLMs), and synthesizing audio from text. We recommend this predictable architecture if you're new to building voice agents. Both the user input and model's response are in text, so you have a transcript and can control what happens in your application. It's also a reliable way to convert an existing LLM-based application into a voice agent.

You're chaining these models: `gpt-4o-transcribe` → `gpt-4o` → `gpt-4o-mini-tts`

|Strengths|Best for|
|---|---|
|High control and transparency|Structured workflows focused on specific user objectives|
|Robust function calling and structured interactions|Customer support|
|Reliable, predictable responses|Sales and inbound triage|
|Support for extended conversational context|Scenarios that involve transcripts and scripted responses|

Build a voice agent
-------------------

Use OpenAI's APIs and SDKs to create powerful, context-aware voice agents.

### Use a speech-to-speech architecture for realtime processing

Building a speech-to-speech voice agent requires:

1.  Establishing a connection for realtime data transfer
2.  Creating a realtime session with the Realtime API
3.  Using an OpenAI model with realtime audio input and output capabilities

To get started, read [the Realtime API guide](/docs/guides/realtime) and [the Realtime API reference](/docs/api-reference/realtime-sessions/create). Compatible models include `gpt-4o-realtime-preview` and `gpt-4o-mini-realtime-preview`.

### Chain together audio input → text processing → audio output

The Agents SDK supports extending your existing agents with voice capabilities. Get started by installing the [OpenAI Agents SDK for Python](https://openai.github.io/openai-agents-python/voice/quickstart/) with voice support:

```text
pip install openai-agents[voice]
```

See the [Agents SDK voice agents quickstart in GitHub](https://openai.github.io/openai-agents-python/voice/quickstart/) to follow a complete example.

In the example, you'll:

*   Run a speech-to-text model to turn audio into text.
*   Run your code, which is usually an agentic workflow, to produce a result.
*   Run a text-to-speech model to turn the result text back into audio.

Was this page useful?
Realtime API

Beta

====================

Build low-latency, multi-modal experiences with the Realtime API.

The OpenAI Realtime API enables low-latency, multimodal interactions including speech-to-speech conversational experiences and real-time transcription.

This API works with natively multimodal models such as [GPT-4o](/docs/models/gpt-4o-realtime) and [GPT-4o mini](/docs/models/gpt-4o-mini-realtime), offering capabilities such as real-time text and audio processing, function calling, and speech generation, and with the latest transcription models [GPT-4o Transcribe](/docs/models/gpt-4o-transcribe) and [GPT-4o mini Transcribe](/docs/models/gpt-4o-mini-transcribe).

Get started with the Realtime API
---------------------------------

You can connect to the Realtime API in two ways:

*   Using [WebRTC](#connect-with-webrtc), which is ideal for client-side applications (for example, a web app)
*   Using [WebSockets](#connect-with-websockets), which is great for server-to-server applications (from your backend or if you're building a voice agent over phone for example)

Start by exploring examples and partner integrations below, or learn how to connect to the Realtime API using the most relevant method for your use case below.

### Example applications

Check out one of the example applications below to see the Realtime API in action.

[

Realtime Console

To get started quickly, download and configure the Realtime console demo. See events flowing back and forth, and inspect their contents. Learn how to execute custom logic with function calling.

](https://github.com/openai/openai-realtime-console)[

Realtime Solar System demo

A demo of the Realtime API with the WebRTC integration, navigating the solar system through voice thanks to function calling.

](https://github.com/openai/openai-realtime-solar-system)[

Twilio Integration Demo

A demo combining the Realtime API with Twilio to build an AI calling assistant.

](https://github.com/openai/openai-realtime-twilio-demo)[

Realtime API Agents Demo

A demonstration of handoffs between Realtime API voice agents with reasoning model validation.

](https://github.com/openai/openai-realtime-agents)

### Partner integrations

Check out these partner integrations, which use the Realtime API in frontend applications and telephony use cases.

[

LiveKit integration guide

How to use the Realtime API with LiveKit's WebRTC infrastructure.

](https://docs.livekit.io/agents/openai/overview/)[

Twilio integration guide

Build Realtime apps using Twilio's powerful voice APIs.

](https://www.twilio.com/en-us/blog/twilio-openai-realtime-api-launch-integration)[

Agora integration quickstart

How to integrate Agora's real-time audio communication capabilities with the Realtime API.

](https://docs.agora.io/en/open-ai-integration/get-started/quickstart)[

Pipecat integration guide

Create voice agents with OpenAI audio models and Pipecat orchestration framework.

](https://docs.pipecat.ai/guides/features/openai-audio-models-and-apis)[](https://github.com/craigsdennis/talk-to-javascript-openai-workers)

[

](https://github.com/craigsdennis/talk-to-javascript-openai-workers)

[

Client-side tool calling

](https://github.com/craigsdennis/talk-to-javascript-openai-workers)

[](https://github.com/craigsdennis/talk-to-javascript-openai-workers)

[Built with Cloudflare Workers, an example application showcasing client-side tool calling. Also check out the](https://github.com/craigsdennis/talk-to-javascript-openai-workers) [tutorial on YouTube](https://www.youtube.com/watch?v=TcOytsfva0o).

Use cases
---------

The most common use case for the Realtime API is to build a real-time, speech-to-speech, conversational experience. This is great for building [voice agents](/docs/guides/voice-agents) and other voice-enabled applications.

The Realtime API can also be used independently for transcription and turn detection use cases. A client can stream audio in and have Realtime API produce streaming transcripts when speech is detected.

Both use-cases benefit from built-in [voice activity detection (VAD)](/docs/guides/realtime-vad) to automatically detect when a user is done speaking. This can be helpful to seamlessly handle conversation turns, or to analyze transcriptions one phrase at a time.

Learn more about these use cases in the dedicated guides.

[

Realtime Speech-to-Speech

Learn to use the Realtime API for streaming speech-to-speech conversations.

](/docs/guides/realtime-conversations)[

Realtime Transcription

Learn to use the Realtime API for transcription-only use cases.

](/docs/guides/realtime-transcription)

Depending on your use case (conversation or transcription), you should initialize a session in different ways. Use the switcher below to see the details for each case.

Connect with WebRTC
-------------------

[WebRTC](https://webrtc.org/) is a powerful set of standard interfaces for building real-time applications. The OpenAI Realtime API supports connecting to realtime models through a WebRTC peer connection. Follow this guide to learn how to configure a WebRTC connection to the Realtime API.

### Overview

In scenarios where you would like to connect to a Realtime model from an insecure client over the network (like a web browser), we recommend using the WebRTC connection method. WebRTC is better equipped to handle variable connection states, and provides a number of convenient APIs for capturing user audio inputs and playing remote audio streams from the model.

Connecting to the Realtime API from the browser should be done with an ephemeral API key, [generated via the OpenAI REST API](/docs/api-reference/realtime-sessions). The process for initializing a WebRTC connection is as follows (assuming a web browser client):

1.  A browser makes a request to a developer-controlled server to mint an ephemeral API key.
2.  The developer's server uses a [standard API key](/settings/organization/api-keys) to request an ephemeral key from the [OpenAI REST API](/docs/api-reference/realtime-sessions), and returns that new key to the browser. Note that ephemeral keys currently expire one minute after being issued.
3.  The browser uses the ephemeral key to authenticate a session directly with the OpenAI Realtime API as a [WebRTC peer connection](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection).

![connect to realtime via WebRTC](https://openaidevs.retool.com/api/file/55b47800-9aaf-48b9-90d5-793ab227ddd3)

While it is technically possible to use a [standard API key](/settings/organization/api-keys) to authenticate client-side WebRTC sessions, **this is a dangerous and insecure practice** because it leaks your secret key. Standard API keys grant access to your full OpenAI API account, and should only be used in secure server-side environments. We recommend ephemeral keys in client-side applications whenever possible.

### Connection details

Connecting via WebRTC requires the following connection information:

|URL|https://api.openai.com/v1/realtime|
|Query Parameters|modelRealtime model ID to connect to, like gpt-4o-realtime-preview-2024-12-17|
|Headers|Authorization: Bearer EPHEMERAL_KEYSubstitute EPHEMERAL_KEY with an ephemeral API token - see below for details on how to generate one.|

The following example shows how to initialize a [WebRTC session](https://webrtc.org/getting-started/overview) (including the data channel to send and receive Realtime API events). It assumes you have already fetched an ephemeral API token (example server code for this can be found in the [next section](#creating-an-ephemeral-token)).

```javascript
async function init() {
  // Get an ephemeral key from your server - see server code below
  const tokenResponse = await fetch("/session");
  const data = await tokenResponse.json();
  const EPHEMERAL_KEY = data.client_secret.value;

  // Create a peer connection
  const pc = new RTCPeerConnection();

  // Set up to play remote audio from the model
  const audioEl = document.createElement("audio");
  audioEl.autoplay = true;
  pc.ontrack = e => audioEl.srcObject = e.streams[0];

  // Add local audio track for microphone input in the browser
  const ms = await navigator.mediaDevices.getUserMedia({
    audio: true
  });
  pc.addTrack(ms.getTracks()[0]);

  // Set up data channel for sending and receiving events
  const dc = pc.createDataChannel("oai-events");
  dc.addEventListener("message", (e) => {
    // Realtime server events appear here!
    console.log(e);
  });

  // Start the session using the Session Description Protocol (SDP)
  const offer = await pc.createOffer();
  await pc.setLocalDescription(offer);

  const baseUrl = "https://api.openai.com/v1/realtime";
  const model = "gpt-4o-realtime-preview-2024-12-17";
  const sdpResponse = await fetch(`${baseUrl}?model=${model}`, {
    method: "POST",
    body: offer.sdp,
    headers: {
      Authorization: `Bearer ${EPHEMERAL_KEY}`,
      "Content-Type": "application/sdp"
    },
  });

  const answer = {
    type: "answer",
    sdp: await sdpResponse.text(),
  };
  await pc.setRemoteDescription(answer);
}

init();
```

The WebRTC APIs provide rich controls for handling media streams and input devices. For more guidance on building user interfaces on top of WebRTC, [refer to the docs on MDN](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API).

### Creating an ephemeral token

To create an ephemeral token to use on the client-side, you will need to build a small server-side application (or integrate with an existing one) to make an [OpenAI REST API](/docs/api-reference/realtime-sessions) request for an ephemeral key. You will use a [standard API key](/settings/organization/api-keys) to authenticate this request on your backend server.

Below is an example of a simple Node.js [express](https://expressjs.com/) server which mints an ephemeral API key using the REST API:

```javascript
import express from "express";

const app = express();

// An endpoint which would work with the client code above - it returns
// the contents of a REST API request to this protected endpoint
app.get("/session", async (req, res) => {
  const r = await fetch("https://api.openai.com/v1/realtime/sessions", {
    method: "POST",
    headers: {
      "Authorization": `Bearer ${process.env.OPENAI_API_KEY}`,
      "Content-Type": "application/json",
    },
    body: JSON.stringify({
      model: "gpt-4o-realtime-preview-2024-12-17",
      voice: "verse",
    }),
  });
  const data = await r.json();

  // Send back the JSON we received from the OpenAI REST API
  res.send(data);
});

app.listen(3000);
```

You can create a server endpoint like this one on any platform that can send and receive HTTP requests. Just ensure that **you only use standard OpenAI API keys on the server, not in the browser.**

### Sending and receiving events

To learn how to send and receive events over the WebRTC data channel, refer to the [Realtime conversations guide](/docs/guides/realtime-conversations#handling-audio-with-webrtc).

Connect with WebSockets
-----------------------

[WebSockets](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API) are a broadly supported API for realtime data transfer, and a great choice for connecting to the OpenAI Realtime API in server-to-server applications. For browser and mobile clients, we recommend connecting via [WebRTC](#connect-with-webrtc).

### Overview

In a server-to-server integration with Realtime, your backend system will connect via WebSocket directly to the Realtime API. You can use a [standard API key](/settings/organization/api-keys) to authenticate this connection, since the token will only be available on your secure backend server.

![connect directly to realtime API](https://openaidevs.retool.com/api/file/464d4334-c467-4862-901b-d0c6847f003a)

WebSocket connections can also be authenticated with an ephemeral client token ([as shown above in the WebRTC section](#creating-an-ephemeral-token)) if you choose to connect to the Realtime API via WebSocket on a client device.

  

Standard OpenAI API tokens **should only be used in secure server-side environments**.

### Connection details

Speech-to-Speech

Connecting via WebSocket requires the following connection information:

|URL|wss://api.openai.com/v1/realtime|
|Query Parameters|modelRealtime model ID to connect to, like gpt-4o-realtime-preview-2024-12-17|
|Headers|Authorization: Bearer YOUR_API_KEYSubstitute YOUR_API_KEY with a standard API key on the server, or an ephemeral token on insecure clients (note that WebRTC is recommended for this use case).OpenAI-Beta: realtime=v1This header is required during the beta period.|

Below are several examples of using these connection details to initialize a WebSocket connection to the Realtime API.

ws module (Node.js)

Connect using the ws module (Node.js)

```javascript
import WebSocket from "ws";

const url = "wss://api.openai.com/v1/realtime?model=gpt-4o-realtime-preview-2024-12-17";
const ws = new WebSocket(url, {
  headers: {
    "Authorization": "Bearer " + process.env.OPENAI_API_KEY,
    "OpenAI-Beta": "realtime=v1",
  },
});

ws.on("open", function open() {
  console.log("Connected to server.");
});

ws.on("message", function incoming(message) {
  console.log(JSON.parse(message.toString()));
});
```

websocket-client (Python)

Connect with websocket-client (Python)

```python
# example requires websocket-client library:
# pip install websocket-client

import os
import json
import websocket

OPENAI_API_KEY = os.environ.get("OPENAI_API_KEY")

url = "wss://api.openai.com/v1/realtime?model=gpt-4o-realtime-preview-2024-12-17"
headers = [
    "Authorization: Bearer " + OPENAI_API_KEY,
    "OpenAI-Beta: realtime=v1"
]

def on_open(ws):
    print("Connected to server.")

def on_message(ws, message):
    data = json.loads(message)
    print("Received event:", json.dumps(data, indent=2))

ws = websocket.WebSocketApp(
    url,
    header=headers,
    on_open=on_open,
    on_message=on_message,
)

ws.run_forever()
```

WebSocket (browsers)

Connect with standard WebSocket (browsers)

```javascript
/*
Note that in client-side environments like web browsers, we recommend
using WebRTC instead. It is possible, however, to use the standard 
WebSocket interface in browser-like environments like Deno and 
Cloudflare Workers.
*/

const ws = new WebSocket(
  "wss://api.openai.com/v1/realtime?model=gpt-4o-realtime-preview-2024-12-17",
  [
    "realtime",
    // Auth
    "openai-insecure-api-key." + OPENAI_API_KEY, 
    // Optional
    "openai-organization." + OPENAI_ORG_ID,
    "openai-project." + OPENAI_PROJECT_ID,
    // Beta protocol, required
    "openai-beta.realtime-v1"
  ]
);

ws.on("open", function open() {
  console.log("Connected to server.");
});

ws.on("message", function incoming(message) {
  console.log(message.data);
});
```

### Sending and receiving events

To learn how to send and receive events over Websockets, refer to the [Realtime conversations guide](/docs/guides/realtime-conversations#handling-audio-with-websockets).

Transcription

Connecting via WebSocket requires the following connection information:

|URL|wss://api.openai.com/v1/realtime|
|Query Parameters|intentThe intent of the connection: transcription|
|Headers|Authorization: Bearer YOUR_API_KEYSubstitute YOUR_API_KEY with a standard API key on the server, or an ephemeral token on insecure clients (note that WebRTC is recommended for this use case).OpenAI-Beta: realtime=v1This header is required during the beta period.|

Below are several examples of using these connection details to initialize a WebSocket connection to the Realtime API.

ws module (Node.js)

Connect using the ws module (Node.js)

```javascript
import WebSocket from "ws";

const url = "wss://api.openai.com/v1/realtime?intent=transcription";
const ws = new WebSocket(url, {
  headers: {
    "Authorization": "Bearer " + process.env.OPENAI_API_KEY,
    "OpenAI-Beta": "realtime=v1",
  },
});

ws.on("open", function open() {
  console.log("Connected to server.");
});

ws.on("message", function incoming(message) {
  console.log(JSON.parse(message.toString()));
});
```

websocket-client (Python)

Connect with websocket-client (Python)

```python
import os
import json
import websocket

OPENAI_API_KEY = os.environ.get("OPENAI_API_KEY")

url = "wss://api.openai.com/v1/realtime?intent=transcription"
headers = [
    "Authorization: Bearer " + OPENAI_API_KEY,
    "OpenAI-Beta: realtime=v1"
]

def on_open(ws):
    print("Connected to server.")

def on_message(ws, message):
    data = json.loads(message)
    print("Received event:", json.dumps(data, indent=2))

ws = websocket.WebSocketApp(
    url,
    header=headers,
    on_open=on_open,
    on_message=on_message,
)

ws.run_forever()
```

WebSocket (browsers)

Connect with standard WebSocket (browsers)

```javascript
/*
Note that in client-side environments like web browsers, we recommend
using WebRTC instead. It is possible, however, to use the standard 
WebSocket interface in browser-like environments like Deno and 
Cloudflare Workers.
*/

const ws = new WebSocket(
  "wss://api.openai.com/v1/realtime?intent=transcription",
  [
    "realtime",
    // Auth
    "openai-insecure-api-key." + OPENAI_API_KEY, 
    // Optional
    "openai-organization." + OPENAI_ORG_ID,
    "openai-project." + OPENAI_PROJECT_ID,
    // Beta protocol, required
    "openai-beta.realtime-v1"
  ]
);

ws.on("open", function open() {
  console.log("Connected to server.");
});

ws.on("message", function incoming(message) {
  console.log(message.data);
});
```

### Sending and receiving events

To learn how to send and receive events over Websockets, refer to the [Realtime transcription guide](/docs/guides/realtime-transcription#handling-transcriptions).

Was this page useful?
Realtime conversations

Beta

==============================

Learn how to manage Realtime speech-to-speech conversations.

Once you have connected to the Realtime API through either [WebRTC](/docs/guides/realtime-webrtc) or [WebSocket](/docs/guides/realtime-websocket), you can call a Realtime model (such as [gpt-4o-realtime-preview](/docs/models/gpt-4o-realtime-preview)) to have speech-to-speech conversations. Doing so will require you to **send client events** to initiate actions, and **listen for server events** to respond to actions taken by the Realtime API.

This guide will walk through the event flows required to use model capabilities like audio and text generation and function calling, and how to think about the state of a Realtime Session.

If you do not need to have a conversation with the model, meaning you don't expect any response, you can use the Realtime API in [transcription mode](/docs/guides/realtime-transcription).

Realtime speech-to-speech sessions
----------------------------------

A Realtime Session is a stateful interaction between the model and a connected client. The key components of the session are:

*   The **Session** object, which controls the parameters of the interaction, like the model being used, the voice used to generate output, and other configuration.
*   A **Conversation**, which represents user input Items and model output Items generated during the current session.
*   **Responses**, which are model-generated audio or text Items that are added to the Conversation.

**Input audio buffer and WebSockets**

If you are using WebRTC, much of the media handling required to send and receive audio from the model is assisted by WebRTC APIs.

  

If you are using WebSockets for audio, you will need to manually interact with the **input audio buffer** by sending audio to the server, sent with JSON events with base64-encoded audio.

All these components together make up a Realtime Session. You will use client events to update the state of the session, and listen for server events to react to state changes within the session.

![diagram realtime state](https://openaidevs.retool.com/api/file/11fe71d2-611e-4a26-a587-881719a90e56)

Session lifecycle events
------------------------

After initiating a session via either [WebRTC](/docs/guides/realtime-webrtc) or [WebSockets](/docs/guides/realtime-websockets), the server will send a [`session.created`](/docs/api-reference/realtime-server-events/session/created) event indicating the session is ready. On the client, you can update the current session configuration with the [`session.update`](/docs/api-reference/realtime-client-events/session/update) event. Most session properties can be updated at any time, except for the `voice` the model uses for audio output, after the model has responded with audio once during the session. The maximum duration of a Realtime session is **30 minutes**.

The following example shows updating the session with a `session.update` client event. See the [WebRTC](/docs/guides/realtime-webrtc#sending-and-receiving-events) or [WebSocket](/docs/guides/realtime-websocket#sending-and-receiving-events) guide for more on sending client events over these channels.

Update the system instructions used by the model in this session

```javascript
const event = {
  type: "session.update",
  session: {
    instructions: "Never use the word 'moist' in your responses!"
  },
};

// WebRTC data channel and WebSocket both have .send()
dataChannel.send(JSON.stringify(event));
```

```python
event = {
    "type": "session.update",
    "session": {
        "instructions": "Never use the word 'moist' in your responses!"
    }
}
ws.send(json.dumps(event))
```

When the session has been updated, the server will emit a [`session.updated`](/docs/api-reference/realtime-server-events/session/updated) event with the new state of the session.

||
|session.update|session.createdsession.updated|

Text inputs and outputs
-----------------------

To generate text with a Realtime model, you can add text inputs to the current conversation, ask the model to generate a response, and listen for server-sent events indicating the progress of the model's response. In order to generate text, the [session must be configured](/docs/api-reference/realtime-client-events/session/update) with the `text` modality (this is true by default).

Create a new text conversation item using the [`conversation.item.create`](/docs/api-reference/realtime-client-events/conversation/item/create) client event. This is similar to sending a [user message (prompt) in Chat Completions](/docs/guides/text-generation) in the REST API.

Create a conversation item with user input

```javascript
const event = {
  type: "conversation.item.create",
  item: {
    type: "message",
    role: "user",
    content: [
      {
        type: "input_text",
        text: "What Prince album sold the most copies?",
      }
    ]
  },
};

// WebRTC data channel and WebSocket both have .send()
dataChannel.send(JSON.stringify(event));
```

```python
event = {
    "type": "conversation.item.create",
    "item": {
        "type": "message",
        "role": "user",
        "content": [
            {
                "type": "input_text",
                "text": "What Prince album sold the most copies?",
            }
        ]
    }
}
ws.send(json.dumps(event))
```

After adding the user message to the conversation, send the [`response.create`](/docs/api-reference/realtime-client-events/response/create) event to initiate a response from the model. If both audio and text are enabled for the current session, the model will respond with both audio and text content. If you'd like to generate text only, you can specify that when sending the `response.create` client event, as shown below.

Generate a text-only response

```javascript
const event = {
  type: "response.create",
  response: {
    modalities: [ "text" ]
  },
};

// WebRTC data channel and WebSocket both have .send()
dataChannel.send(JSON.stringify(event));
```

```python
event = {
    "type": "response.create",
    "response": {
        "modalities": [ "text" ]
    }
}
ws.send(json.dumps(event))
```

When the response is completely finished, the server will emit the [`response.done`](/docs/api-reference/realtime-server-events/response/done) event. This event will contain the full text generated by the model, as shown below.

Listen for response.done to see the final results

```javascript
function handleEvent(e) {
  const serverEvent = JSON.parse(e.data);
  if (serverEvent.type === "response.done") {
    console.log(serverEvent.response.output[0]);
  }
}

// Listen for server messages (WebRTC)
dataChannel.addEventListener("message", handleEvent);

// Listen for server messages (WebSocket)
// ws.on("message", handleEvent);
```

```python
def on_message(ws, message):
    server_event = json.loads(message)
    if server_event.type == "response.done":
        print(server_event.response.output[0])
```

While the model response is being generated, the server will emit a number of lifecycle events during the process. You can listen for these events, such as [`response.text.delta`](/docs/api-reference/realtime-server-events/response/text/delta), to provide realtime feedback to users as the response is generated. A full listing of the events emitted by there server are found below under **related server events**. They are provided in the rough order of when they are emitted, along with relevant client-side events for text generation.

||
|conversation.item.createresponse.create|conversation.item.createdresponse.createdresponse.output_item.addedresponse.content_part.addedresponse.text.deltaresponse.text.doneresponse.content_part.doneresponse.output_item.doneresponse.donerate_limits.updated|

Audio inputs and outputs
------------------------

One of the most powerful features of the Realtime API is voice-to-voice interaction with the model, without an intermediate text-to-speech or speech-to-text step. This enables lower latency for voice interfaces, and gives the model more data to work with around the tone and inflection of voice input.

### Voice options

Realtime sessions can be configured to use one of several built‑in voices when producing audio output. You can set the `voice` on session creation (or on a `response.create`) to control how the model sounds. Current voice options are `alloy`, `ash`, `ballad`, `coral`, `echo`, `sage`, `shimmer`, and `verse`. Once the model has emitted audio in a session, the `voice` cannot be modified for that session.

### Handling audio with WebRTC

If you are connecting to the Realtime API using WebRTC, the Realtime API is acting as a [peer connection](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection) to your client. Audio output from the model is delivered to your client as a [remote media stream](hhttps://developer.mozilla.org/en-US/docs/Web/API/MediaStream). Audio input to the model is collected using audio devices ([`getUserMedia`](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia)), and media streams are added as tracks to to the peer connection.

The example code from the [WebRTC connection guide](/docs/guides/realtime-webrtc) shows a basic example of configuring both local and remote audio using browser APIs:

```javascript
// Create a peer connection
const pc = new RTCPeerConnection();

// Set up to play remote audio from the model
const audioEl = document.createElement("audio");
audioEl.autoplay = true;
pc.ontrack = e => audioEl.srcObject = e.streams[0];

// Add local audio track for microphone input in the browser
const ms = await navigator.mediaDevices.getUserMedia({
  audio: true
});
pc.addTrack(ms.getTracks()[0]);
```

The snippet above enables simple interaction with the Realtime API, but there's much more that can be done. For more examples of different kinds of user interfaces, check out the [WebRTC samples](https://github.com/webrtc/samples) repository. Live demos of these samples can also be [found here](https://webrtc.github.io/samples/).

Using [media captures and streams](https://developer.mozilla.org/en-US/docs/Web/API/Media_Capture_and_Streams_API) in the browser enables you to do things like mute and unmute microphones, select which device to collect input from, and more.

### Client and server events for audio in WebRTC

By default, WebRTC clients don't need to send any client events to the Realtime API before sending audio inputs. Once a local audio track is added to the peer connection, your users can just start talking!

However, WebRTC clients still receive a number of server-sent lifecycle events as audio is moving back and forth between client and server over the peer connection. Examples include:

*   When input is sent over the local media track, you will receive [`input_audio_buffer.speech_started`](/docs/api-reference/realtime-server-events/input_audio_buffer/speech_started) events from the server.
*   When local audio input stops, you'll receive the [`input_audio_buffer.speech_stopped`](/docs/api-reference/realtime-server-events/input_audio_buffer/speech_started) event.
*   You'll receive [delta events for the in-progress audio transcript](/docs/api-reference/realtime-server-events/response/audio_transcript/delta).
*   You'll receive a [`response.done`](/docs/api-reference/realtime-server-events/response/done) event when the model has transcribed and completed sending a response.

Manipulating WebRTC APIs for media streams may give you all the control you need. However, it may occasionally be necessary to use lower-level interfaces for audio input and output. Refer to the WebSockets section below for more information and a listing of events required for granular audio input handling.

### Handling audio with WebSockets

When sending and receiving audio over a WebSocket, you will have a bit more work to do in order to send media from the client, and receive media from the server. Below, you'll find a table describing the flow of events during a WebSocket session that are necessary to send and receive audio over the WebSocket.

The events below are given in lifecycle order, though some events (like the `delta` events) may happen concurrently.

||
|Session initialization|session.update|session.createdsession.updated|
|User audio input|conversation.item.create  (send whole audio message)input_audio_buffer.append  (stream audio in chunks)input_audio_buffer.commit  (used when VAD is disabled)response.create  (used when VAD is disabled)|input_audio_buffer.speech_startedinput_audio_buffer.speech_stoppedinput_audio_buffer.committed|
|Server audio output|input_audio_buffer.clear  (used when VAD is disabled)|conversation.item.createdresponse.createdresponse.output_item.createdresponse.content_part.addedresponse.audio.deltaresponse.audio_transcript.deltaresponse.text.deltaresponse.audio.doneresponse.audio_transcript.doneresponse.text.doneresponse.content_part.doneresponse.output_item.doneresponse.donerate_limits.updated|

### Streaming audio input to the server

To stream audio input to the server, you can use the [`input_audio_buffer.append`](/docs/api-reference/realtime-client-events/input_audio_buffer/append) client event. This event requires you to send chunks of **Base64-encoded audio bytes** to the Realtime API over the socket. Each chunk cannot exceed 15 MB in size.

The format of the input chunks can be configured either for the entire session, or per response.

*   Session: `session.input_audio_format` in [`session.update`](/docs/api-reference/realtime-client-events/session/update)
*   Response: `response.input_audio_format` in [`response.create`](/docs/api-reference/realtime-client-events/response/create)

Append audio input bytes to the conversation

```javascript
import fs from 'fs';
import decodeAudio from 'audio-decode';

// Converts Float32Array of audio data to PCM16 ArrayBuffer
function floatTo16BitPCM(float32Array) {
  const buffer = new ArrayBuffer(float32Array.length * 2);
  const view = new DataView(buffer);
  let offset = 0;
  for (let i = 0; i < float32Array.length; i++, offset += 2) {
    let s = Math.max(-1, Math.min(1, float32Array[i]));
    view.setInt16(offset, s < 0 ? s * 0x8000 : s * 0x7fff, true);
  }
  return buffer;
}

// Converts a Float32Array to base64-encoded PCM16 data
base64EncodeAudio(float32Array) {
  const arrayBuffer = floatTo16BitPCM(float32Array);
  let binary = '';
  let bytes = new Uint8Array(arrayBuffer);
  const chunkSize = 0x8000; // 32KB chunk size
  for (let i = 0; i < bytes.length; i += chunkSize) {
    let chunk = bytes.subarray(i, i + chunkSize);
    binary += String.fromCharCode.apply(null, chunk);
  }
  return btoa(binary);
}

// Fills the audio buffer with the contents of three files,
// then asks the model to generate a response.
const files = [
  './path/to/sample1.wav',
  './path/to/sample2.wav',
  './path/to/sample3.wav'
];

for (const filename of files) {
  const audioFile = fs.readFileSync(filename);
  const audioBuffer = await decodeAudio(audioFile);
  const channelData = audioBuffer.getChannelData(0);
  const base64Chunk = base64EncodeAudio(channelData);
  ws.send(JSON.stringify({
    type: 'input_audio_buffer.append',
    audio: base64Chunk
  }));
});

ws.send(JSON.stringify({type: 'input_audio_buffer.commit'}));
ws.send(JSON.stringify({type: 'response.create'}));
```

```python
import base64
import json
import struct
import soundfile as sf
from websocket import create_connection

# ... create websocket-client named ws ...

def float_to_16bit_pcm(float32_array):
    clipped = [max(-1.0, min(1.0, x)) for x in float32_array]
    pcm16 = b''.join(struct.pack('<h', int(x * 32767)) for x in clipped)
    return pcm16

def base64_encode_audio(float32_array):
    pcm_bytes = float_to_16bit_pcm(float32_array)
    encoded = base64.b64encode(pcm_bytes).decode('ascii')
    return encoded

files = [
    './path/to/sample1.wav',
    './path/to/sample2.wav',
    './path/to/sample3.wav'
]

for filename in files:
    data, samplerate = sf.read(filename, dtype='float32')  
    channel_data = data[:, 0] if data.ndim > 1 else data
    base64_chunk = base64_encode_audio(channel_data)
    
    # Send the client event
    event = {
        "type": "input_audio_buffer.append",
        "audio": base64_chunk
    }
    ws.send(json.dumps(event))
```

### Send full audio messages

It is also possible to create conversation messages that are full audio recordings. Use the [`conversation.item.create`](/docs/api-reference/realtime-client-events/conversation/item/create) client event to create messages with `input_audio` content.

Create full audio input conversation items

```javascript
const fullAudio = "<a base64-encoded string of audio bytes>";

const event = {
  type: "conversation.item.create",
  item: {
    type: "message",
    role: "user",
    content: [
      {
        type: "input_audio",
        audio: fullAudio,
      },
    ],
  },
};

// WebRTC data channel and WebSocket both have .send()
dataChannel.send(JSON.stringify(event));
```

```python
fullAudio = "<a base64-encoded string of audio bytes>"

event = {
    "type": "conversation.item.create",
    "item": {
        "type": "message",
        "role": "user",
        "content": [
            {
                "type": "input_audio",
                "audio": fullAudio,
            }
        ],
    },
}

ws.send(json.dumps(event))
```

### Working with audio output from a WebSocket

**To play output audio back on a client device like a web browser, we recommend using WebRTC rather than WebSockets**. WebRTC will be more robust sending media to client devices over uncertain network conditions.

But to work with audio output in server-to-server applications using a WebSocket, you will need to listen for [`response.audio.delta`](/docs/api-reference/realtime-server-events/response/audio/delta) events containing the Base64-encoded chunks of audio data from the model. You will either need to buffer these chunks and write them out to a file, or maybe immediately stream them to another source like [a phone call with Twilio](https://www.twilio.com/en-us/blog/twilio-openai-realtime-api-launch-integration).

Note that the [`response.audio.done`](/docs/api-reference/realtime-server-events/response/audio/done) and [`response.done`](/docs/api-reference/realtime-server-events/response/done) events won't actually contain audio data in them - just audio content transcriptions. To get the actual bytes, you'll need to listen for the [`response.audio.delta`](/docs/api-reference/realtime-server-events/response/audio/delta) events.

The format of the output chunks can be configured either for the entire session, or per response.

*   Session: `session.output_audio_format` in [`session.update`](/docs/api-reference/realtime-client-events/session/update)
*   Response: `response.output_audio_format` in [`response.create`](/docs/api-reference/realtime-client-events/response/create)

Listen for response.audio.delta events

```javascript
function handleEvent(e) {
  const serverEvent = JSON.parse(e.data);
  if (serverEvent.type === "response.audio.delta") {
    // Access Base64-encoded audio chunks
    // console.log(serverEvent.delta);
  }
}

// Listen for server messages (WebSocket)
ws.on("message", handleEvent);
```

```python
def on_message(ws, message):
    server_event = json.loads(message)
    if server_event.type == "response.audio.delta":
        # Access Base64-encoded audio chunks:
        # print(server_event.delta)
```

Voice activity detection
------------------------

By default, Realtime sessions have **voice activity detection (VAD)** enabled, which means the API will determine when the user has started or stopped speaking and respond automatically.

Read more about how to configure VAD in our [voice activity detection](/docs/guides/realtime-vad) guide.

### Disable VAD

VAD can be disabled by setting `turn_detection` to `null` with the [`session.update`](/docs/api-reference/realtime-client-events/session/update) client event. This can be useful for interfaces where you would like to take granular control over audio input, like [push to talk](https://en.wikipedia.org/wiki/Push-to-talk) interfaces.

When VAD is disabled, the client will have to manually emit some additional client events to trigger audio responses:

*   Manually send [`input_audio_buffer.commit`](/docs/api-reference/realtime-client-events/input_audio_buffer/commit), which will create a new user input item for the conversation.
*   Manually send [`response.create`](/docs/api-reference/realtime-client-events/response/create) to trigger an audio response from the model.
*   Send [`input_audio_buffer.clear`](/docs/api-reference/realtime-client-events/input_audio_buffer/clear) before beginning a new user input.

### Keep VAD, but disable automatic responses

If you would like to keep VAD mode enabled, but would just like to retain the ability to manually decide when a response is generated, you can set `turn_detection.interrupt_response` and `turn_detection.create_response` to `false` with the [`session.update`](/docs/api-reference/realtime-client-events/session/update) client event. This will retain all the behavior of VAD but not automatically create new Responses. Clients can trigger these manually with a [`response.create`](/docs/api-reference/realtime-client-events/response/create) event.

This can be useful for moderation or input validation or RAG patterns, where you're comfortable trading a bit more latency in the interaction for control over inputs.

Create responses outside the default conversation
-------------------------------------------------

By default, all responses generated during a session are added to the session's conversation state (the "default conversation"). However, you may want to generate model responses outside the context of the session's default conversation, or have multiple responses generated concurrently. You might also want to have more granular control over which conversation items are considered while the model generates a response (e.g. only the last N number of turns).

Generating "out-of-band" responses which are not added to the default conversation state is possible by setting the `response.conversation` field to the string `none` when creating a response with the [`response.create`](/docs/api-reference/realtime-client-events/response/create) client event.

When creating an out-of-band response, you will probably also want some way to identify which server-sent events pertain to this response. You can provide `metadata` for your model response that will help you identify which response is being generated for this client-sent event.

Create an out-of-band model response

```javascript
const prompt = `
Analyze the conversation so far. If it is related to support, output
"support". If it is related to sales, output "sales".
`;

const event = {
  type: "response.create",
  response: {
    // Setting to "none" indicates the response is out of band
    // and will not be added to the default conversation
    conversation: "none",

    // Set metadata to help identify responses sent back from the model
    metadata: { topic: "classification" },
    
    // Set any other available response fields
    modalities: [ "text" ],
    instructions: prompt,
  },
};

// WebRTC data channel and WebSocket both have .send()
dataChannel.send(JSON.stringify(event));
```

```python
prompt = """
Analyze the conversation so far. If it is related to support, output
"support". If it is related to sales, output "sales".
"""

event = {
    "type": "response.create",
    "response": {
        # Setting to "none" indicates the response is out of band,
        # and will not be added to the default conversation
        "conversation": "none",

        # Set metadata to help identify responses sent back from the model
        "metadata": { "topic": "classification" },

        # Set any other available response fields
        "modalities": [ "text" ],
        "instructions": prompt,
    },
}

ws.send(json.dumps(event))
```

Now, when you listen for the [`response.done`](/docs/api-reference/realtime-server-events/response/done) server event, you can identify the result of your out-of-band response.

Create an out-of-band model response

```javascript
function handleEvent(e) {
  const serverEvent = JSON.parse(e.data);
  if (
    serverEvent.type === "response.done" &&
    serverEvent.response.metadata?.topic === "classification"
  ) {
    // this server event pertained to our OOB model response
    console.log(serverEvent.response.output[0]);
  }
}

// Listen for server messages (WebRTC)
dataChannel.addEventListener("message", handleEvent);

// Listen for server messages (WebSocket)
// ws.on("message", handleEvent);
```

```python
def on_message(ws, message):
    server_event = json.loads(message)
    topic = ""

    # See if metadata is present
    try:
        topic = server_event.response.metadata.topic
    except AttributeError:
        print("topic not set")
    
    if server_event.type == "response.done" and topic == "classification":
        # this server event pertained to our OOB model response
        print(server_event.response.output[0])
```

### Create a custom context for responses

You can also construct a custom context that the model will use to generate a response, outside the default/current conversation. This can be done using the `input` array on a [`response.create`](/docs/api-reference/realtime-client-events/response/create) client event. You can use new inputs, or reference existing input items in the conversation by ID.

Listen for out-of-band model response with custom context

```javascript
const event = {
  type: "response.create",
  response: {
    conversation: "none",
    metadata: { topic: "pizza" },
    modalities: [ "text" ],

    // Create a custom input array for this request with whatever context
    // is appropriate
    input: [
      // potentially include existing conversation items:
      {
        type: "item_reference",
        id: "some_conversation_item_id"
      },
      {
        type: "message",
        role: "user",
        content: [
          {
            type: "input_text",
            text: "Is it okay to put pineapple on pizza?",
          },
        ],
      },
    ],
  },
};

// WebRTC data channel and WebSocket both have .send()
dataChannel.send(JSON.stringify(event));
```

```python
event = {
    "type": "response.create",
    "response": {
        "conversation": "none",
        "metadata": { "topic": "pizza" },
        "modalities": [ "text" ],

        # Create a custom input array for this request with whatever 
        # context is appropriate
        "input": [
            # potentially include existing conversation items:
            {
                "type": "item_reference",
                "id": "some_conversation_item_id"
            },

            # include new content as well
            {
                "type": "message",
                "role": "user",
                "content": [
                    {
                        "type": "input_text",
                        "text": "Is it okay to put pineapple on pizza?",
                    }
                ],
            }
        ],
    },
}

ws.send(json.dumps(event))
```

### Create responses with no context

You can also insert responses into the default conversation, ignoring all other instructions and context. Do this by setting `input` to an empty array.

Insert no-context model responses into the default conversation

```javascript
const prompt = `
Say exactly the following:
I'm a little teapot, short and stout! 
This is my handle, this is my spout!
`;

const event = {
  type: "response.create",
  response: {
    // An empty input array removes existing context
    input: [],
    instructions: prompt,
  },
};

// WebRTC data channel and WebSocket both have .send()
dataChannel.send(JSON.stringify(event));
```

```python
prompt = """
Say exactly the following:
I'm a little teapot, short and stout! 
This is my handle, this is my spout!
"""

event = {
    "type": "response.create",
    "response": {
        # An empty input array removes all prior context
        "input": [],
        "instructions": prompt,
    },
}

ws.send(json.dumps(event))
```

Function calling
----------------

The Realtime models also support **function calling**, which enables you to execute custom code to extend the capabilities of the model. Here's how it works at a high level:

1.  When [updating the session](/docs/api-reference/realtime-client-events/session/update) or [creating a response](/docs/api-reference/realtime-client-events/response/create), you can specify a list of available functions for the model to call.
2.  If when processing input, the model determines it should make a function call, it will add items to the conversation representing arguments to a function call.
3.  When the client detects conversation items that contain function call arguments, it will execute custom code using those arguments
4.  When the custom code has been executed, the client will create new conversation items that contain the output of the function call, and ask the model to respond.

Let's see how this would work in practice by adding a callable function that will provide today's horoscope to users of the model. We'll show the shape of the client event objects that need to be sent, and what the server will emit in turn.

### Configure callable functions

First, we must give the model a selection of functions it can call based on user input. Available functions can be configured either at the session level, or the individual response level.

*   Session: `session.tools` property in [`session.update`](/docs/api-reference/realtime-client-events/session/update)
*   Response: `response.tools` property in [`response.create`](/docs/api-reference/realtime-client-events/response/create)

Here's an example client event payload for a `session.update` that configures a horoscope generation function, that takes a single argument (the astrological sign for which the horoscope should be generated):

[`session.update`](/docs/api-reference/realtime-client-events/session/update)

```json
{
  "type": "session.update",
  "session": {
    "tools": [
      {
        "type": "function",
        "name": "generate_horoscope",
        "description": "Give today's horoscope for an astrological sign.",
        "parameters": {
          "type": "object",
          "properties": {
            "sign": {
              "type": "string",
              "description": "The sign for the horoscope.",
              "enum": [
                "Aries",
                "Taurus",
                "Gemini",
                "Cancer",
                "Leo",
                "Virgo",
                "Libra",
                "Scorpio",
                "Sagittarius",
                "Capricorn",
                "Aquarius",
                "Pisces"
              ]
            }
          },
          "required": ["sign"]
        }
      }
    ],
    "tool_choice": "auto",
  }
}
```

The `description` fields for the function and the parameters help the model choose whether or not to call the function, and what data to include in each parameter. If the model receives input that indicates the user wants their horoscope, it will call this function with a `sign` parameter.

### Detect when the model wants to call a function

Based on inputs to the model, the model may decide to call a function in order to generate the best response. Let's say our application adds the following conversation item and attempts to generate a response:

[`conversation.item.create`](/docs/api-reference/realtime-client-events/conversation/item/create)

```json
{
  "type": "conversation.item.create",
  "item": {
    "type": "message",
    "role": "user",
    "content": [
      {
        "type": "input_text",
        "text": "What is my horoscope? I am an aquarius."
      }
    ]
  }
}
```

Followed by a client event to generate a response:

[`response.create`](/docs/api-reference/realtime-client-events/response/create)

```json
{
  "type": "response.create"
}
```

Instead of immediately returning a text or audio response, the model will instead generate a response that contains the arguments that should be passed to a function in the developer's application. You can listen for realtime updates to function call arguments using the [`response.function_call_arguments.delta`](/docs/api-reference/realtime-server-events/response/function_call_arguments/delta) server event, but `response.done` will also have the complete data we need to call our function.

[`response.done`](/docs/api-reference/realtime-server-events/response/done)

```json
{
  "type": "response.done",
  "event_id": "event_AeqLA8iR6FK20L4XZs2P6",
  "response": {
    "object": "realtime.response",
    "id": "resp_AeqL8XwMUOri9OhcQJIu9",
    "status": "completed",
    "status_details": null,
    "output": [
      {
        "object": "realtime.item",
        "id": "item_AeqL8gmRWDn9bIsUM2T35",
        "type": "function_call",
        "status": "completed",
        "name": "generate_horoscope",
        "call_id": "call_sHlR7iaFwQ2YQOqm",
        "arguments": "{\"sign\":\"Aquarius\"}"
      }
    ],
    "usage": {
      "total_tokens": 541,
      "input_tokens": 521,
      "output_tokens": 20,
      "input_token_details": {
        "text_tokens": 292,
        "audio_tokens": 229,
        "cached_tokens": 0,
        "cached_tokens_details": { "text_tokens": 0, "audio_tokens": 0 }
      },
      "output_token_details": {
        "text_tokens": 20,
        "audio_tokens": 0
      }
    },
    "metadata": null
  }
}
```

In the JSON emitted by the server, we can detect that the model wants to call a custom function:

|Property|Function calling purpose|
|---|---|
|response.output[0].type|When set to function_call, indicates this response contains arguments for a named function call.|
|response.output[0].name|The name of the configured function to call, in this case generate_horoscope|
|response.output[0].arguments|A JSON string containing arguments to the function. In our case, "{\"sign\":\"Aquarius\"}".|
|response.output[0].call_id|A system-generated ID for this function call - you will need this ID to pass a function call result back to the model.|

Given this information, we can execute code in our application to generate the horoscope, and then provide that information back to the model so it can generate a response.

### Provide the results of a function call to the model

Upon receiving a response from the model with arguments to a function call, your application can execute code that satisfies the function call. This could be anything you want, like talking to external APIs or accessing databases.

Once you are ready to give the model the results of your custom code, you can create a new conversation item containing the result via the `conversation.item.create` client event.

[`conversation.item.create`](/docs/api-reference/realtime-client-events/conversation/item/create)

```json
{
  "type": "conversation.item.create",
  "item": {
    "type": "function_call_output",
    "call_id": "call_sHlR7iaFwQ2YQOqm",
    "output": "{\"horoscope\": \"You will soon meet a new friend.\"}"
  }
}
```

*   The conversation item type is `function_call_output`
*   `item.call_id` is the same ID we got back in the `response.done` event above
*   `item.output` is a JSON string containing the results of our function call

Once we have added the conversation item containing our function call results, we again emit the `response.create` event from the client. This will trigger a model response using the data from the function call.

[`response.create`](/docs/api-reference/realtime-client-events/response/create)

```json
{
  "type": "response.create"
}
```

Error handling
--------------

The [`error`](/docs/api-reference/realtime-server-events/error) event is emitted by the server whenever an error condition is encountered on the server during the session. Occasionally, these errors can be traced to a client event that was emitted by your application.

Unlike HTTP requests and responses, where a response is implicitly tied to a request from the client, we need to use an `event_id` property on client events to know when one of them has triggered an error condition on the server. This technique is shown in the code below, where the client attempts to emit an unsupported event type.

```javascript
const event = {
  event_id: "my_awesome_event",
  type: "scooby.dooby.doo",
};

dataChannel.send(JSON.stringify(event));
```

This unsuccessful event sent from the client will emit an error event like the following:

```json
{
  "type": "invalid_request_error",
  "code": "invalid_value",
  "message": "Invalid value: 'scooby.dooby.doo' ...",
  "param": "type",
  "event_id": "my_awesome_event"
}
```

Was this page useful?
Realtime transcription

Beta

==============================

Learn how to transcribe audio in real-time with the Realtime API.

You can use the Realtime API for transcription-only use cases, either with input from a microphone or from a file. For example, you can use it to generate subtitles or transcripts in real-time. With the transcription-only mode, the model will not generate responses.

If you want the model to produce responses, you can use the Realtime API in [speech-to-speech conversation mode](/docs/guides/realtime-conversations).

Realtime transcription sessions
-------------------------------

To use the Realtime API for transcription, you need to create a transcription session, connecting via [WebSockets](/docs/guides/realtime?use-case=transcription#connect-with-websockets) or [WebRTC](/docs/guides/realtime?use-case=transcription#connect-with-webrtc).

Unlike the regular Realtime API sessions for conversations, the transcription sessions typically don't contain responses from the model.

The transcription session object is also different from regular Realtime API sessions:

```json
{
  object: "realtime.transcription_session",
  id: string,
  input_audio_format: string,
  input_audio_transcription: [{
    model: string,
    prompt: string,
    language: string
  }],
  turn_detection: {
    type: "server_vad",
    threshold: float,
    prefix_padding_ms: integer,
    silence_duration_ms: integer,
  } | null,
  input_audio_noise_reduction: {
    type: "near_field" | "far_field"
  },
  include: list[string] | null
}
```

Some of the additional properties transcription sessions support are:

*   `input_audio_transcription.model`: The transcription model to use, currently `gpt-4o-transcribe`, `gpt-4o-mini-transcribe`, and `whisper-1` are supported
*   `input_audio_transcription.prompt`: The prompt to use for the transcription, to guide the model (e.g. "Expect words related to technology")
*   `input_audio_transcription.language`: The language to use for the transcription, ideally in ISO-639-1 format (e.g. "en", "fr"...) to improve accuracy and latency
*   `input_audio_noise_reduction`: The noise reduction configuration to use for the transcription
*   `include`: The list of properties to include in the transcription events

Possible values for the input audio format are: `pcm16` (default), `g711_ulaw` and `g711_alaw`.

You can find more information about the transcription session object in the [API reference](/docs/api-reference/realtime-sessions/transcription_session_object).

Handling transcriptions
-----------------------

When using the Realtime API for transcription, you can listen for the `conversation.item.input_audio_transcription.delta` and `conversation.item.input_audio_transcription.completed` events.

For `whisper-1` the `delta` event will contain full turn transcript, same as `completed` event. For `gpt-4o-transcribe` and `gpt-4o-mini-transcribe` the `delta` event will contain incremental transcripts as they are streamed out from the model.

Here is an example transcription delta event:

```json
{
  "event_id": "event_2122",
  "type": "conversation.item.input_audio_transcription.delta",
  "item_id": "item_003",
  "content_index": 0,
  "delta": "Hello,"
}
```

Here is an example transcription completion event:

```json
{
  "event_id": "event_2122",
  "type": "conversation.item.input_audio_transcription.completed",
  "item_id": "item_003",
  "content_index": 0,
  "transcript": "Hello, how are you?"
}
```

Note that ordering between completion events from different speech turns is not guaranteed. You should use `item_id` to match these events to the `input_audio_buffer.committed` events and use `input_audio_buffer.committed.previous_item_id` to handle the ordering.

To send audio data to the transcription session, you can use the `input_audio_buffer.append` event.

You have 2 options:

*   Use a streaming microphone input
*   Stream data from a wav file

Voice activity detection
------------------------

The Realtime API supports automatic voice activity detection (VAD). Enabled by default, VAD will control when the input audio buffer is committed, therefore when transcription begins.

Read more about configuring VAD in our [Voice Activity Detection](/docs/guides/realtime-vad) guide.

You can also disable VAD by setting the `turn_detection` property to `null`, and control when to commit the input audio on your end.

Additional configurations
-------------------------

### Noise reduction

You can use the `input_audio_noise_reduction` property to configure how to handle noise reduction in the audio stream.

The possible values are:

*   `near_field`: Use near-field noise reduction.
*   `far_field`: Use far-field noise reduction.
*   `null`: Disable noise reduction.

The default value is `near_field`, and you can disable noise reduction by setting the property to `null`.

### Using logprobs

You can use the `include` property to include logprobs in the transcription events, using `item.input_audio_transcription.logprobs`.

Those logprobs can be used to calculate the confidence score of the transcription.

```json
{
  "type": "transcription_session.update",
  "input_audio_format": "pcm16",
  "input_audio_transcription": {
    "model": "gpt-4o-transcribe",
    "prompt": "",
    "language": ""
  },
  "turn_detection": {
    "type": "server_vad",
    "threshold": 0.5,
    "prefix_padding_ms": 300,
    "silence_duration_ms": 500,
  },
  "input_audio_noise_reduction": {
    "type": "near_field"
  },
  "include": [ 
    "item.input_audio_transcription.logprobs",
  ],
}
```

Was this page useful?
Voice activity detection (VAD)

Beta

======================================

Learn about automatic voice activity detection in the Realtime API.

Voice activity detection (VAD) is a feature available in the Realtime API allowing to automatically detect when the user has started or stopped speaking. It is enabled by default in [speech-to-speech](/docs/guides/realtime-conversations) or [transcription](/docs/guides/realtime-transcription) Realtime sessions, but is optional and can be turned off.

Overview
--------

When VAD is enabled, the audio is chunked automatically and the Realtime API sends events to indicate when the user has started or stopped speaking:

*   `input_audio_buffer.speech_started`: The start of a speech turn
*   `input_audio_buffer.speech_stopped`: The end of a speech turn

You can use these events to handle speech turns in your application. For example, you can use them to manage conversation state or process transcripts in chunks.

You can use the `turn_detection` property of the `session.update` event to configure how audio is chunked within each speech-to-text sample.

There are two modes for VAD:

*   `server_vad`: Automatically chunks the audio based on periods of silence.
*   `semantic_vad`: Chunks the audio when the model believes based on the words said by the user that they have completed their utterance.

The default value is `server_vad`.

Read below to learn more about the different modes.

Server VAD
----------

Server VAD is the default mode for Realtime sessions, and uses periods of silence to automatically chunk the audio.

You can adjust the following properties to fine-tune the VAD settings:

*   `threshold`: Activation threshold (0 to 1). A higher threshold will require louder audio to activate the model, and thus might perform better in noisy environments.
*   `prefix_padding_ms`: Amount of audio (in milliseconds) to include before the VAD detected speech.
*   `silence_duration_ms`: Duration of silence (in milliseconds) to detect speech stop. With shorter values turns will be detected more quickly.

Here is an example VAD configuration:

```json
{
  "type": "session.update",
  "session": {
    "turn_detection": {
      "type": "server_vad",
      "threshold": 0.5,
      "prefix_padding_ms": 300,
      "silence_duration_ms": 500,
      "create_response": true, // only in conversation mode
      "interrupt_response": true, // only in conversation mode
    }
  }
}
```

Semantic VAD
------------

Semantic VAD is a new mode that uses a semantic classifier to detect when the user has finished speaking, based on the words they have uttered. This classifier scores the input audio based on the probability that the user is done speaking. When the probability is low, the model will wait for a timeout, whereas when it is high, there is no need to wait. For example, user audio that trails off with an "ummm..." would result in a longer timeout than a definitive statement.

With this mode, the model is less likely to interrupt the user during a speech-to-speech conversation, or chunk a transcript before the user is done speaking.

Semantic VAD can be activated by setting `turn_detection.type` to `semantic_vad` in a [`session.update`](/docs/api-reference/realtime-client-events/session/update) event.

It can be configured like this:

```json
{
  "type": "session.update",
  "session": {
    "turn_detection": {
      "type": "semantic_vad",
      "eagerness": "low" | "medium" | "high" | "auto", // optional
      "create_response": true, // only in conversation mode
      "interrupt_response": true, // only in conversation mode
    }
  }
}
```

The optional `eagerness` property is a way to control how eager the model is to interrupt the user, tuning the maximum wait timeout. In transcription mode, even if the model doesn't reply, it affects how the audio is chunked.

*   `auto` is the default value, and is equivalent to `medium`.
*   `low` will let the user take their time to speak.
*   `high` will chunk the audio as soon as possible.

If you want the model to respond more often in conversation mode, or to return transcription events faster in transcription mode, you can set `eagerness` to `high`.

On the other hand, if you want to let the user speak uninterrupted in conversation mode, or if you would like larger transcript chunks in transcription mode, you can set `eagerness` to `low`.

Was this page useful?
Image generation
================

Learn how to generate or manipulate images with DALL·E.

Introduction
------------

The [Image generation API](/docs/api-reference/images) has three endpoints with different abilities:

*   **Generations**: Images from scratch, based on a text prompt
*   **Edits**: Edited versions of images, where the model replaces some areas of a pre-existing image, based on a new text prompt
*   **Variations**: Variations of an existing image

This guide covers the basics of using these endpoints with code samples. To try DALL·E 3 without writing any code, go to [ChatGPT](https://chatgpt.com/).

Which model should I use?
-------------------------

DALL·E 2 and DALL·E 3 have different options for generating images.

||
|DALL·E 2|Generations, edits, variations|More options (edits and variations), more control in prompting, more requests at once|
|DALL·E 3|Only image generations|Higher quality, larger sizes for generated images|

Generations
-----------

The [image generations](/docs/api-reference/images/create) endpoint allows you to create an original image with a text prompt. Each image can be returned either as a URL or Base64 data, using the [response\_format](/docs/api-reference/images/create#images/create-response_format) parameter. The default output is URL, and each URL expires after an hour.

### Size and quality options

Square, standard quality images are the fastest to generate. The default size of generated images is `1024x1024` pixels, but each model has different options:

||
|DALL·E 2|256x256512x5121024x1024|Only standard|Up to 10 images at a time, with the n parameter|
|DALL·E 3|1024x10241024x17921792x1024|Defaults to standardSet quality: "hd" for enhanced detail|Only 1 at a time, but can request more by making parallel requests|

The following code example uses DALL·E 3 to generate a square, standard quality image of a cat.

Generate an image

```javascript
import OpenAI from "openai";
const openai = new OpenAI();

const response = await openai.images.generate({
  model: "dall-e-3",
  prompt: "a white siamese cat",
  n: 1,
  size: "1024x1024",
});

console.log(response.data[0].url);
```

```python
from openai import OpenAI
client = OpenAI()

response = client.images.generate(
    model="dall-e-3",
    prompt="a white siamese cat",
    size="1024x1024",
    quality="standard",
    n=1,
)

print(response.data[0].url)
```

```bash
curl https://api.openai.com/v1/images/generations \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "dall-e-3",
    "prompt": "a white siamese cat",
    "n": 1,
    "size": "1024x1024"
  }'
```

### DALL·E 3 prompting

With the release of DALL·E 3, the model takes in your prompt and automatically rewrites it:

*   For safety reasons
*   To add more detail (more detailed prompts generally result in higher quality images)

You can't disable this feature, but you can get outputs closer to your requested image by adding the following to your prompt:

`I NEED to test how the tool works with extremely simple prompts. DO NOT add any detail, just use it AS-IS:`

The updated prompt is visible in the `revised_prompt` field of the data response object.

[

What's new with DALL·E 3

Explore what's new with DALL·E 3 in the OpenAI Cookbook

](https://cookbook.openai.com/articles/what_is_new_with_dalle_3)

Edits (DALL·E 2 only)
---------------------

The [image edits](/docs/api-reference/images/create-edit) endpoint lets you edit or extend an image by uploading an image and mask indicating which areas should be replaced. This process is also known as **inpainting**.

The transparent areas of the mask indicate where the image should be edited, and the prompt should describe the full new image, **not just the erased area**. This endpoint enables experiences like DALL·E image editing in ChatGPT Plus.

Edit an image

```javascript
import OpenAI from "openai";
const openai = new OpenAI();

const response = await openai.images.generate({
  model: "dall-e-3",
  prompt: "a white siamese cat",
  n: 1,
  size: "1024x1024",
});

console.log(response.data[0].url);
```

```python
from openai import OpenAI
client = OpenAI()

response = client.images.edit(
    model="dall-e-2",
    image=open("sunlit_lounge.png", "rb"),
    mask=open("mask.png", "rb"),
    prompt="A sunlit indoor lounge area with a pool containing a flamingo",
    n=1,
    size="1024x1024",
)

print(response.data[0].url)
```

```bash
curl https://api.openai.com/v1/images/edits \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -F model="dall-e-2" \
  -F image="@sunlit_lounge.png" \
  -F mask="@mask.png" \
  -F prompt="A sunlit indoor lounge area with a pool containing a flamingo" \
  -F n=1 \
  -F size="1024x1024"
```

|Image|Mask|Output|
|---|---|---|
||||

Prompt: a sunlit indoor lounge area with a pool containing a flamingo

The uploaded image and mask must both be square PNG images, less than 4MB in size, and have the same dimensions as each other. The non-transparent areas of the mask aren't used to generate the output, so they don’t need to match the original image like our example.

Variations (DALL·E 2 only)
--------------------------

The [image variations](/docs/api-reference/images/create-variation) endpoint allows you to generate a variation of a given image.

Generate an image variation

```javascript
import OpenAI from "openai";
const openai = new OpenAI();

const response = await openai.images.createVariation({
  model: "dall-e-2",
  image: fs.createReadStream("corgi_and_cat_paw.png"),
  n: 1,
  size: "1024x1024"
});

console.log(response.data[0].url);
```

```python
from openai import OpenAI
client = OpenAI()

response = client.images.create_variation(
    model="dall-e-2",
    image=open("corgi_and_cat_paw.png", "rb"),
    n=1,
    size="1024x1024"
)

print(response.data[0].url)
```

```bash
curl https://api.openai.com/v1/images/variations \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -F model="dall-e-2" \
  -F image="@corgi_and_cat_paw.png" \
  -F n=1 \
  -F size="1024x1024"
```

|Image|Output|
|---|---|
|||

Similar to the edits endpoint, the input image must be a square PNG image less than 4MB in size.

### Content moderation

Prompts and images are filtered based on our [content policy](https://labs.openai.com/policies/content-policy), returning an error when a prompt or image is flagged.

Language-specific tips
----------------------

Node.js

### Using in-memory image data

The Node.js examples in the guide above use the `fs` module to read image data from disk. In some cases, you may have your image data in memory instead. Here's an example API call that uses image data stored in a Node.js `Buffer` object:

```javascript
import OpenAI from "openai";

const openai = new OpenAI();

// This is the Buffer object that contains your image data
const buffer = [your image data];

// Set a `name` that ends with .png so that the API knows it's a PNG image
buffer.name = "image.png";

async function main() {
  const image = await openai.images.createVariation({ model: "dall-e-2", image: buffer, n: 1, size: "1024x1024" });
  console.log(image.data);
}
main();
```

### Working with TypeScript

If you're using TypeScript, you may encounter some quirks with image file arguments. Here's an example of working around the type mismatch by explicitly casting the argument:

```javascript
import fs from "fs";
import OpenAI from "openai";

const openai = new OpenAI();

async function main() {
  // Cast the ReadStream to `any` to appease the TypeScript compiler
  const image = await openai.images.createVariation({
    image: fs.createReadStream("image.png") as any,
  });

  console.log(image.data);
}
main();
```

And here's a similar example for in-memory image data:

```javascript
import fs from "fs";
import OpenAI from "openai";

const openai = new OpenAI();

// This is the Buffer object that contains your image data
const buffer: Buffer = [your image data];

// Cast the buffer to `any` so that we can set the `name` property
const file: any = buffer;

// Set a `name` that ends with .png so that the API knows it's a PNG image
file.name = "image.png";

async function main() {
  const image = await openai.images.createVariation({
    file,
    1,
    "1024x1024"
  });
  console.log(image.data);
}
main();
```

### Error handling

API requests can potentially return errors due to invalid inputs, rate limits, or other issues. These errors can be handled with a `try...catch` statement, and the error details can be found in either `error.response` or `error.message`:

```javascript
import fs from "fs";
import OpenAI from "openai";

const openai = new OpenAI();

async function main() {
    try {
        const image = await openai.images.createVariation({
            image: fs.createReadStream("image.png"),
            n: 1,
            size: "1024x1024",
        });
        console.log(image.data);
    } catch (error) {
        if (error.response) {
            console.log(error.response.status);
            console.log(error.response.data);
        } else {
            console.log(error.message);
        }
    }
}

main();
```

Python

### Using in-memory image data

The Python examples in the guide above use the `open` function to read image data from disk. In some cases, you may have your image data in memory instead. Here's an example API call that uses image data stored in a `BytesIO` object:

```python
from io import BytesIO
from openai import OpenAI
client = OpenAI()

# This is the BytesIO object that contains your image data
byte_stream: BytesIO = [your image data]
byte_array = byte_stream.getvalue()
response = client.images.create_variation(
    model="dall-e-2",
    image=byte_array,
    n=1,
    size="1024x1024",
)
```

### Operating on image data

It may be useful to perform operations on images before passing them to the API. Here's an example that uses `PIL` to resize an image:

```python
from io import BytesIO
from PIL import Image
from openai import OpenAI
client = OpenAI()

# Read the image file from disk and resize it
image = Image.open("image.png")
width, height = 256, 256
image = image.resize((width, height))

# Convert the image to a BytesIO object
byte_stream = BytesIO()
image.save(byte_stream, format='PNG')
byte_array = byte_stream.getvalue()

response = client.images.create_variation(
    model="dall-e-2",
    image=byte_array,
    n=1,
    size="1024x1024",
)
```

### Error handling

API requests can potentially return errors due to invalid inputs, rate limits, or other issues. These errors can be handled with a `try...except` statement, and the error details can be found in `e.error`:

```python
import openai
from openai import OpenAI
client = OpenAI()

try:
    response = client.images.create_variation(
        model="dall-e-2",
        image=open("image_edit_mask.png", "rb"),
        n=1,
        size="1024x1024",
    )
    print(response.data[0].url)
except openai.OpenAIError as e:
    print(e.http_status)
    print(e.error)
```

Was this page useful?
Text to speech
==============

Learn how to turn text into lifelike spoken audio.

The Audio API provides a [`speech`](/docs/api-reference/audio/createSpeech) endpoint based on our [GPT-4o mini TTS (text-to-speech) model](/docs/models/gpt-4o-mini-tts). It comes with 11 built-in voices and can be used to:

*   Narrate a written blog post
*   Produce spoken audio in multiple languages
*   Give realtime audio output using streaming

Here's an example of the `alloy` voice:

Our [usage policies](https://openai.com/policies/usage-policies) require you to provide a clear disclosure to end users that the TTS voice they are hearing is AI-generated and not a human voice.

Quickstart
----------

The `speech` endpoint takes three key inputs:

1.  The [model](/docs/api-reference/audio/createSpeech#audio-createspeech-model) you're using
2.  The [text](/docs/api-reference/audio/createSpeech#audio-createspeech-input) to be turned into audio
3.  The [voice](/docs/api-reference/audio/createSpeech#audio-createspeech-voice) that will speak the output

Here's a simple request example:

Generate spoken audio from input text

```javascript
import fs from "fs";
import path from "path";
import OpenAI from "openai";

const openai = new OpenAI();
const speechFile = path.resolve("./speech.mp3");

const mp3 = await openai.audio.speech.create({
  model: "gpt-4o-mini-tts",
  voice: "coral",
  input: "Today is a wonderful day to build something people love!",
  instructions: "Speak in a cheerful and positive tone.",
});

const buffer = Buffer.from(await mp3.arrayBuffer());
await fs.promises.writeFile(speechFile, buffer);
```

```python
from pathlib import Path
from openai import OpenAI

client = OpenAI()
speech_file_path = Path(__file__).parent / "speech.mp3"

with client.audio.speech.with_streaming_response.create(
    model="gpt-4o-mini-tts",
    voice="coral",
    input="Today is a wonderful day to build something people love!",
    instructions="Speak in a cheerful and positive tone.",
) as response:
    response.stream_to_file(speech_file_path)
```

```bash
curl https://api.openai.com/v1/audio/speech \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-4o-mini-tts",
    "input": "Today is a wonderful day to build something people love!",
    "voice": "coral",
    "instructions": "Speak in a cheerful and positive tone."
  }' \
  --output speech.mp3
```

By default, the endpoint outputs an MP3 of the spoken audio, but you can configure it to output any [supported format](#supported-output-formats).

### Text-to-speech models

For intelligent realtime applications, use the `gpt-4o-mini-tts` model, our newest and most reliable text-to-speech model. You can prompt the model to control aspects of speech, including:

*   Accent
*   Emotional range
*   Intonation
*   Impressions
*   Speed of speech
*   Tone
*   Whispering

Our other text-to-speech models are `tts-1` and `tts-1-hd`. The `tts-1` model provides lower latency, but at a lower quality than the `tts-1-hd` model.

### Voice options

The TTS endpoint provides 11 built‑in voices to control how speech is rendered from text. **Hear and play with these voices in [OpenAI.fm](https://openai.fm), our interactive demo for trying the latest text-to-speech model in the OpenAI API**. Voices are currently optimized for English.

*   `alloy`
*   `ash`
*   `ballad`
*   `coral`
*   `echo`
*   `fable`
*   `onyx`
*   `nova`
*   `sage`
*   `shimmer`

If you're using the [Realtime API](/docs/guides/realtime), note that the set of available voices is slightly different—see the [realtime model capabilities guide](/docs/guides/realtime-model-capabilities#voice-options) for current realtime voices.

### Streaming realtime audio

The Speech API provides support for realtime audio streaming using [chunk transfer encoding](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Transfer-Encoding). This means the audio can be played before the full file is generated and made accessible.

Stream spoken audio from input text directly to your speakers

```javascript
import OpenAI from "openai";
import { playAudio } from "openai/helpers/audio";

const openai = new OpenAI();

const response = await openai.audio.speech.create({
  model: "gpt-4o-mini-tts",
  voice: "coral",
  input: "Today is a wonderful day to build something people love!",
  instructions: "Speak in a cheerful and positive tone.",
  response_format: "wav",
});

await playAudio(response);
```

```python
import asyncio

from openai import AsyncOpenAI
from openai.helpers import LocalAudioPlayer

openai = AsyncOpenAI()

async def main() -> None:
    async with openai.audio.speech.with_streaming_response.create(
        model="gpt-4o-mini-tts",
        voice="coral",
        input="Today is a wonderful day to build something people love!",
        instructions="Speak in a cheerful and positive tone.",
        response_format="pcm",
    ) as response:
        await LocalAudioPlayer().play(response)

if __name__ == "__main__":
    asyncio.run(main())
```

```bash
curl https://api.openai.com/v1/audio/speech \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-4o-mini-tts",
    "input": "Today is a wonderful day to build something people love!",
    "voice": "coral",
    "instructions": "Speak in a cheerful and positive tone.",
    "response_format": "wav"
  }' | ffplay -i -
```

For the fastest response times, we recommend using `wav` or `pcm` as the response format.

Supported output formats
------------------------

The default response format is `mp3`, but other formats like `opus` and `wav` are available.

*   **MP3**: The default response format for general use cases.
*   **Opus**: For internet streaming and communication, low latency.
*   **AAC**: For digital audio compression, preferred by YouTube, Android, iOS.
*   **FLAC**: For lossless audio compression, favored by audio enthusiasts for archiving.
*   **WAV**: Uncompressed WAV audio, suitable for low-latency applications to avoid decoding overhead.
*   **PCM**: Similar to WAV but contains the raw samples in 24kHz (16-bit signed, low-endian), without the header.

Supported languages
-------------------

The TTS model generally follows the Whisper model in terms of language support. Whisper [supports the following languages](https://github.com/openai/whisper#available-models-and-languages) and performs well, despite voices being optimized for English:

Afrikaans, Arabic, Armenian, Azerbaijani, Belarusian, Bosnian, Bulgarian, Catalan, Chinese, Croatian, Czech, Danish, Dutch, English, Estonian, Finnish, French, Galician, German, Greek, Hebrew, Hindi, Hungarian, Icelandic, Indonesian, Italian, Japanese, Kannada, Kazakh, Korean, Latvian, Lithuanian, Macedonian, Malay, Marathi, Maori, Nepali, Norwegian, Persian, Polish, Portuguese, Romanian, Russian, Serbian, Slovak, Slovenian, Spanish, Swahili, Swedish, Tagalog, Tamil, Thai, Turkish, Ukrainian, Urdu, Vietnamese, and Welsh.

You can generate spoken audio in these languages by providing input text in the language of your choice.

Customization and ownership
---------------------------

### Custom voices

We do not support custom voices or creating a copy of your own voice.

### Who owns the output?

As with all outputs from our API, the person who created them owns the output. You are still required to inform end users that they are hearing audio generated by AI and not a real person talking to them.

Was this page useful?
Speech to text
==============

Learn how to turn audio into text.

The Audio API provides two speech to text endpoints:

*   `transcriptions`
*   `translations`

Historically, both endpoints have been backed by our open source [Whisper model](https://openai.com/blog/whisper/) (`whisper-1`). The `transcriptions` endpoint now also supports higher quality model snapshots, with limited parameter support:

*   `gpt-4o-mini-transcribe`
*   `gpt-4o-transcribe`

All endpoints can be used to:

*   Transcribe audio into whatever language the audio is in.
*   Translate and transcribe the audio into English.

File uploads are currently limited to 25 MB, and the following input file types are supported: `mp3`, `mp4`, `mpeg`, `mpga`, `m4a`, `wav`, and `webm`.

Quickstart
----------

### Transcriptions

The transcriptions API takes as input the audio file you want to transcribe and the desired output file format for the transcription of the audio. All models support the same set of input formats. On output, `whisper-1` supports a range of formats (`json`, `text`, `srt`, `verbose_json`, `vtt`); the newer `gpt-4o-mini-transcribe` and `gpt-4o-transcribe` snapshots currently only support `json` or plain `text` responses.

Transcribe audio

```javascript
import fs from "fs";
import OpenAI from "openai";

const openai = new OpenAI();

const transcription = await openai.audio.transcriptions.create({
  file: fs.createReadStream("/path/to/file/audio.mp3"),
  model: "gpt-4o-transcribe",
});

console.log(transcription.text);
```

```python
from openai import OpenAI

client = OpenAI()
audio_file= open("/path/to/file/audio.mp3", "rb")

transcription = client.audio.transcriptions.create(
    model="gpt-4o-transcribe", 
    file=audio_file
)

print(transcription.text)
```

```bash
curl --request POST \
  --url https://api.openai.com/v1/audio/transcriptions \
  --header "Authorization: Bearer $OPENAI_API_KEY" \
  --header 'Content-Type: multipart/form-data' \
  --form file=@/path/to/file/audio.mp3 \
  --form model=gpt-4o-transcribe
```

By default, the response type will be json with the raw text included.

{ "text": "Imagine the wildest idea that you've ever had, and you're curious about how it might scale to something that's a 100, a 1,000 times bigger. .... }

The Audio API also allows you to set additional parameters in a request. For example, if you want to set the `response_format` as `text`, your request would look like the following:

Additional options

```javascript
import fs from "fs";
import OpenAI from "openai";

const openai = new OpenAI();

const transcription = await openai.audio.transcriptions.create({
  file: fs.createReadStream("/path/to/file/speech.mp3"),
  model: "gpt-4o-transcribe",
  response_format: "text",
});

console.log(transcription.text);
```

```python
from openai import OpenAI

client = OpenAI()
audio_file = open("/path/to/file/speech.mp3", "rb")

transcription = client.audio.transcriptions.create(
    model="gpt-4o-transcribe", 
    file=audio_file, 
    response_format="text"
)

print(transcription.text)
```

```bash
curl --request POST \
  --url https://api.openai.com/v1/audio/transcriptions \
  --header "Authorization: Bearer $OPENAI_API_KEY" \
  --header 'Content-Type: multipart/form-data' \
  --form file=@/path/to/file/speech.mp3 \
  --form model=gpt-4o-transcribe \
  --form response_format=text
```

The [API Reference](/docs/api-reference/audio) includes the full list of available parameters.

The newer `gpt-4o-mini-transcribe` and `gpt-4o-transcribe` models currently have a limited parameter surface: they only support `json` or `text` response formats. Other parameters, such as `timestamp_granularities`, require `verbose_json` output and are therefore only available when using `whisper-1`.

### Translations

The translations API takes as input the audio file in any of the supported languages and transcribes, if necessary, the audio into English. This differs from our /Transcriptions endpoint since the output is not in the original input language and is instead translated to English text. This endpoint supports only the `whisper-1` model.

Translate audio

```javascript
import fs from "fs";
import OpenAI from "openai";

const openai = new OpenAI();

const translation = await openai.audio.translations.create({
  file: fs.createReadStream("/path/to/file/german.mp3"),
  model: "whisper-1",
});

console.log(translation.text);
```

```python
from openai import OpenAI

client = OpenAI()
audio_file = open("/path/to/file/german.mp3", "rb")

translation = client.audio.translations.create(
    model="whisper-1", 
    file=audio_file,
)

print(translation.text)
```

```bash
curl --request POST \
  --url https://api.openai.com/v1/audio/translations \
  --header "Authorization: Bearer $OPENAI_API_KEY" \
  --header 'Content-Type: multipart/form-data' \
  --form file=@/path/to/file/german.mp3 \
  --form model=whisper-1 \
```

In this case, the inputted audio was german and the outputted text looks like:

Hello, my name is Wolfgang and I come from Germany. Where are you heading today?

We only support translation into English at this time.

Supported languages
-------------------

We currently [support the following languages](https://github.com/openai/whisper#available-models-and-languages) through both the `transcriptions` and `translations` endpoint:

Afrikaans, Arabic, Armenian, Azerbaijani, Belarusian, Bosnian, Bulgarian, Catalan, Chinese, Croatian, Czech, Danish, Dutch, English, Estonian, Finnish, French, Galician, German, Greek, Hebrew, Hindi, Hungarian, Icelandic, Indonesian, Italian, Japanese, Kannada, Kazakh, Korean, Latvian, Lithuanian, Macedonian, Malay, Marathi, Maori, Nepali, Norwegian, Persian, Polish, Portuguese, Romanian, Russian, Serbian, Slovak, Slovenian, Spanish, Swahili, Swedish, Tagalog, Tamil, Thai, Turkish, Ukrainian, Urdu, Vietnamese, and Welsh.

While the underlying model was trained on 98 languages, we only list the languages that exceeded <50% [word error rate](https://en.wikipedia.org/wiki/Word_error_rate) (WER) which is an industry standard benchmark for speech to text model accuracy. The model will return results for languages not listed above but the quality will be low.

We support some ISO 639-1 and 639-3 language codes for GPT-4o based models. For language codes we don’t have, try prompting for specific languages (i.e., “Output in English”).

Timestamps
----------

By default, the Transcriptions API will output a transcript of the provided audio in text. The [`timestamp_granularities[]` parameter](/docs/api-reference/audio/createTranscription#audio-createtranscription-timestamp_granularities) enables a more structured and timestamped json output format, with timestamps at the segment, word level, or both. This enables word-level precision for transcripts and video edits, which allows for the removal of specific frames tied to individual words.

Timestamp options

```javascript
import fs from "fs";
import OpenAI from "openai";

const openai = new OpenAI();

const transcription = await openai.audio.transcriptions.create({
  file: fs.createReadStream("audio.mp3"),
  model: "whisper-1",
  response_format: "verbose_json",
  timestamp_granularities: ["word"]
});

console.log(transcription.words);
```

```python
from openai import OpenAI

client = OpenAI()
audio_file = open("/path/to/file/speech.mp3", "rb")

transcription = client.audio.transcriptions.create(
  file=audio_file,
  model="whisper-1",
  response_format="verbose_json",
  timestamp_granularities=["word"]
)

print(transcription.words)
```

```bash
curl https://api.openai.com/v1/audio/transcriptions \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: multipart/form-data" \
  -F file="@/path/to/file/audio.mp3" \
  -F "timestamp_granularities[]=word" \
  -F model="whisper-1" \
  -F response_format="verbose_json"
```

The `timestamp_granularities[]` parameter is only supported for `whisper-1`.

Longer inputs
-------------

By default, the Transcriptions API only supports files that are less than 25 MB. If you have an audio file that is longer than that, you will need to break it up into chunks of 25 MB's or less or used a compressed audio format. To get the best performance, we suggest that you avoid breaking the audio up mid-sentence as this may cause some context to be lost.

One way to handle this is to use the [PyDub open source Python package](https://github.com/jiaaro/pydub) to split the audio:

```python
from pydub import AudioSegment

song = AudioSegment.from_mp3("good_morning.mp3")

# PyDub handles time in milliseconds
ten_minutes = 10 * 60 * 1000

first_10_minutes = song[:ten_minutes]

first_10_minutes.export("good_morning_10.mp3", format="mp3")
```

_OpenAI makes no guarantees about the usability or security of 3rd party software like PyDub._

Prompting
---------

You can use a [prompt](/docs/api-reference/audio/createTranscription#audio/createTranscription-prompt) to improve the quality of the transcripts generated by the Transcriptions API.

Prompting

```javascript
import fs from "fs";
import OpenAI from "openai";

const openai = new OpenAI();

const transcription = await openai.audio.transcriptions.create({
  file: fs.createReadStream("/path/to/file/speech.mp3"),
  model: "gpt-4o-transcribe",
  response_format: "text",
  prompt:"The following conversation is a lecture about the recent developments around OpenAI, GPT-4.5 and the future of AI.",
});

console.log(transcription.text);
```

```python
from openai import OpenAI

client = OpenAI()
audio_file = open("/path/to/file/speech.mp3", "rb")

transcription = client.audio.transcriptions.create(
  model="gpt-4o-transcribe", 
  file=audio_file, 
  response_format="text",
  prompt="The following conversation is a lecture about the recent developments around OpenAI, GPT-4.5 and the future of AI."
)

print(transcription.text)
```

```bash
curl --request POST \
  --url https://api.openai.com/v1/audio/transcriptions \
  --header "Authorization: Bearer $OPENAI_API_KEY" \
  --header 'Content-Type: multipart/form-data' \
  --form file=@/path/to/file/speech.mp3 \
  --form model=gpt-4o-transcribe \
  --form prompt="The following conversation is a lecture about the recent developments around OpenAI, GPT-4.5 and the future of AI."
```

For `gpt-4o-transcribe` and `gpt-4o-mini-transcribe`, you can use the `prompt` parameter to improve the quality of the transcription by giving the model additional context similarly to how you would prompt other GPT-4o models.

Here are some examples of how prompting can help in different scenarios:

1.  Prompts can help correct specific words or acronyms that the model misrecognizes in the audio. For example, the following prompt improves the transcription of the words DALL·E and GPT-3, which were previously written as "GDP 3" and "DALI": "The transcript is about OpenAI which makes technology like DALL·E, GPT-3, and ChatGPT with the hope of one day building an AGI system that benefits all of humanity."
2.  To preserve the context of a file that was split into segments, prompt the model with the transcript of the preceding segment. The model uses relevant information from the previous audio, improving transcription accuracy. The `whisper-1` model only considers the final 224 tokens of the prompt and ignores anything earlier. For multilingual inputs, Whisper uses a custom tokenizer. For English-only inputs, it uses the standard GPT-2 tokenizer. Find both tokenizers in the open source [Whisper Python package](https://github.com/openai/whisper/blob/main/whisper/tokenizer.py#L361).
3.  Sometimes the model skips punctuation in the transcript. To prevent this, use a simple prompt that includes punctuation: "Hello, welcome to my lecture."
4.  The model may also leave out common filler words in the audio. If you want to keep the filler words in your transcript, use a prompt that contains them: "Umm, let me think like, hmm... Okay, here's what I'm, like, thinking."
5.  Some languages can be written in different ways, such as simplified or traditional Chinese. The model might not always use the writing style that you want for your transcript by default. You can improve this by using a prompt in your preferred writing style.

For `whisper-1`, the model tries to match the style of the prompt, so it's more likely to use capitalization and punctuation if the prompt does too. However, the current prompting system is more limited than our other language models and provides limited control over the generated text.

You can find more examples on improving your `whisper-1` transcriptions in the [improving reliability](#improving-reliability) section.

Streaming transcriptions
------------------------

There are two ways you can stream your transcription depending on your use case and whether you are trying to transcribe an already completed audio recording or handle an ongoing stream of audio and use OpenAI for turn detection.

### Streaming the transcription of a completed audio recording

If you have an already completed audio recording, either because it's an audio file or you are using your own turn detection (like push-to-talk), you can use our Transcription API with `stream=True` to receive a stream of [transcript events](/docs/api-reference/audio/transcript-text-delta-event) as soon as the model is done transcribing that part of the audio.

Stream transcriptions

```javascript
import fs from "fs";
import OpenAI from "openai";

const openai = new OpenAI();

const stream = await openai.audio.transcriptions.create({
  file: fs.createReadStream("/path/to/file/speech.mp3"),
  model: "gpt-4o-mini-transcribe",
  response_format: "text",
  stream: true,
});

for await (const event of stream) {
  console.log(event);
}
```

```python
from openai import OpenAI

client = OpenAI()
audio_file = open("/path/to/file/speech.mp3", "rb")

stream = client.audio.transcriptions.create(
  model="gpt-4o-mini-transcribe", 
  file=audio_file, 
  response_format="text",
  stream=True
)

for event in stream:
  print(event)
```

```bash
curl --request POST \
  --url https://api.openai.com/v1/audio/transcriptions \
  --header "Authorization: Bearer $OPENAI_API_KEY" \
  --header 'Content-Type: multipart/form-data' \
  --form file=@example.wav \
  --form model=whisper-1 \
  --form stream=True
```

You will receive a stream of `transcript.text.delta` events as soon as the model is done transcribing that part of the audio, followed by a `transcript.text.done` event when the transcription is complete that includes the full transcript.

Additionally, you can use the `include[]` parameter to include `logprobs` in the response to get the log probabilities of the tokens in the transcription. These can be helpful to determine how confident the model is in the transcription of that particular part of the transcript.

Streamed transcription is not supported in `whisper-1`.

### Streaming the transcription of an ongoing audio recording

In the Realtime API, you can stream the transcription of an ongoing audio recording. To start a streaming session with the Realtime API, create a WebSocket connection with the following URL:

```text
wss://api.openai.com/v1/realtime?intent=transcription
```

Below is an example payload for setting up a transcription session:

```json
{
  "type": "transcription_session.update",
  "input_audio_format": "pcm16",
  "input_audio_transcription": {
    "model": "gpt-4o-transcribe",
    "prompt": "",
    "language": ""
  },
  "turn_detection": {
    "type": "server_vad",
    "threshold": 0.5,
    "prefix_padding_ms": 300,
    "silence_duration_ms": 500,
  },
  "input_audio_noise_reduction": {
    "type": "near_field"
  },
  "include": [
    "item.input_audio_transcription.logprobs"
  ]
}
```

To stream audio data to the API, append audio buffers:

```json
{
  "type": "input_audio_buffer.append",
  "audio": "Base64EncodedAudioData"
}
```

When in VAD mode, the API will respond with `input_audio_buffer.committed` every time a chunk of speech has been detected. Use `input_audio_buffer.committed.item_id` and `input_audio_buffer.committed.previous_item_id` to enforce the ordering.

The API responds with transcription events indicating speech start, stop, and completed transcriptions.

The primary resource used by the streaming ASR API is the `TranscriptionSession`:

```json
{
  "object": "realtime.transcription_session",
  "id": "string",
  "input_audio_format": "pcm16",
  "input_audio_transcription": [{
    "model": "whisper-1" | "gpt-4o-transcribe" | "gpt-4o-mini-transcribe",
    "prompt": "string",
    "language": "string"
  }],
  "turn_detection": {
    "type": "server_vad",
    "threshold": "float",
    "prefix_padding_ms": "integer",
    "silence_duration_ms": "integer",
  } | null,
  "input_audio_noise_reduction": {
    "type": "near_field" | "far_field"
  },
  "include": ["string"]
}
```

Authenticate directly through the WebSocket connection using your API key or an ephemeral token obtained from:

```text
POST /v1/realtime/transcription_sessions
```

This endpoint returns an ephemeral token (`client_secret`) to securely authenticate WebSocket connections.

Improving reliability
---------------------

One of the most common challenges faced when using Whisper is the model often does not recognize uncommon words or acronyms. Here are some different techniques to improve the reliability of Whisper in these cases:

Using the prompt parameter

The first method involves using the optional prompt parameter to pass a dictionary of the correct spellings.

Because it wasn't trained with instruction-following techniques, Whisper operates more like a base GPT model. Keep in mind that Whisper only considers the first 224 tokens of the prompt.

Prompt parameter

```javascript
import fs from "fs";
import OpenAI from "openai";

const openai = new OpenAI();

const transcription = await openai.audio.transcriptions.create({
  file: fs.createReadStream("/path/to/file/speech.mp3"),
  model: "whisper-1",
  response_format: "text",
  prompt:"ZyntriQix, Digique Plus, CynapseFive, VortiQore V8, EchoNix Array, OrbitalLink Seven, DigiFractal Matrix, PULSE, RAPT, B.R.I.C.K., Q.U.A.R.T.Z., F.L.I.N.T.",
});

console.log(transcription.text);
```

```python
from openai import OpenAI

client = OpenAI()
audio_file = open("/path/to/file/speech.mp3", "rb")

transcription = client.audio.transcriptions.create(
  model="whisper-1", 
  file=audio_file, 
  response_format="text",
  prompt="ZyntriQix, Digique Plus, CynapseFive, VortiQore V8, EchoNix Array, OrbitalLink Seven, DigiFractal Matrix, PULSE, RAPT, B.R.I.C.K., Q.U.A.R.T.Z., F.L.I.N.T."
)

print(transcription.text)
```

```bash
curl --request POST \
  --url https://api.openai.com/v1/audio/transcriptions \
  --header "Authorization: Bearer $OPENAI_API_KEY" \
  --header 'Content-Type: multipart/form-data' \
  --form file=@/path/to/file/speech.mp3 \
  --form model=whisper-1 \
  --form prompt="ZyntriQix, Digique Plus, CynapseFive, VortiQore V8, EchoNix Array, OrbitalLink Seven, DigiFractal Matrix, PULSE, RAPT, B.R.I.C.K., Q.U.A.R.T.Z., F.L.I.N.T."
```

While it increases reliability, this technique is limited to 224 tokens, so your list of SKUs needs to be relatively small for this to be a scalable solution.

Post-processing with GPT-4

The second method involves a post-processing step using GPT-4 or GPT-3.5-Turbo.

We start by providing instructions for GPT-4 through the `system_prompt` variable. Similar to what we did with the prompt parameter earlier, we can define our company and product names.

Post-processing

```javascript
const systemPrompt = `
You are a helpful assistant for the company ZyntriQix. Your task is 
to correct any spelling discrepancies in the transcribed text. Make 
sure that the names of the following products are spelled correctly: 
ZyntriQix, Digique Plus, CynapseFive, VortiQore V8, EchoNix Array, 
OrbitalLink Seven, DigiFractal Matrix, PULSE, RAPT, B.R.I.C.K., 
Q.U.A.R.T.Z., F.L.I.N.T. Only add necessary punctuation such as 
periods, commas, and capitalization, and use only the context provided.
`;

const transcript = await transcribe(audioFile);
const completion = await openai.chat.completions.create({
model: "gpt-4o",
temperature: temperature,
messages: [
  {
    role: "system",
    content: systemPrompt
  },
  {
    role: "user",
    content: transcript
  }
],
store: true,
});

console.log(completion.choices[0].message.content);
```

```python
system_prompt = """
You are a helpful assistant for the company ZyntriQix. Your task is to correct 
any spelling discrepancies in the transcribed text. Make sure that the names of 
the following products are spelled correctly: ZyntriQix, Digique Plus, 
CynapseFive, VortiQore V8, EchoNix Array, OrbitalLink Seven, DigiFractal 
Matrix, PULSE, RAPT, B.R.I.C.K., Q.U.A.R.T.Z., F.L.I.N.T. Only add necessary 
punctuation such as periods, commas, and capitalization, and use only the 
context provided.
"""

def generate_corrected_transcript(temperature, system_prompt, audio_file):
  response = client.chat.completions.create(
      model="gpt-4o",
      temperature=temperature,
      messages=[
          {
              "role": "system",
              "content": system_prompt
          },
          {
              "role": "user",
              "content": transcribe(audio_file, "")
          }
      ]
  )
  return completion.choices[0].message.content
corrected_text = generate_corrected_transcript(
  0, system_prompt, fake_company_filepath
)
```

If you try this on your own audio file, you'll see that GPT-4 corrects many misspellings in the transcript. Due to its larger context window, this method might be more scalable than using Whisper's prompt parameter. It's also more reliable, as GPT-4 can be instructed and guided in ways that aren't possible with Whisper due to its lack of instruction following.

Was this page useful?
Vector embeddings
=================

Learn how to turn text into numbers, unlocking use cases like search.

New embedding models

`text-embedding-3-small` and `text-embedding-3-large`, our newest and most performant embedding models, are now available. They feature lower costs, higher multilingual performance, and new parameters to control the overall size.

What are embeddings?
--------------------

OpenAI’s text embeddings measure the relatedness of text strings. Embeddings are commonly used for:

*   **Search** (where results are ranked by relevance to a query string)
*   **Clustering** (where text strings are grouped by similarity)
*   **Recommendations** (where items with related text strings are recommended)
*   **Anomaly detection** (where outliers with little relatedness are identified)
*   **Diversity measurement** (where similarity distributions are analyzed)
*   **Classification** (where text strings are classified by their most similar label)

An embedding is a vector (list) of floating point numbers. The [distance](#which-distance-function-should-i-use) between two vectors measures their relatedness. Small distances suggest high relatedness and large distances suggest low relatedness.

Visit our [pricing page](https://openai.com/api/pricing/) to learn about embeddings pricing. Requests are billed based on the number of [tokens](/tokenizer) in the [input](/docs/api-reference/embeddings/create#embeddings/create-input).

How to get embeddings
---------------------

To get an embedding, send your text string to the [embeddings API endpoint](/docs/api-reference/embeddings) along with the embedding model name (e.g., `text-embedding-3-small`):

Example: Getting embeddings

```javascript
import OpenAI from "openai";
const openai = new OpenAI();

const embedding = await openai.embeddings.create({
  model: "text-embedding-3-small",
  input: "Your text string goes here",
  encoding_format: "float",
});

console.log(embedding);
```

```python
from openai import OpenAI
client = OpenAI()

response = client.embeddings.create(
    input="Your text string goes here",
    model="text-embedding-3-small"
)

print(response.data[0].embedding)
```

```bash
curl https://api.openai.com/v1/embeddings \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "input": "Your text string goes here",
    "model": "text-embedding-3-small"
  }'
```

The response contains the embedding vector (list of floating point numbers) along with some additional metadata. You can extract the embedding vector, save it in a vector database, and use for many different use cases.

```json
{
  "object": "list",
  "data": [
    {
      "object": "embedding",
      "index": 0,
      "embedding": [
        -0.006929283495992422,
        -0.005336422007530928,
        -4.547132266452536e-05,
        -0.024047505110502243
      ],
    }
  ],
  "model": "text-embedding-3-small",
  "usage": {
    "prompt_tokens": 5,
    "total_tokens": 5
  }
}
```

By default, the length of the embedding vector is `1536` for `text-embedding-3-small` or `3072` for `text-embedding-3-large`. To reduce the embedding's dimensions without losing its concept-representing properties, pass in the [dimensions parameter](/docs/api-reference/embeddings/create#embeddings-create-dimensions). Find more detail on embedding dimensions in the [embedding use case section](#use-cases).

Embedding models
----------------

OpenAI offers two powerful third-generation embedding model (denoted by `-3` in the model ID). Read the embedding v3 [announcement blog post](https://openai.com/blog/new-embedding-models-and-api-updates) for more details.

Usage is priced per input token. Below is an example of pricing pages of text per US dollar (assuming ~800 tokens per page):

|Model|~ Pages per dollar|Performance on MTEB eval|Max input|
|---|---|---|---|
|text-embedding-3-small|62,500|62.3%|8191|
|text-embedding-3-large|9,615|64.6%|8191|
|text-embedding-ada-002|12,500|61.0%|8191|

Use cases
---------

Here we show some representative use cases, using the [Amazon fine-food reviews dataset](https://www.kaggle.com/snap/amazon-fine-food-reviews).

### Obtaining the embeddings

The dataset contains a total of 568,454 food reviews left by Amazon users up to October 2012. We use a subset of the 1000 most recent reviews for illustration purposes. The reviews are in English and tend to be positive or negative. Each review has a `ProductId`, `UserId`, `Score`, review title (`Summary`) and review body (`Text`). For example:

|Product Id|User Id|Score|Summary|Text|
|---|---|---|---|---|
|B001E4KFG0|A3SGXH7AUHU8GW|5|Good Quality Dog Food|I have bought several of the Vitality canned...|
|B00813GRG4|A1D87F6ZCVE5NK|1|Not as Advertised|Product arrived labeled as Jumbo Salted Peanut...|

Below, we combine the review summary and review text into a single combined text. The model encodes this combined text and output a single vector embedding.

[Get\_embeddings\_from\_dataset.ipynb](https://cookbook.openai.com/examples/get_embeddings_from_dataset)

```python
from openai import OpenAI
client = OpenAI()

def get_embedding(text, model="text-embedding-3-small"):
    text = text.replace("\n", " ")
    return client.embeddings.create(input = [text], model=model).data[0].embedding

df['ada_embedding'] = df.combined.apply(lambda x: get_embedding(x, model='text-embedding-3-small'))
df.to_csv('output/embedded_1k_reviews.csv', index=False)
```

To load the data from a saved file, you can run the following:

```python
import pandas as pd

df = pd.read_csv('output/embedded_1k_reviews.csv')
df['ada_embedding'] = df.ada_embedding.apply(eval).apply(np.array)
```

Reducing embedding dimensions

Using larger embeddings, for example storing them in a vector store for retrieval, generally costs more and consumes more compute, memory and storage than using smaller embeddings.

Both of our new embedding models were trained [with a technique](https://arxiv.org/abs/2205.13147) that allows developers to trade-off performance and cost of using embeddings. Specifically, developers can shorten embeddings (i.e. remove some numbers from the end of the sequence) without the embedding losing its concept-representing properties by passing in the [`dimensions` API parameter](/docs/api-reference/embeddings/create#embeddings-create-dimensions). For example, on the MTEB benchmark, a `text-embedding-3-large` embedding can be shortened to a size of 256 while still outperforming an unshortened `text-embedding-ada-002` embedding with a size of 1536. You can read more about how changing the dimensions impacts performance in our [embeddings v3 launch blog post](https://openai.com/blog/new-embedding-models-and-api-updates#:~:text=Native%20support%20for%20shortening%20embeddings).

In general, using the `dimensions` parameter when creating the embedding is the suggested approach. In certain cases, you may need to change the embedding dimension after you generate it. When you change the dimension manually, you need to be sure to normalize the dimensions of the embedding as is shown below.

```python
from openai import OpenAI
import numpy as np

client = OpenAI()

def normalize_l2(x):
    x = np.array(x)
    if x.ndim == 1:
        norm = np.linalg.norm(x)
        if norm == 0:
            return x
        return x / norm
    else:
        norm = np.linalg.norm(x, 2, axis=1, keepdims=True)
        return np.where(norm == 0, x, x / norm)

response = client.embeddings.create(
    model="text-embedding-3-small", input="Testing 123", encoding_format="float"
)

cut_dim = response.data[0].embedding[:256]
norm_dim = normalize_l2(cut_dim)

print(norm_dim)
```

Dynamically changing the dimensions enables very flexible usage. For example, when using a vector data store that only supports embeddings up to 1024 dimensions long, developers can now still use our best embedding model `text-embedding-3-large` and specify a value of 1024 for the `dimensions` API parameter, which will shorten the embedding down from 3072 dimensions, trading off some accuracy in exchange for the smaller vector size.

Question answering using embeddings-based search

[Question\_answering\_using\_embeddings.ipynb](https://cookbook.openai.com/examples/question_answering_using_embeddings)

There are many common cases where the model is not trained on data which contains key facts and information you want to make accessible when generating responses to a user query. One way of solving this, as shown below, is to put additional information into the context window of the model. This is effective in many use cases but leads to higher token costs. In this notebook, we explore the tradeoff between this approach and embeddings bases search.

```python
query = f"""Use the below article on the 2022 Winter Olympics to answer the subsequent question. If the answer cannot be found, write "I don't know."

Article:
\"\"\"
{wikipedia_article_on_curling}
\"\"\"

Question: Which athletes won the gold medal in curling at the 2022 Winter Olympics?"""

response = client.chat.completions.create(
    messages=[
        {'role': 'system', 'content': 'You answer questions about the 2022 Winter Olympics.'},
        {'role': 'user', 'content': query},
    ],
    model=GPT_MODEL,
    temperature=0,
)

print(response.choices[0].message.content)
```

Text search using embeddings

[Semantic\_text\_search\_using\_embeddings.ipynb](https://cookbook.openai.com/examples/semantic_text_search_using_embeddings)

To retrieve the most relevant documents we use the cosine similarity between the embedding vectors of the query and each document, and return the highest scored documents.

```python
from openai.embeddings_utils import get_embedding, cosine_similarity

def search_reviews(df, product_description, n=3, pprint=True):
    embedding = get_embedding(product_description, model='text-embedding-3-small')
    df['similarities'] = df.ada_embedding.apply(lambda x: cosine_similarity(x, embedding))
    res = df.sort_values('similarities', ascending=False).head(n)
    return res

res = search_reviews(df, 'delicious beans', n=3)
```

Code search using embeddings

[Code\_search.ipynb](https://cookbook.openai.com/examples/code_search_using_embeddings)

Code search works similarly to embedding-based text search. We provide a method to extract Python functions from all the Python files in a given repository. Each function is then indexed by the `text-embedding-3-small` model.

To perform a code search, we embed the query in natural language using the same model. Then we calculate cosine similarity between the resulting query embedding and each of the function embeddings. The highest cosine similarity results are most relevant.

```python
from openai.embeddings_utils import get_embedding, cosine_similarity

df['code_embedding'] = df['code'].apply(lambda x: get_embedding(x, model='text-embedding-3-small'))

def search_functions(df, code_query, n=3, pprint=True, n_lines=7):
    embedding = get_embedding(code_query, model='text-embedding-3-small')
    df['similarities'] = df.code_embedding.apply(lambda x: cosine_similarity(x, embedding))

    res = df.sort_values('similarities', ascending=False).head(n)
    return res

res = search_functions(df, 'Completions API tests', n=3)
```

Recommendations using embeddings

[Recommendation\_using\_embeddings.ipynb](https://cookbook.openai.com/examples/recommendation_using_embeddings)

Because shorter distances between embedding vectors represent greater similarity, embeddings can be useful for recommendation.

Below, we illustrate a basic recommender. It takes in a list of strings and one 'source' string, computes their embeddings, and then returns a ranking of the strings, ranked from most similar to least similar. As a concrete example, the linked notebook below applies a version of this function to the [AG news dataset](http://groups.di.unipi.it/~gulli/AG_corpus_of_news_articles.html) (sampled down to 2,000 news article descriptions) to return the top 5 most similar articles to any given source article.

```python
def recommendations_from_strings(
    strings: List[str],
    index_of_source_string: int,
    model="text-embedding-3-small",
) -> List[int]:
    """Return nearest neighbors of a given string."""

    # get embeddings for all strings
    embeddings = [embedding_from_string(string, model=model) for string in strings]

    # get the embedding of the source string
    query_embedding = embeddings[index_of_source_string]

    # get distances between the source embedding and other embeddings (function from embeddings_utils.py)
    distances = distances_from_embeddings(query_embedding, embeddings, distance_metric="cosine")

    # get indices of nearest neighbors (function from embeddings_utils.py)
    indices_of_nearest_neighbors = indices_of_nearest_neighbors_from_distances(distances)
    return indices_of_nearest_neighbors
```

Data visualization in 2D

[Visualizing\_embeddings\_in\_2D.ipynb](https://cookbook.openai.com/examples/visualizing_embeddings_in_2d)

The size of the embeddings varies with the complexity of the underlying model. In order to visualize this high dimensional data we use the t-SNE algorithm to transform the data into two dimensions.

We color the individual reviews based on the star rating which the reviewer has given:

*   1-star: red
*   2-star: dark orange
*   3-star: gold
*   4-star: turquoise
*   5-star: dark green

![Amazon ratings visualized in language using t-SNE](https://cdn.openai.com/API/docs/images/embeddings-tsne.png)

The visualization seems to have produced roughly 3 clusters, one of which has mostly negative reviews.

```python
import pandas as pd
from sklearn.manifold import TSNE
import matplotlib.pyplot as plt
import matplotlib

df = pd.read_csv('output/embedded_1k_reviews.csv')
matrix = df.ada_embedding.apply(eval).to_list()

# Create a t-SNE model and transform the data
tsne = TSNE(n_components=2, perplexity=15, random_state=42, init='random', learning_rate=200)
vis_dims = tsne.fit_transform(matrix)

colors = ["red", "darkorange", "gold", "turquiose", "darkgreen"]
x = [x for x,y in vis_dims]
y = [y for x,y in vis_dims]
color_indices = df.Score.values - 1

colormap = matplotlib.colors.ListedColormap(colors)
plt.scatter(x, y, c=color_indices, cmap=colormap, alpha=0.3)
plt.title("Amazon ratings visualized in language using t-SNE")
```

Embedding as a text feature encoder for ML algorithms

[Regression\_using\_embeddings.ipynb](https://cookbook.openai.com/examples/regression_using_embeddings)

An embedding can be used as a general free-text feature encoder within a machine learning model. Incorporating embeddings will improve the performance of any machine learning model, if some of the relevant inputs are free text. An embedding can also be used as a categorical feature encoder within a ML model. This adds most value if the names of categorical variables are meaningful and numerous, such as job titles. Similarity embeddings generally perform better than search embeddings for this task.

We observed that generally the embedding representation is very rich and information dense. For example, reducing the dimensionality of the inputs using SVD or PCA, even by 10%, generally results in worse downstream performance on specific tasks.

This code splits the data into a training set and a testing set, which will be used by the following two use cases, namely regression and classification.

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    list(df.ada_embedding.values),
    df.Score,
    test_size = 0.2,
    random_state=42
)
```

#### Regression using the embedding features

Embeddings present an elegant way of predicting a numerical value. In this example we predict the reviewer’s star rating, based on the text of their review. Because the semantic information contained within embeddings is high, the prediction is decent even with very few reviews.

We assume the score is a continuous variable between 1 and 5, and allow the algorithm to predict any floating point value. The ML algorithm minimizes the distance of the predicted value to the true score, and achieves a mean absolute error of 0.39, which means that on average the prediction is off by less than half a star.

```python
from sklearn.ensemble import RandomForestRegressor

rfr = RandomForestRegressor(n_estimators=100)
rfr.fit(X_train, y_train)
preds = rfr.predict(X_test)
```

Classification using the embedding features

[Classification\_using\_embeddings.ipynb](https://cookbook.openai.com/examples/classification_using_embeddings)

This time, instead of having the algorithm predict a value anywhere between 1 and 5, we will attempt to classify the exact number of stars for a review into 5 buckets, ranging from 1 to 5 stars.

After the training, the model learns to predict 1 and 5-star reviews much better than the more nuanced reviews (2-4 stars), likely due to more extreme sentiment expression.

```python
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import classification_report, accuracy_score

clf = RandomForestClassifier(n_estimators=100)
clf.fit(X_train, y_train)
preds = clf.predict(X_test)
```

Zero-shot classification

[Zero-shot\_classification\_with\_embeddings.ipynb](https://cookbook.openai.com/examples/zero-shot_classification_with_embeddings)

We can use embeddings for zero shot classification without any labeled training data. For each class, we embed the class name or a short description of the class. To classify some new text in a zero-shot manner, we compare its embedding to all class embeddings and predict the class with the highest similarity.

```python
from openai.embeddings_utils import cosine_similarity, get_embedding

df= df[df.Score!=3]
df['sentiment'] = df.Score.replace({1:'negative', 2:'negative', 4:'positive', 5:'positive'})

labels = ['negative', 'positive']
label_embeddings = [get_embedding(label, model=model) for label in labels]

def label_score(review_embedding, label_embeddings):
    return cosine_similarity(review_embedding, label_embeddings[1]) - cosine_similarity(review_embedding, label_embeddings[0])

prediction = 'positive' if label_score('Sample Review', label_embeddings) > 0 else 'negative'
```

Obtaining user and product embeddings for cold-start recommendation

[User\_and\_product\_embeddings.ipynb](https://cookbook.openai.com/examples/user_and_product_embeddings)

We can obtain a user embedding by averaging over all of their reviews. Similarly, we can obtain a product embedding by averaging over all the reviews about that product. In order to showcase the usefulness of this approach we use a subset of 50k reviews to cover more reviews per user and per product.

We evaluate the usefulness of these embeddings on a separate test set, where we plot similarity of the user and product embedding as a function of the rating. Interestingly, based on this approach, even before the user receives the product we can predict better than random whether they would like the product.

![Boxplot grouped by Score](https://cdn.openai.com/API/docs/images/embeddings-boxplot.png)

```python
user_embeddings = df.groupby('UserId').ada_embedding.apply(np.mean)
prod_embeddings = df.groupby('ProductId').ada_embedding.apply(np.mean)
```

Clustering

[Clustering.ipynb](https://cookbook.openai.com/examples/clustering)

Clustering is one way of making sense of a large volume of textual data. Embeddings are useful for this task, as they provide semantically meaningful vector representations of each text. Thus, in an unsupervised way, clustering will uncover hidden groupings in our dataset.

In this example, we discover four distinct clusters: one focusing on dog food, one on negative reviews, and two on positive reviews.

![Clusters identified visualized in language 2d using t-SNE](https://cdn.openai.com/API/docs/images/embeddings-cluster.png)

```python
import numpy as np
from sklearn.cluster import KMeans

matrix = np.vstack(df.ada_embedding.values)
n_clusters = 4

kmeans = KMeans(n_clusters = n_clusters, init='k-means++', random_state=42)
kmeans.fit(matrix)
df['Cluster'] = kmeans.labels_
```

FAQ
---

### How can I tell how many tokens a string has before I embed it?

In Python, you can split a string into tokens with OpenAI's tokenizer [`tiktoken`](https://github.com/openai/tiktoken).

Example code:

```python
import tiktoken

def num_tokens_from_string(string: str, encoding_name: str) -> int:
    """Returns the number of tokens in a text string."""
    encoding = tiktoken.get_encoding(encoding_name)
    num_tokens = len(encoding.encode(string))
    return num_tokens

num_tokens_from_string("tiktoken is great!", "cl100k_base")
```

For third-generation embedding models like `text-embedding-3-small`, use the `cl100k_base` encoding.

More details and example code are in the OpenAI Cookbook guide [how to count tokens with tiktoken](https://cookbook.openai.com/examples/how_to_count_tokens_with_tiktoken).

### How can I retrieve K nearest embedding vectors quickly?

For searching over many vectors quickly, we recommend using a vector database. You can find examples of working with vector databases and the OpenAI API [in our Cookbook](https://cookbook.openai.com/examples/vector_databases/readme) on GitHub.

### Which distance function should I use?

We recommend [cosine similarity](https://en.wikipedia.org/wiki/Cosine_similarity). The choice of distance function typically doesn't matter much.

OpenAI embeddings are normalized to length 1, which means that:

*   Cosine similarity can be computed slightly faster using just a dot product
*   Cosine similarity and Euclidean distance will result in the identical rankings

### Can I share my embeddings online?

Yes, customers own their input and output from our models, including in the case of embeddings. You are responsible for ensuring that the content you input to our API does not violate any applicable law or our [Terms of Use](https://openai.com/policies/terms-of-use).

### Do V3 embedding models know about recent events?

No, the `text-embedding-3-large` and `text-embedding-3-small` models lack knowledge of events that occurred after September 2021. This is generally not as much of a limitation as it would be for text generation models but in certain edge cases it can reduce performance.

Was this page useful?
Moderation
==========

Identify potentially harmful content in text and images.

Use the [moderations](/docs/api-reference/moderations) endpoint to check whether text or images are potentially harmful. If harmful content is identified, you can take corrective action, like filtering content or intervening with user accounts creating offending content. The moderation endpoint is free to use.

You can use two models for this endpoint:

*   `omni-moderation-latest`: This model and all snapshots support more categorization options and multi-modal inputs.
*   `text-moderation-latest` **(Legacy)**: Older model that supports only text inputs and fewer input categorizations. The newer omni-moderation models will be the best choice for new applications.

Quickstart
----------

Use the tabs below to see how you can moderate text inputs or image inputs, using our [official SDKs](/docs/libraries) and the [omni-moderation-latest model](/docs/models#moderation):

Moderate text inputs

Get classification information for a text input

```python
from openai import OpenAI
client = OpenAI()

response = client.moderations.create(
    model="omni-moderation-latest",
    input="...text to classify goes here...",
)

print(response)
```

```javascript
import OpenAI from "openai";
const openai = new OpenAI();

const moderation = await openai.moderations.create({
    model: "omni-moderation-latest",
    input: "...text to classify goes here...",
});

console.log(moderation);
```

```bash
curl https://api.openai.com/v1/moderations \
  -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "omni-moderation-latest",
    "input": "...text to classify goes here..."
  }'
```

Moderate images and text

Get classification information for image and text input

```python
from openai import OpenAI
client = OpenAI()

response = client.moderations.create(
    model="omni-moderation-latest",
    input=[
        {"type": "text", "text": "...text to classify goes here..."},
        {
            "type": "image_url",
            "image_url": {
                "url": "https://example.com/image.png",
                # can also use base64 encoded image URLs
                # "url": "data:image/jpeg;base64,abcdefg..."
            }
        },
    ],
)

print(response)
```

```javascript
import OpenAI from "openai";
const openai = new OpenAI();

const moderation = await openai.moderations.create({
    model: "omni-moderation-latest",
    input: [
        { type: "text", text: "...text to classify goes here..." },
        {
            type: "image_url",
            image_url: {
                url: "https://example.com/image.png"
                // can also use base64 encoded image URLs
                // url: "data:image/jpeg;base64,abcdefg..."
            }
        }
    ],
});

console.log(moderation);
```

```bash
curl https://api.openai.com/v1/moderations \
  -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "omni-moderation-latest",
    "input": [
      { "type": "text", "text": "...text to classify goes here..." },
      {
        "type": "image_url",
        "image_url": {
          "url": "https://example.com/image.png"
        }
      }
    ]
  }'
```

Here's a full example output, where the input is an image from a single frame of a war movie. The model correctly predicts indicators of violence in the image, with a `violence` category score of greater than 0.8.

```json
{
  "id": "modr-970d409ef3bef3b70c73d8232df86e7d",
  "model": "omni-moderation-latest",
  "results": [
    {
      "flagged": true,
      "categories": {
        "sexual": false,
        "sexual/minors": false,
        "harassment": false,
        "harassment/threatening": false,
        "hate": false,
        "hate/threatening": false,
        "illicit": false,
        "illicit/violent": false,
        "self-harm": false,
        "self-harm/intent": false,
        "self-harm/instructions": false,
        "violence": true,
        "violence/graphic": false
      },
      "category_scores": {
        "sexual": 2.34135824776394e-7,
        "sexual/minors": 1.6346470245419304e-7,
        "harassment": 0.0011643905680426018,
        "harassment/threatening": 0.0022121340080906377,
        "hate": 3.1999824407395835e-7,
        "hate/threatening": 2.4923252458203563e-7,
        "illicit": 0.0005227032493135171,
        "illicit/violent": 3.682979260160596e-7,
        "self-harm": 0.0011175734280627694,
        "self-harm/intent": 0.0006264858507989037,
        "self-harm/instructions": 7.368592981140821e-8,
        "violence": 0.8599265510337075,
        "violence/graphic": 0.37701736389561064
      },
      "category_applied_input_types": {
        "sexual": [
          "image"
        ],
        "sexual/minors": [],
        "harassment": [],
        "harassment/threatening": [],
        "hate": [],
        "hate/threatening": [],
        "illicit": [],
        "illicit/violent": [],
        "self-harm": [
          "image"
        ],
        "self-harm/intent": [
          "image"
        ],
        "self-harm/instructions": [
          "image"
        ],
        "violence": [
          "image"
        ],
        "violence/graphic": [
          "image"
        ]
      }
    }
  ]
}
```

The output has several categories in the JSON response, which tell you which (if any) categories of content are present in the inputs, and to what degree the model believes them to be present.

||
|flagged|Set to true if the model classifies the content as potentially harmful, false otherwise.|
|categories|Contains a dictionary of per-category violation flags. For each category, the value is true if the model flags the corresponding category as violated, false otherwise.|
|category_scores|Contains a dictionary of per-category scores output by the model, denoting the model's confidence that the input violates the OpenAI's policy for the category. The value is between 0 and 1, where higher values denote higher confidence.|
|category_applied_input_types|This property contains information on which input types were flagged in the response, for each category. For example, if the both the image and text inputs to the model are flagged for "violence/graphic", the violence/graphic property will be set to ["image", "text"]. This is only available on omni models.|

We plan to continuously upgrade the moderation endpoint's underlying model. Therefore, custom policies that rely on `category_scores` may need recalibration over time.

Content classifications
-----------------------

The table below describes the types of content that can be detected in the moderation API, along with which models and input types are supported for each category.

Categories marked as "Text only" do not support image inputs. If you send only images (without accompanying text) to the `omni-moderation-latest` model, it will return a score of 0 for these unsupported categories.

||
|harassment|Content that expresses, incites, or promotes harassing language towards any target.|All|Text only|
|harassment/threatening|Harassment content that also includes violence or serious harm towards any target.|All|Text only|
|hate|Content that expresses, incites, or promotes hate based on race, gender, ethnicity, religion, nationality, sexual orientation, disability status, or caste. Hateful content aimed at non-protected groups (e.g., chess players) is harassment.|All|Text only|
|hate/threatening|Hateful content that also includes violence or serious harm towards the targeted group based on race, gender, ethnicity, religion, nationality, sexual orientation, disability status, or caste.|All|Text only|
|illicit|Content that gives advice or instruction on how to commit illicit acts. A phrase like "how to shoplift" would fit this category.|Omni only|Text only|
|illicit/violent|The same types of content flagged by the illicit category, but also includes references to violence or procuring a weapon.|Omni only|Text only|
|self-harm|Content that promotes, encourages, or depicts acts of self-harm, such as suicide, cutting, and eating disorders.|All|Text and images|
|self-harm/intent|Content where the speaker expresses that they are engaging or intend to engage in acts of self-harm, such as suicide, cutting, and eating disorders.|All|Text and images|
|self-harm/instructions|Content that encourages performing acts of self-harm, such as suicide, cutting, and eating disorders, or that gives instructions or advice on how to commit such acts.|All|Text and images|
|sexual|Content meant to arouse sexual excitement, such as the description of sexual activity, or that promotes sexual services (excluding sex education and wellness).|All|Text and images|
|sexual/minors|Sexual content that includes an individual who is under 18 years old.|All|Text only|
|violence|Content that depicts death, violence, or physical injury.|All|Text and images|
|violence/graphic|Content that depicts death, violence, or physical injury in graphic detail.|All|Text and images|

Was this page useful?
Prompt engineering
==================

Enhance results with prompt engineering strategies.

The process of crafting prompts to get the right output from a model is called **prompt engineering**. You can improve output by giving the model precise instructions, examples, and necessary context information—like private or specialized information not included in the model's training data.

### Messages and roles

Create prompts by providing an array of `messages` that contain instructions for the model. Each message can have a different `role`, which influences how the model might interpret the input.

||
|user|Instructions that request some output from the model. Similar to messages you'd type in ChatGPT as an end user.|Pass your end-user's message to the model.Write a haiku about programming.|
|developer|Instructions to the model that are prioritized ahead of user messages, following chain of command. Previously called the system prompt.|Describe how the model should generally behave and respond.You are a helpful assistant
that answers programming
questions in the style of a
southern belle from the
southeast United States.Now, any response to a user message should have a southern belle personality and tone.|
|assistant|A message generated by the model, perhaps in a previous generation request (see the "Conversations" section below).|Provide examples to the model for how it should respond to the current request.For example, to get a model to respond correctly to knock-knock jokes, you might provide a full back-and-forth dialogue of a knock-knock joke.|

Message roles may help you get better responses, especially if you want a model to follow hierarchical instructions. They're not deterministic, so the best way to use them is just trying things and seeing what gives you good results.

Here's an example of a developer message that modifies the behavior of the model when generating a response to a `user` message:

### Using the Responses API

```javascript
const response = await openai.chat.completions.create({
  model: "gpt-4o",
  messages: [
    {
      "role": "developer",
      "content": [
        {
          "type": "text",
          "text": `
            You are a helpful assistant that answers programming 
            questions in the style of a southern belle from the 
            southeast United States.
          `
        }
      ]
    },
    {
      "role": "user",
      "content": [
        {
          "type": "text",
          "text": "Are semicolons optional in JavaScript?"
        }
      ]
    }
  ],
  store: true,
});
```

This prompt returns a text output in the rhetorical style requested:

```text
Well, sugar, that's a fine question you've got there! Now, in the 
world of JavaScript, semicolons are indeed a bit like the pearls 
on a necklace – you might slip by without 'em, but you sure do look 
more polished with 'em in place. 

Technically, JavaScript has this little thing called "automatic 
semicolon insertion" where it kindly adds semicolons for you 
where it thinks they oughta go. However, it's not always perfect, 
bless its heart. Sometimes, it might get a tad confused and cause 
all sorts of unexpected behavior.
```

### Using the Chat Completions API

```javascript
const response = await openai.chat.completions.create({
  model: "gpt-4o",
  messages: [
    {
      "role": "developer",
      "content": [
        {
          "type": "text",
          "text": `
            You are a helpful assistant that answers programming 
            questions in the style of a southern belle from the 
            southeast United States.
          `
        }
      ]
    },
    {
      "role": "user",
      "content": [
        {
          "type": "text",
          "text": "Are semicolons optional in JavaScript?"
        }
      ]
    }
  ],
  store: true,
});
```

This prompt returns a text output in the rhetorical style requested:

```text
Well, sugar, that's a fine question you've got there! Now, in the 
world of JavaScript, semicolons are indeed a bit like the pearls 
on a necklace – you might slip by without 'em, but you sure do look 
more polished with 'em in place. 

Technically, JavaScript has this little thing called "automatic 
semicolon insertion" where it kindly adds semicolons for you 
where it thinks they oughta go. However, it's not always perfect, 
bless its heart. Sometimes, it might get a tad confused and cause 
all sorts of unexpected behavior.
```

### Giving the model additional data to use for generation

You can also use the message types above to provide additional information to the model, outside of its training data. You might want to include the results of a database query, a text document, or other resources to help the model generate a relevant response. This technique is often referred to as **retrieval augmented generation**, or RAG. [Learn more about RAG techniques](https://help.openai.com/en/articles/8868588-retrieval-augmented-generation-rag-and-semantic-search-for-gpts).

This guide shares strategies and tactics for getting better results from large language models (sometimes referred to as GPT models) like GPT-4o. The methods described here can sometimes be deployed in combination for greater effect. We encourage experimentation to find the methods that work best for you.

You can also explore example prompts which showcase what our models are capable of:

[

Prompt examples

Explore prompt examples to learn what GPT models can do

](/examples)

Six strategies for getting better results
-----------------------------------------

### Write clear instructions

These models can’t read your mind. If outputs are too long, ask for brief replies. If outputs are too simple, ask for expert-level writing. If you dislike the format, demonstrate the format you’d like to see. The less the model has to guess at what you want, the more likely you’ll get it.

Tactics:

*   [Include details in your query to get more relevant answers](#tactic-include-details-in-your-query-to-get-more-relevant-answers)
*   [Ask the model to adopt a persona](#tactic-ask-the-model-to-adopt-a-persona)
*   [Use delimiters to clearly indicate distinct parts of the input](#tactic-use-delimiters-to-clearly-indicate-distinct-parts-of-the-input)
*   [Specify the steps required to complete a task](#tactic-specify-the-steps-required-to-complete-a-task)
*   [Provide examples](#tactic-provide-examples)
*   [Specify the desired length of the output](#tactic-specify-the-desired-length-of-the-output)

### Provide reference text

Language models can confidently invent fake answers, especially when asked about esoteric topics or for citations and URLs. In the same way that a sheet of notes can help a student do better on a test, providing reference text to these models can help in answering with fewer fabrications.

Tactics:

*   [Instruct the model to answer using a reference text](#tactic-instruct-the-model-to-answer-using-a-reference-text)
*   [Instruct the model to answer with citations from a reference text](#tactic-instruct-the-model-to-answer-with-citations-from-a-reference-text)

### Split complex tasks into simpler subtasks

Just as it is good practice in software engineering to decompose a complex system into a set of modular components, the same is true of tasks submitted to a language model. Complex tasks tend to have higher error rates than simpler tasks. Furthermore, complex tasks can often be re-defined as a workflow of simpler tasks in which the outputs of earlier tasks are used to construct the inputs to later tasks.

Tactics:

*   [Use intent classification to identify the most relevant instructions for a user query](#tactic-use-intent-classification-to-identify-the-most-relevant-instructions-for-a-user-query)
*   [For dialogue applications that require very long conversations, summarize or filter previous dialogue](#tactic-for-dialogue-applications-that-require-very-long-conversations-summarize-or-filter-previous-dialogue)
*   [Summarize long documents piecewise and construct a full summary recursively](#tactic-summarize-long-documents-piecewise-and-construct-a-full-summary-recursively)

### Give the model time to "think"

If asked to multiply 17 by 28, you might not know it instantly, but can still work it out with time. Similarly, models make more reasoning errors when trying to answer right away, rather than taking time to work out an answer. Asking for a "chain of thought" before an answer can help the model reason its way toward correct answers more reliably.

Tactics:

*   [Instruct the model to work out its own solution before rushing to a conclusion](#tactic-instruct-the-model-to-work-out-its-own-solution-before-rushing-to-a-conclusion)
*   [Use inner monologue or a sequence of queries to hide the model's reasoning process](#tactic-use-inner-monologue-or-a-sequence-of-queries-to-hide-the-model-s-reasoning-process)
*   [Ask the model if it missed anything on previous passes](#tactic-ask-the-model-if-it-missed-anything-on-previous-passes)

### Use external tools

Compensate for the weaknesses of the model by feeding it the outputs of other tools. For example, a text retrieval system (sometimes called RAG or retrieval augmented generation) can tell the model about relevant documents. A code execution engine like OpenAI's Code Interpreter can help the model do math and run code. If a task can be done more reliably or efficiently by a tool rather than by a language model, offload it to get the best of both.

Tactics:

*   [Use embeddings-based search to implement efficient knowledge retrieval](#tactic-use-embeddings-based-search-to-implement-efficient-knowledge-retrieval)
*   [Use code execution to perform more accurate calculations or call external APIs](#tactic-use-code-execution-to-perform-more-accurate-calculations-or-call-external-apis)
*   [Give the model access to specific functions](#tactic-give-the-model-access-to-specific-functions)

### Test changes systematically

Improving performance is easier if you can measure it. In some cases a modification to a prompt will achieve better performance on a few isolated examples but lead to worse overall performance on a more representative set of examples. Therefore to be sure that a change is net positive to performance it may be necessary to define a comprehensive test suite (also known an as an "eval").

Tactic:

*   [Evaluate model outputs with reference to gold-standard answers](#tactic-evaluate-model-outputs-with-reference-to-gold-standard-answers)

Tactics
-------

Each of the strategies listed above can be instantiated with specific tactics. These tactics are meant to provide ideas for things to try. They are by no means fully comprehensive, and you should feel free to try creative ideas not represented here.

### Strategy: Write clear instructions

#### Tactic: Include details in your query to get more relevant answers

In order to get a highly relevant response, make sure that requests provide any important details or context. Otherwise you are leaving it up to the model to guess what you mean.

|||
|---|---|
|Worse|Better|
|How do I add numbers in Excel?|How do I add up a row of dollar amounts in Excel? I want to do this automatically for a whole sheet of rows with all the totals ending up on the right in a column called "Total".|
|Who’s president?|Who was the president of Mexico in 2021, and how frequently are elections held?|
|Write code to calculate the Fibonacci sequence.|Write a TypeScript function to efficiently calculate the Fibonacci sequence. Comment the code liberally to explain what each piece does and why it's written that way.|
|Summarize the meeting notes.|Summarize the meeting notes in a single paragraph. Then write a markdown list of the speakers and each of their key points. Finally, list the next steps or action items suggested by the speakers, if any.|

#### Tactic: Ask the model to adopt a persona

The system message can be used to specify the persona used by the model in its replies.

SYSTEM

When I ask for help to write something, you will reply with a document that contains at least one joke or playful comment in every paragraph.

USER

Write a thank you note to my steel bolt vendor for getting the delivery in on time and in short notice. This made it possible for us to deliver an important order.

Based on internal evals, the `gpt-4.5-preview` model has a particular system message that results in better performance. Add your own system message contents after this:

SYSTEM

You are a highly capable, thoughtful, and precise assistant. Your goal is to deeply understand the user's intent, ask clarifying questions when needed, think step-by-step through complex problems, provide clear and accurate answers, and proactively anticipate helpful follow-up information. Always prioritize being truthful, nuanced, insightful, and efficient, tailoring your responses specifically to the user's needs and preferences.

#### Tactic: Use delimiters to clearly indicate distinct parts of the input

Delimiters like triple quotation marks, XML tags, section titles, etc. can help demarcate sections of text to be treated differently.

USER

Summarize the text delimited by triple quotes with a haiku. """insert text here"""

SYSTEM

You will be provided with a pair of articles (delimited with XML tags) about the same topic. First summarize the arguments of each article. Then indicate which of them makes a better argument and explain why.

USER

<article> insert first article here </article> <article> insert second article here </article>

SYSTEM

You will be provided with a thesis abstract and a suggested title for it. The thesis title should give the reader a good idea of the topic of the thesis but should also be eye-catching. If the title does not meet these criteria, suggest 5 alternatives.

USER

Abstract: insert abstract here Title: insert title here

For straightforward tasks such as these, using delimiters might not make a difference in the output quality. However, the more complex a task is the more important it is to disambiguate task details. Don’t make the model work to understand exactly what you are asking of them.

#### Tactic: Specify the steps required to complete a task

Some tasks are best specified as a sequence of steps. Writing the steps out explicitly can make it easier for the model to follow them.

SYSTEM

Use the following step-by-step instructions to respond to user inputs. Step 1 - The user will provide you with text in triple quotes. Summarize this text in one sentence with a prefix that says "Summary: ". Step 2 - Translate the summary from Step 1 into Spanish, with a prefix that says "Translation: ".

USER

"""insert text here"""

#### Tactic: Provide examples

Providing general instructions that apply to all examples is generally more efficient than demonstrating all permutations of a task by example, but in some cases providing examples may be easier. For example, if you intend for the model to copy a particular style of responding to user queries which is difficult to describe explicitly. This is known as "few-shot" prompting.

SYSTEM

Answer in a consistent style.

USER

Teach me about patience.

ASSISTANT

The river that carves the deepest valley flows from a modest spring; the grandest symphony originates from a single note; the most intricate tapestry begins with a solitary thread.

USER

Teach me about the ocean.

#### Tactic: Specify the desired length of the output

You can ask the model to produce outputs that are of a given target length. The targeted output length can be specified in terms of the count of words, sentences, paragraphs, bullet points, etc. Note however that instructing the model to generate a specific number of words does not work with high precision. The model can more reliably generate outputs with a specific number of paragraphs or bullet points.

USER

Summarize the text delimited by triple quotes in about 50 words. """insert text here"""

USER

Summarize the text delimited by triple quotes in 2 paragraphs. """insert text here"""

USER

Summarize the text delimited by triple quotes in 3 bullet points. """insert text here"""

### Strategy: Provide reference text

#### Tactic: Instruct the model to answer using a reference text

If we can provide a model with trusted information that is relevant to the current query, then we can instruct the model to use the provided information to compose its answer.

SYSTEM

Use the provided articles delimited by triple quotes to answer questions. If the answer cannot be found in the articles, write "I could not find an answer."

USER

<insert articles, each delimited by triple quotes> Question: <insert question here>

Given that all models have limited context windows, we need some way to dynamically lookup information that is relevant to the question being asked. [Embeddings](https://platform.openai.com/docs/guides/embeddings#what-are-embeddings) can be used to implement efficient knowledge retrieval. See the tactic ["Use embeddings-based search to implement efficient knowledge retrieval"](#tactic-use-embeddings-based-search-to-implement-efficient-knowledge-retrieval) for more details on how to implement this.

#### Tactic: Instruct the model to answer with citations from a reference text

If the input has been supplemented with relevant knowledge, it's straightforward to request that the model add citations to its answers by referencing passages from provided documents. Note that citations in the output can then be verified programmatically by string matching within the provided documents.

SYSTEM

You will be provided with a document delimited by triple quotes and a question. Your task is to answer the question using only the provided document and to cite the passage(s) of the document used to answer the question. If the document does not contain the information needed to answer this question then simply write: "Insufficient information." If an answer to the question is provided, it must be annotated with a citation. Use the following format for to cite relevant passages ({"citation": …}).

USER

"""<insert document here>""" Question: <insert question here>

### Strategy: Split complex tasks into simpler subtasks

#### Tactic: Use intent classification to identify the most relevant instructions for a user query

For tasks in which lots of independent sets of instructions are needed to handle different cases, it can be beneficial to first classify the type of query and to use that classification to determine which instructions are needed. This can be achieved by defining fixed categories and hardcoding instructions that are relevant for handling tasks in a given category. This process can also be applied recursively to decompose a task into a sequence of stages. The advantage of this approach is that each query will contain only those instructions that are required to perform the next stage of a task which can result in lower error rates compared to using a single query to perform the whole task. This can also result in lower costs since larger prompts cost more to run ([see pricing information](https://openai.com/api/pricing)).

Suppose for example that for a customer service application, queries could be usefully classified as follows:

SYSTEM

You will be provided with customer service queries. Classify each query into a primary category and a secondary category. Provide your output in json format with the keys: primary and secondary. Primary categories: Billing, Technical Support, Account Management, or General Inquiry. Billing secondary categories: - Unsubscribe or upgrade - Add a payment method - Explanation for charge - Dispute a charge Technical Support secondary categories: - Troubleshooting - Device compatibility - Software updates Account Management secondary categories: - Password reset - Update personal information - Close account - Account security General Inquiry secondary categories: - Product information - Pricing - Feedback - Speak to a human

USER

I need to get my internet working again.

Based on the classification of the customer query, a set of more specific instructions can be provided to a model for it to handle next steps. For example, suppose the customer requires help with "troubleshooting".

SYSTEM

You will be provided with customer service inquiries that require troubleshooting in a technical support context. Help the user by: - Ask them to check that all cables to/from the router are connected. Note that it is common for cables to come loose over time. - If all cables are connected and the issue persists, ask them which router model they are using - Now you will advise them how to restart their device: -- If the model number is MTD-327J, advise them to push the red button and hold it for 5 seconds, then wait 5 minutes before testing the connection. -- If the model number is MTD-327S, advise them to unplug and replug it, then wait 5 minutes before testing the connection. - If the customer's issue persists after restarting the device and waiting 5 minutes, connect them to IT support by outputting {"IT support requested"}. - If the user starts asking questions that are unrelated to this topic then confirm if they would like to end the current chat about troubleshooting and classify their request according to the following scheme: <insert primary/secondary classification scheme from above here>

USER

I need to get my internet working again.

Notice that the model has been instructed to emit special strings to indicate when the state of the conversation changes. This enables us to turn our system into a state machine where the state determines which instructions are injected. By keeping track of state, what instructions are relevant at that state, and also optionally what state transitions are allowed from that state, we can put guardrails around the user experience that would be hard to achieve with a less structured approach.

#### Tactic: For dialogue applications that require very long conversations, summarize or filter previous dialogue

Since models have a fixed context length, dialogue between a user and an assistant in which the entire conversation is included in the context window cannot continue indefinitely.

There are various workarounds to this problem, one of which is to summarize previous turns in the conversation. Once the size of the input reaches a predetermined threshold length, this could trigger a query that summarizes part of the conversation and the summary of the prior conversation could be included as part of the system message. Alternatively, prior conversation could be summarized asynchronously in the background throughout the entire conversation.

An alternative solution is to dynamically select previous parts of the conversation that are most relevant to the current query. See the tactic ["Use embeddings-based search to implement efficient knowledge retrieval"](#tactic-use-embeddings-based-search-to-implement-efficient-knowledge-retrieval).

#### Tactic: Summarize long documents piecewise and construct a full summary recursively

Since models have a fixed context length, they cannot be used to summarize a text longer than the context length minus the length of the generated summary in a single query.

To summarize a very long document such as a book we can use a sequence of queries to summarize each section of the document. Section summaries can be concatenated and summarized producing summaries of summaries. This process can proceed recursively until an entire document is summarized. If it’s necessary to use information about earlier sections in order to make sense of later sections, then a further trick that can be useful is to include a running summary of the text that precedes any given point in the book while summarizing content at that point. The effectiveness of this procedure for summarizing books has been studied in previous [research](https://openai.com/research/summarizing-books) by OpenAI using variants of GPT-3.

### Strategy: Give models time to "think"

#### Tactic: Instruct the model to work out its own solution before rushing to a conclusion

Sometimes we get better results when we explicitly instruct the model to reason from first principles before coming to a conclusion. Suppose for example we want a model to evaluate a student’s solution to a math problem. The most obvious way to approach this is to simply ask the model if the student's solution is correct or not.

SYSTEM

Determine if the student's solution is correct or not.

USER

Problem Statement: I'm building a solar power installation and I need help working out the financials. - Land costs $100 / square foot - I can buy solar panels for $250 / square foot - I negotiated a contract for maintenance that will cost me a flat $100k per year, and an additional $10 / square foot What is the total cost for the first year of operations as a function of the number of square feet. Student's Solution: Let x be the size of the installation in square feet. 1. Land cost: 100x 2. Solar panel cost: 250x 3. Maintenance cost: 100,000 + 100x Total cost: 100x + 250x + 100,000 + 100x = 450x + 100,000

ASSISTANT

The student's solution is correct.

But the student's solution is actually not correct! We can get the model to successfully notice this by prompting the model to generate its own solution first.

SYSTEM

First work out your own solution to the problem. Then compare your solution to the student's solution and evaluate if the student's solution is correct or not. Don't decide if the student's solution is correct until you have done the problem yourself.

USER

Problem Statement: I'm building a solar power installation and I need help working out the financials. - Land costs $100 / square foot - I can buy solar panels for $250 / square foot - I negotiated a contract for maintenance that will cost me a flat $100k per year, and an additional $10 / square foot What is the total cost for the first year of operations as a function of the number of square feet. Student's Solution: Let x be the size of the installation in square feet. 1. Land cost: 100x 2. Solar panel cost: 250x 3. Maintenance cost: 100,000 + 100x Total cost: 100x + 250x + 100,000 + 100x = 450x + 100,000

ASSISTANT

Let x be the size of the installation in square feet. 1. Land cost: 100x 2. Solar panel cost: 250x 3. Maintenance cost: 100,000 + 10x Total cost: 100x + 250x + 100,000 + 10x = 360x + 100,000 The student's solution is incorrect. They made an error in the maintenance cost calculation, using 100x instead of 10x. The correct total cost for the first year of operations is 360x + 100,000.

#### Tactic: Use inner monologue or a sequence of queries to hide the model's reasoning process

The previous tactic demonstrates that it is sometimes important for the model to reason in detail about a problem before answering a specific question. For some applications, the reasoning process that a model uses to arrive at a final answer would be inappropriate to share with the user. For example, in tutoring applications we may want to encourage students to work out their own answers, but a model’s reasoning process about the student’s solution could reveal the answer to the student.

Inner monologue is a tactic that can be used to mitigate this. The idea of inner monologue is to instruct the model to put parts of the output that are meant to be hidden from the user into a structured format that makes parsing them easy. Then before presenting the output to the user, the output is parsed and only part of the output is made visible.

SYSTEM

Follow these steps to answer the user queries. Step 1 - First work out your own solution to the problem. Don't rely on the student's solution since it may be incorrect. Enclose all your work for this step within triple quotes ("""). Step 2 - Compare your solution to the student's solution and evaluate if the student's solution is correct or not. Enclose all your work for this step within triple quotes ("""). Step 3 - If the student made a mistake, determine what hint you could give the student without giving away the answer. Enclose all your work for this step within triple quotes ("""). Step 4 - If the student made a mistake, provide the hint from the previous step to the student (outside of triple quotes). Instead of writing "Step 4 - ..." write "Hint:".

USER

Problem Statement: <insert problem statement> Student Solution: <insert student solution>

Alternatively, this can be achieved with a sequence of queries in which all except the last have their output hidden from the end user.

First, we can ask the model to solve the problem on its own. Since this initial query doesn't require the student’s solution, it can be omitted. This provides the additional advantage that there is no chance that the model’s solution will be biased by the student’s attempted solution.

USER

<insert problem statement>

Next, we can have the model use all available information to assess the correctness of the student’s solution.

SYSTEM

Compare your solution to the student's solution and evaluate if the student's solution is correct or not.

USER

Problem statement: """<insert problem statement>""" Your solution: """<insert model generated solution>""" Student’s solution: """<insert student's solution>"""

Finally, we can let the model use its own analysis to construct a reply in the persona of a helpful tutor.

SYSTEM

You are a math tutor. If the student made an error, offer a hint to the student in a way that does not reveal the answer. If the student did not make an error, simply offer them an encouraging comment.

USER

Problem statement: """<insert problem statement>""" Your solution: """<insert model generated solution>""" Student’s solution: """<insert student's solution>""" Analysis: """<insert model generated analysis from previous step>"""

#### Tactic: Ask the model if it missed anything on previous passes

Suppose that we are using a model to list excerpts from a source which are relevant to a particular question. After listing each excerpt the model needs to determine if it should start writing another or if it should stop. If the source document is large, it is common for a model to stop too early and fail to list all relevant excerpts. In that case, better performance can often be obtained by prompting the model with followup queries to find any excerpts it missed on previous passes.

SYSTEM

You will be provided with a document delimited by triple quotes. Your task is to select excerpts which pertain to the following question: "What significant paradigm shifts have occurred in the history of artificial intelligence." Ensure that excerpts contain all relevant context needed to interpret them - in other words don't extract small snippets that are missing important context. Provide output in JSON format as follows: \[{"excerpt": "..."}, ... {"excerpt": "..."}\]

USER

"""<insert document here>"""

ASSISTANT

\[{"excerpt": "the model writes an excerpt here"}, ... {"excerpt": "the model writes another excerpt here"}\]

USER

Are there more relevant excerpts? Take care not to repeat excerpts. Also ensure that excerpts contain all relevant context needed to interpret them - in other words don't extract small snippets that are missing important context.

### Strategy: Use external tools

#### Tactic: Use embeddings-based search to implement efficient knowledge retrieval

A model can leverage external sources of information if provided as part of its input. This can help the model to generate more informed and up-to-date responses. For example, if a user asks a question about a specific movie, it may be useful to add high quality information about the movie (e.g. actors, director, etc…) to the model’s input. Embeddings can be used to implement efficient knowledge retrieval, so that relevant information can be added to the model input dynamically at run-time.

A text embedding is a vector that can measure the relatedness between text strings. Similar or relevant strings will be closer together than unrelated strings. This fact, along with the existence of fast vector search algorithms means that embeddings can be used to implement efficient knowledge retrieval. In particular, a text corpus can be split up into chunks, and each chunk can be embedded and stored. Then a given query can be embedded and vector search can be performed to find the embedded chunks of text from the corpus that are most related to the query (i.e. closest together in the embedding space).

Example implementations can be found in the [OpenAI Cookbook](https://cookbook.openai.com/examples/vector_databases/readme). See the tactic [“Instruct the model to use retrieved knowledge to answer queries”](#tactic-instruct-the-model-to-answer-using-a-reference-text) for an example of how to use knowledge retrieval to minimize the likelihood that a model will make up incorrect facts.

#### Tactic: Use code execution to perform more accurate calculations or call external APIs

Language models cannot be relied upon to perform arithmetic or long calculations accurately on their own. In cases where this is needed, a model can be instructed to write and run code instead of making its own calculations. In particular, a model can be instructed to put code that is meant to be run into a designated format such as triple backtick. After an output is produced, the code can be extracted and run. Finally, if necessary, the output from the code execution engine (i.e. Python interpreter) can be provided as an input to the model for the next query.

SYSTEM

You can write and execute Python code by enclosing it in triple backticks, e.g. \`\`\`code goes here\`\`\`. Use this to perform calculations.

USER

Find all real-valued roots of the following polynomial: 3\*x\*\*5 - 5\*x\*\*4 - 3\*x\*\*3 - 7\*x - 10.

Another good use case for code execution is calling external APIs. If a model is instructed in the proper use of an API, it can write code that makes use of it. A model can be instructed in how to use an API by providing it with documentation and/or code samples showing how to use the API.

SYSTEM

You can write and execute Python code by enclosing it in triple backticks. Also note that you have access to the following module to help users send messages to their friends: \`\`\`python import message message.write(to="John", message="Hey, want to meetup after work?")\`\`\`

**WARNING: Executing code produced by a model is not inherently safe and precautions should be taken in any application that seeks to do this. In particular, a sandboxed code execution environment is needed to limit the harm that untrusted code could cause.**

#### Tactic: Give the model access to specific functions

The Chat Completions API allows passing a list of function descriptions in requests. This enables models to generate function arguments according to the provided schemas. Generated function arguments are returned by the API in JSON format and can be used to execute function calls. Output provided by function calls can then be fed back into a model in the following request to close the loop. This is the recommended way of using OpenAI models to call external functions. To learn more see the [function calling section](/docs/guides/function-calling) in our introductory text generation guide and more [function calling examples](https://cookbook.openai.com/examples/how_to_call_functions_with_chat_models) in the OpenAI Cookbook.

### Strategy: Test changes systematically

Sometimes it can be hard to tell whether a change — e.g., a new instruction or a new design — makes your system better or worse. Looking at a few examples may hint at which is better, but with small sample sizes it can be hard to distinguish between a true improvement or random luck. Maybe the change helps performance on some inputs, but hurts performance on others.

Evaluation procedures (or "evals") are useful for optimizing system designs. Good evals are:

*   Representative of real-world usage (or at least diverse)
*   Contain many test cases for greater statistical power (see table below for guidelines)
*   Easy to automate or repeat

|Difference to detect|Sample size needed for 95% confidence|
|---|---|
|30%|~10|
|10%|~100|
|3%|~1,000|
|1%|~10,000|

Evaluation of outputs can be done by computers, humans, or a mix. Computers can automate evals with objective criteria (e.g., questions with single correct answers) as well as some subjective or fuzzy criteria, in which model outputs are evaluated by other model queries. [OpenAI Evals](https://github.com/openai/evals) is an open-source software framework that provides tools for creating automated evals.

Model-based evals can be useful when there exists a range of possible outputs that would be considered equally high in quality (e.g. for questions with long answers). The boundary between what can be realistically evaluated with a model-based eval and what requires a human to evaluate is fuzzy and is constantly shifting as models become more capable. We encourage experimentation to figure out how well model-based evals can work for your use case.

#### Tactic: Evaluate model outputs with reference to gold-standard answers

Suppose it is known that the correct answer to a question should make reference to a specific set of known facts. Then we can use a model query to count how many of the required facts are included in the answer.

For example, using the following system message:

SYSTEM

You will be provided with text delimited by triple quotes that is supposed to be the answer to a question. Check if the following pieces of information are directly contained in the answer: - Neil Armstrong was the first person to walk on the moon. - The date Neil Armstrong first walked on the moon was July 21, 1969. For each of these points perform the following steps: 1 - Restate the point. 2 - Provide a citation from the answer which is closest to this point. 3 - Consider if someone reading the citation who doesn't know the topic could directly infer the point. Explain why or why not before making up your mind. 4 - Write "yes" if the answer to 3 was yes, otherwise write "no". Finally, provide a count of how many "yes" answers there are. Provide this count as {"count": <insert count here>}.

Here's an example input where both points are satisfied:

SYSTEM

<insert system message above>

USER

"""Neil Armstrong is famous for being the first human to set foot on the Moon. This historic event took place on July 21, 1969, during the Apollo 11 mission."""

Here's an example input where only one point is satisfied:

SYSTEM

<insert system message above>

USER

"""Neil Armstrong made history when he stepped off the lunar module, becoming the first person to walk on the moon."""

Here's an example input where none are satisfied:

SYSTEM

<insert system message above>

USER

"""In the summer of '69, a voyage grand, Apollo 11, bold as legend's hand. Armstrong took a step, history unfurled, "One small step," he said, for a new world."""

There are many possible variants on this type of model-based eval. Consider the following variation which tracks the kind of overlap between the candidate answer and the gold-standard answer, and also tracks whether the candidate answer contradicts any part of the gold-standard answer.

SYSTEM

Use the following steps to respond to user inputs. Fully restate each step before proceeding. i.e. "Step 1: Reason...". Step 1: Reason step-by-step about whether the information in the submitted answer compared to the expert answer is either: disjoint, equal, a subset, a superset, or overlapping (i.e. some intersection but not subset/superset). Step 2: Reason step-by-step about whether the submitted answer contradicts any aspect of the expert answer. Step 3: Output a JSON object structured like: {"type\_of\_overlap": "disjoint" or "equal" or "subset" or "superset" or "overlapping", "contradiction": true or false}

Here's an example input with a substandard answer which nonetheless does not contradict the expert answer:

SYSTEM

<insert system message above>

USER

Question: """What event is Neil Armstrong most famous for and on what date did it occur? Assume UTC time.""" Submitted Answer: """Didn't he walk on the moon or something?""" Expert Answer: """Neil Armstrong is most famous for being the first person to walk on the moon. This historic event occurred on July 21, 1969."""

Here's an example input with answer that directly contradicts the expert answer:

SYSTEM

<insert system message above>

USER

Question: """What event is Neil Armstrong most famous for and on what date did it occur? Assume UTC time.""" Submitted Answer: """On the 21st of July 1969, Neil Armstrong became the second person to walk on the moon, following after Buzz Aldrin.""" Expert Answer: """Neil Armstrong is most famous for being the first person to walk on the moon. This historic event occurred on July 21, 1969."""

Here's an example input with a correct answer that also provides a bit more detail than is necessary:

SYSTEM

<insert system message above>

USER

Question: """What event is Neil Armstrong most famous for and on what date did it occur? Assume UTC time.""" Submitted Answer: """At approximately 02:56 UTC on July 21st 1969, Neil Armstrong became the first human to set foot on the lunar surface, marking a monumental achievement in human history.""" Expert Answer: """Neil Armstrong is most famous for being the first person to walk on the moon. This historic event occurred on July 21, 1969."""

Optimizing model outputs
------------------------

As you iterate on your prompts, you'll continually aim to improve **accuracy**, **cost**, and **latency**. Below, find techniques that optimize for each goal.

||
|Accuracy|Ensure the model produces accurate and useful responses to your prompts.|Accurate responses require that the model has all the information it needs to generate a response, and knows how to go about creating a response (from interpreting input to formatting and styling). Often, this will require a mix of prompt engineering, RAG, and model fine-tuning.Learn more about optimizing for accuracy.|
|Cost|Drive down total cost of using models by reducing token usage and using cheaper models when possible.|To control costs, you can try to use fewer tokens or smaller, cheaper models. Learn more about optimizing for cost.|
|Latency|Decrease the time it takes to generate responses to your prompts.|Optimizing for low latency is a multifaceted process including prompt engineering and parallelism in your own code. Learn more about optimizing for latency.|

Other resources
---------------

For more inspiration, visit the [OpenAI Cookbook](https://cookbook.openai.com), which contains example code and also links to third-party resources such as:

*   [Prompting libraries & tools](https://cookbook.openai.com/related_resources#prompting-libraries--tools)
*   [Prompting guides](https://cookbook.openai.com/related_resources#prompting-guides)
*   [Video courses](https://cookbook.openai.com/related_resources#video-courses)
*   [Papers on advanced prompting to improve reasoning](https://cookbook.openai.com/related_resources#papers-on-advanced-prompting-to-improve-reasoning)

Was this page useful?
Production best practices
=========================

Transition AI projects to production with best practices.

This guide provides a comprehensive set of best practices to help you transition from prototype to production. Whether you are a seasoned machine learning engineer or a recent enthusiast, this guide should provide you with the tools you need to successfully put the platform to work in a production setting: from securing access to our API to designing a robust architecture that can handle high traffic volumes. Use this guide to help develop a plan for deploying your application as smoothly and effectively as possible.

If you want to explore best practices for going into production further, please check out our Developer Day talk:

Setting up your organization
----------------------------

Once you [log in](/login) to your OpenAI account, you can find your organization name and ID in your [organization settings](/settings/organization/general). The organization name is the label for your organization, shown in user interfaces. The organization ID is the unique identifier for your organization which can be used in API requests.

Users who belong to multiple organizations can [pass a header](/docs/api-reference/requesting-organization) to specify which organization is used for an API request. Usage from these API requests will count against the specified organization's quota. If no header is provided, the [default organization](/settings/organization/api-keys) will be billed. You can change your default organization in your [user settings](/settings/organization/api-keys).

You can invite new members to your organization from the [Team page](/settings/organization/team). Members can be **readers** or **owners**.

Readers:

*   Can make API requests.
*   Can view basic organization information.
*   Can create, update, and delete resources (like Assistants) in the organization, unless otherwise noted.

Owners:

*   Have all the permissions of readers.
*   Can modify billing information.
*   Can manage members within the organization.

### Managing billing limits

To begin using the OpenAI API, enter your [billing information](/settings/organization/billing/overview). If no billing information is entered, you will still have login access but will be unable to make API requests.

Once you’ve entered your billing information, you will have an approved usage limit of $100 per month, which is set by OpenAI. Your quota limit will automatically increase as your usage on your platform increases and you move from one [usage tier](/docs/guides/rate-limits#usage-tiers) to another. You can review your current usage limit in the [limits](/settings/organization/limits) page in your account settings.

If you’d like to be notified when your usage exceeds a certain dollar amount, you can set a notification threshold through the [usage limits](/settings/organization/limits) page. When the notification threshold is reached, the owners of the organization will receive an email notification. You can also set a monthly budget so that, once the monthly budget is reached, any subsequent API requests will be rejected. Note that these limits are best effort, and there may be 5 to 10 minutes of delay between the usage and the limits being enforced.

### API keys

The OpenAI API uses API keys for authentication. Visit your [API keys](/settings/organization/api-keys) page to retrieve the API key you'll use in your requests.

This is a relatively straightforward way to control access, but you must be vigilant about securing these keys. Avoid exposing the API keys in your code or in public repositories; instead, store them in a secure location. You should expose your keys to your application using environment variables or secret management service, so that you don't need to hard-code them in your codebase. Read more in our [Best practices for API key safety](https://help.openai.com/en/articles/5112595-best-practices-for-api-key-safety).

API key usage can be monitored on the [Usage page](/usage) once tracking is enabled. If you are using an API key generated prior to Dec 20, 2023 tracking will not be enabled by default. You can enable tracking going forward on the [API key management dashboard](/api-keys). All API keys generated past Dec 20, 2023 have tracking enabled. Any previous untracked usage will be displayed as `Untracked` in the dashboard.

### Staging projects

As you scale, you may want to create separate projects for your staging and production environments. You can create these projects in the dashboard, allowing you to isolate your development and testing work, so you don't accidentally disrupt your live application. You can also limit user access to your production project, and set custom rate and spend limits per project.

Scaling your solution architecture
----------------------------------

When designing your application or service for production that uses our API, it's important to consider how you will scale to meet traffic demands. There are a few key areas you will need to consider regardless of the cloud service provider of your choice:

*   **Horizontal scaling**: You may want to scale your application out horizontally to accommodate requests to your application that come from multiple sources. This could involve deploying additional servers or containers to distribute the load. If you opt for this type of scaling, make sure that your architecture is designed to handle multiple nodes and that you have mechanisms in place to balance the load between them.
*   **Vertical scaling**: Another option is to scale your application up vertically, meaning you can beef up the resources available to a single node. This would involve upgrading your server's capabilities to handle the additional load. If you opt for this type of scaling, make sure your application is designed to take advantage of these additional resources.
*   **Caching**: By storing frequently accessed data, you can improve response times without needing to make repeated calls to our API. Your application will need to be designed to use cached data whenever possible and invalidate the cache when new information is added. There are a few different ways you could do this. For example, you could store data in a database, filesystem, or in-memory cache, depending on what makes the most sense for your application.
*   **Load balancing**: Finally, consider load-balancing techniques to ensure requests are distributed evenly across your available servers. This could involve using a load balancer in front of your servers or using DNS round-robin. Balancing the load will help improve performance and reduce bottlenecks.

### Managing rate limits

When using our API, it's important to understand and plan for [rate limits](/docs/guides/rate-limits).

Improving latencies
-------------------

Check out our most up-to-date guide on [latency optimization](/docs/guides/latency-optimization).

Latency is the time it takes for a request to be processed and a response to be returned. In this section, we will discuss some factors that influence the latency of our text generation models and provide suggestions on how to reduce it.

The latency of a completion request is mostly influenced by two factors: the model and the number of tokens generated. The life cycle of a completion request looks like this:

Network

End user to API latency

Server

Time to process prompt tokens

Server

Time to sample/generate tokens

Network

API to end user latency

  

The bulk of the latency typically arises from the token generation step.

> **Intuition**: Prompt tokens add very little latency to completion calls. Time to generate completion tokens is much longer, as tokens are generated one at a time. Longer generation lengths will accumulate latency due to generation required for each token.

### Common factors affecting latency and possible mitigation techniques

Now that we have looked at the basics of latency, let’s take a look at various factors that can affect latency, broadly ordered from most impactful to least impactful.

#### Model

Our API offers different models with varying levels of complexity and generality. The most capable models, such as `gpt-4`, can generate more complex and diverse completions, but they also take longer to process your query. Models such as `gpt-4o-mini`, can generate faster and cheaper Chat Completions, but they may generate results that are less accurate or relevant for your query. You can choose the model that best suits your use case and the trade-off between speed, cost, and quality.

#### Number of completion tokens

Requesting a large amount of generated tokens completions can lead to increased latencies:

*   **Lower max tokens**: for requests with a similar token generation count, those that have a lower `max_tokens` parameter incur less latency.
*   **Include stop sequences**: to prevent generating unneeded tokens, add a stop sequence. For example, you can use stop sequences to generate a list with a specific number of items. In this case, by using `11.` as a stop sequence, you can generate a list with only 10 items, since the completion will stop when `11.` is reached. [Read our help article on stop sequences](https://help.openai.com/en/articles/5072263-how-do-i-use-stop-sequences) for more context on how you can do this.
*   **Generate fewer completions**: lower the values of `n` and `best_of` when possible where `n` refers to how many completions to generate for each prompt and `best_of` is used to represent the result with the highest log probability per token.

If `n` and `best_of` both equal 1 (which is the default), the number of generated tokens will be at most, equal to `max_tokens`.

If `n` (the number of completions returned) or `best_of` (the number of completions generated for consideration) are set to `> 1`, each request will create multiple outputs. Here, you can consider the number of generated tokens as `[ max_tokens * max (n, best_of) ]`

#### Streaming

Setting `stream: true` in a request makes the model start returning tokens as soon as they are available, instead of waiting for the full sequence of tokens to be generated. It does not change the time to get all the tokens, but it reduces the time for first token for an application where we want to show partial progress or are going to stop generations. This can be a better user experience and a UX improvement so it’s worth experimenting with streaming.

#### Infrastructure

Our servers are currently located in the US. While we hope to have global redundancy in the future, in the meantime you could consider locating the relevant parts of your infrastructure in the US to minimize the roundtrip time between your servers and the OpenAI servers.

#### Batching

Depending on your use case, batching _may help_. If you are sending multiple requests to the same endpoint, you can [batch the prompts](/docs/guides/rate-limits#batching-requests) to be sent in the same request. This will reduce the number of requests you need to make. The prompt parameter can hold up to 20 unique prompts. We advise you to test out this method and see if it helps. In some cases, you may end up increasing the number of generated tokens which will slow the response time.

Managing costs
--------------

To monitor your costs, you can set a [notification threshold](/settings/organization/limits) in your account to receive an email alert once you pass a certain usage threshold. You can also set a [monthly budget](/settings/organization/limits). Please be mindful of the potential for a monthly budget to cause disruptions to your application/users. Use the [usage tracking dashboard](/settings/organization/usage) to monitor your token usage during the current and past billing cycles.

### Text generation

One of the challenges of moving your prototype into production is budgeting for the costs associated with running your application. OpenAI offers a [pay-as-you-go pricing model](https://openai.com/api/pricing/), with prices per 1,000 tokens (roughly equal to 750 words). To estimate your costs, you will need to project the token utilization. Consider factors such as traffic levels, the frequency with which users will interact with your application, and the amount of data you will be processing.

**One useful framework for thinking about reducing costs is to consider costs as a function of the number of tokens and the cost per token.** There are two potential avenues for reducing costs using this framework. First, you could work to reduce the cost per token by switching to smaller models for some tasks in order to reduce costs. Alternatively, you could try to reduce the number of tokens required. There are a few ways you could do this, such as by using shorter prompts, [fine-tuning](/docs/guides/fine-tuning) models, or caching common user queries so that they don't need to be processed repeatedly.

You can experiment with our interactive [tokenizer tool](/tokenizer) to help you estimate costs. The API and playground also returns token counts as part of the response. Once you’ve got things working with our most capable model, you can see if the other models can produce the same results with lower latency and costs. Learn more in our [token usage help article](https://help.openai.com/en/articles/6614209-how-do-i-check-my-token-usage).

MLOps strategy
--------------

As you move your prototype into production, you may want to consider developing an MLOps strategy. MLOps (machine learning operations) refers to the process of managing the end-to-end life cycle of your machine learning models, including any models you may be fine-tuning using our API. There are a number of areas to consider when designing your MLOps strategy. These include

*   Data and model management: managing the data used to train or fine-tune your model and tracking versions and changes.
*   Model monitoring: tracking your model's performance over time and detecting any potential issues or degradation.
*   Model retraining: ensuring your model stays up to date with changes in data or evolving requirements and retraining or fine-tuning it as needed.
*   Model deployment: automating the process of deploying your model and related artifacts into production.

Thinking through these aspects of your application will help ensure your model stays relevant and performs well over time.

Security and compliance
-----------------------

As you move your prototype into production, you will need to assess and address any security and compliance requirements that may apply to your application. This will involve examining the data you are handling, understanding how our API processes data, and determining what regulations you must adhere to. Our [security practices](https://www.openai.com/security) and [trust and compliance portal](https://trust.openai.com/) provide our most comprehensive and up-to-date documentation. For reference, here is our [Privacy Policy](https://openai.com/privacy/) and [Terms of Use](https://openai.com/api/policies/terms/).

Some common areas you'll need to consider include data storage, data transmission, and data retention. You might also need to implement data privacy protections, such as encryption or anonymization where possible. In addition, you should follow best practices for secure coding, such as input sanitization and proper error handling.

### Safety best practices

When creating your application with our API, consider our [safety best practices](/docs/guides/safety-best-practices) to ensure your application is safe and successful. These recommendations highlight the importance of testing the product extensively, being proactive about addressing potential issues, and limiting opportunities for misuse.

Business considerations
-----------------------

As projects using AI move from prototype to production, it is important to consider how to build a great product with AI and how that ties back to your core business. We certainly don't have all the answers but a great starting place is a talk from our Developer Day where we dive into this with some of our customers:

Was this page useful?
Safety best practices
=====================

Implement safety measures like moderation and human oversight.

### Use our free Moderation API

OpenAI's [Moderation API](/docs/guides/moderation) is free-to-use and can help reduce the frequency of unsafe content in your completions. Alternatively, you may wish to develop your own content filtration system tailored to your use case.

### Adversarial testing

We recommend “red-teaming” your application to ensure it's robust to adversarial input. Test your product over a wide range of inputs and user behaviors, both a representative set and those reflective of someone trying to ‘break' your application. Does it wander off topic? Can someone easily redirect the feature via prompt injections, e.g. “ignore the previous instructions and do this instead”?

### Human in the loop (HITL)

Wherever possible, we recommend having a human review outputs before they are used in practice. This is especially critical in high-stakes domains, and for code generation. Humans should be aware of the limitations of the system, and have access to any information needed to verify the outputs (for example, if the application summarizes notes, a human should have easy access to the original notes to refer back).

### Prompt engineering

“Prompt engineering” can help constrain the topic and tone of output text. This reduces the chance of producing undesired content, even if a user tries to produce it. Providing additional context to the model (such as by giving a few high-quality examples of desired behavior prior to the new input) can make it easier to steer model outputs in desired directions.

### “Know your customer” (KYC)

Users should generally need to register and log-in to access your service. Linking this service to an existing account, such as a Gmail, LinkedIn, or Facebook log-in, may help, though may not be appropriate for all use-cases. Requiring a credit card or ID card reduces risk further.

### Constrain user input and limit output tokens

Limiting the amount of text a user can input into the prompt helps avoid prompt injection. Limiting the number of output tokens helps reduce the chance of misuse.

Narrowing the ranges of inputs or outputs, especially drawn from trusted sources, reduces the extent of misuse possible within an application.

Allowing user inputs through validated dropdown fields (e.g., a list of movies on Wikipedia) can be more secure than allowing open-ended text inputs.

Returning outputs from a validated set of materials on the backend, where possible, can be safer than returning novel generated content (for instance, routing a customer query to the best-matching existing customer support article, rather than attempting to answer the query from-scratch).

### Allow users to report issues

Users should generally have an easily-available method for reporting improper functionality or other concerns about application behavior (listed email address, ticket submission method, etc). This method should be monitored by a human and responded to as appropriate.

### Understand and communicate limitations

From hallucinating inaccurate information, to offensive outputs, to bias, and much more, language models may not be suitable for every use case without significant modifications. Consider whether the model is fit for your purpose, and evaluate the performance of the API on a wide range of potential inputs in order to identify cases where the API's performance might drop. Consider your customer base and the range of inputs that they will be using, and ensure their expectations are calibrated appropriately.

Safety and security are very important to us at OpenAI.

If in the course of your development you do notice any safety or security issues with the API or anything else related to OpenAI, please submit these through our [Coordinated Vulnerability Disclosure Program](https://openai.com/security/disclosure/).

End-user IDs
------------

Sending end-user IDs in your requests can be a useful tool to help OpenAI monitor and detect abuse. This allows OpenAI to provide your team with more actionable feedback in the event that we detect any policy violations in your application.

The IDs should be a string that uniquely identifies each user. We recommend hashing their username or email address, in order to avoid sending us any identifying information. If you offer a preview of your product to non-logged in users, you can send a session ID instead.

You can include end-user IDs in your API requests via the `user` parameter as follows:

Example: Providing a user identifer

```python
from openai import OpenAI
client = OpenAI()

response = client.chat.completions.create(
  model="gpt-4o-mini",
  messages=[
    {"role": "user", "content": "This is a test"}
  ],
  max_tokens=5,
  user="user_123456"
)
```

```bash
curl https://api.openai.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
  "model": "gpt-4o-mini",
  "messages": [
    {"role": "user", "content": "This is a test"}
  ],
  "max_tokens": 5,
  "user": "user123456"
}'
```

Was this page useful?
Prompt caching
==============

Reduce latency and cost with prompt caching.

Model prompts often contain repetitive content, like system prompts and common instructions. OpenAI routes API requests to servers that recently processed the same prompt, making it cheaper and faster than processing a prompt from scratch. This can reduce latency by up to 80% and cost by 50% for long prompts. Prompt Caching works automatically on all your API requests (no code changes required) and has no additional fees associated with it.

Prompt Caching is enabled for the following [models](/docs/models):

|Model|Text Input Cost|Audio Input Cost|
|---|---|---|
|gpt-4.5-preview|50% less|n/a|
|gpt-4o (excludes gpt-4o-2024-05-13 and chatgpt-4o-latest)|50% less|n/a|
|gpt-4o-mini|50% less|n/a|
|gpt-4o-realtime-preview|50% less|80% less|
|o1-preview|50% less|n/a|
|o1-mini|50% less|n/a|

This guide describes how prompt caching works in detail, so that you can optimize your prompts for lower latency and cost.

Structuring prompts
-------------------

Cache hits are only possible for exact prefix matches within a prompt. To realize caching benefits, place static content like instructions and examples at the beginning of your prompt, and put variable content, such as user-specific information, at the end. This also applies to images and tools, which must be identical between requests.

![Prompt Caching visualization](https://openaidevs.retool.com/api/file/8593d9bb-4edb-4eb6-bed9-62bfb98db5ee)

How it works
------------

Caching is enabled automatically for prompts that are 1024 tokens or longer. When you make an API request, the following steps occur:

1.  **Cache Lookup**: The system checks if the initial portion (prefix) of your prompt is stored in the cache.
2.  **Cache Hit**: If a matching prefix is found, the system uses the cached result. This significantly decreases latency and reduces costs.
3.  **Cache Miss**: If no matching prefix is found, the system processes your full prompt. After processing, the prefix of your prompt is cached for future requests.

Cached prefixes generally remain active for 5 to 10 minutes of inactivity. However, during off-peak periods, caches may persist for up to one hour.

Requirements
------------

Caching is available for prompts containing 1024 tokens or more, with cache hits occurring in increments of 128 tokens. Therefore, the number of cached tokens in a request will always fall within the following sequence: 1024, 1152, 1280, 1408, and so on, depending on the prompt's length.

All requests, including those with fewer than 1024 tokens, will display a `cached_tokens` field of the `usage.prompt_tokens_details` [Chat Completions object](/docs/api-reference/chat/object) indicating how many of the prompt tokens were a cache hit. For requests under 1024 tokens, `cached_tokens` will be zero.

```json
"usage": {
  "prompt_tokens": 2006,
  "completion_tokens": 300,
  "total_tokens": 2306,
  "prompt_tokens_details": {
    "cached_tokens": 1920
  },
  "completion_tokens_details": {
    "reasoning_tokens": 0,
    "accepted_prediction_tokens": 0,
    "rejected_prediction_tokens": 0
  }
}
```

### What can be cached

*   **Messages:** The complete messages array, encompassing system, user, and assistant interactions.
*   **Images:** Images included in user messages, either as links or as base64-encoded data, as well as multiple images can be sent. Ensure the detail parameter is set identically, as it impacts image tokenization.
*   **Tool use:** Both the messages array and the list of available `tools` can be cached, contributing to the minimum 1024 token requirement.
*   **Structured outputs:** The structured output schema serves as a prefix to the system message and can be cached.

### Best practices

*   Structure prompts with static or repeated content at the beginning and dynamic content at the end.
*   Monitor metrics such as cache hit rates, latency, and the percentage of tokens cached to optimize your prompt and caching strategy.
*   To increase cache hits, use longer prompts and make API requests during off-peak hours, as cache evictions are more frequent during peak times.
*   Prompts that haven't been used recently are automatically removed from the cache. To minimize evictions, maintain a consistent stream of requests with the same prompt prefix.

### Frequently asked questions

1.  **How is data privacy maintained for caches?**
    
    Prompt caches are not shared between organizations. Only members of the same organization can access caches of identical prompts.
    
2.  **Does Prompt Caching affect output token generation or the final response of the API?**
    
    Prompt Caching does not influence the generation of output tokens or the final response provided by the API. Regardless of whether caching is used, the output generated will be identical. This is because only the prompt itself is cached, while the actual response is computed anew each time based on the cached prompt.
    
3.  **Is there a way to manually clear the cache?**
    
    Manual cache clearing is not currently available. Prompts that have not been encountered recently are automatically cleared from the cache. Typical cache evictions occur after 5-10 minutes of inactivity, though sometimes lasting up to a maximum of one hour during off-peak periods.
    
4.  **Will I be expected to pay extra for writing to Prompt Caching?**
    
    No. Caching happens automatically, with no explicit action needed or extra cost paid to use the caching feature.
    
5.  **Do cached prompts contribute to TPM rate limits?**
    
    Yes, as caching does not affect rate limits.
    
6.  **Is discounting for Prompt Caching available on Scale Tier and the Batch API?**
    
    Discounting for Prompt Caching is not available on the Batch API but is available on Scale Tier. With Scale Tier, any tokens that are spilled over to the shared API will also be eligible for caching.
    
7.  **Does Prompt Caching work on Zero Data Retention requests?**
    
    Yes, Prompt Caching is compliant with existing Zero Data Retention policies.
    

Was this page useful?
Predicted Outputs
=================

Reduce latency for model responses where much of the response is known ahead of time.

**Predicted Outputs** enable you to speed up API responses from [Chat Completions](/docs/api-reference/chat/create) when many of the output tokens are known ahead of time. This is most common when you are regenerating a text or code file with minor modifications. You can provide your prediction using the [`prediction` request parameter in Chat Completions](/docs/api-reference/chat/create#chat-create-prediction).

Predicted Outputs are available today using the latest `gpt-4o` and `gpt-4o-mini` models. Read on to learn how to use Predicted Outputs to reduce latency in your applicatons.

Code refactoring example
------------------------

Predicted Outputs are particularly useful for regenerating text documents and code files with small modifications. Let's say you want the [GPT-4o model](/docs/models#gpt-4o) to refactor a piece of TypeScript code, and convert the `username` property of the `User` class to be `email` instead:

```typescript
class User {
  firstName: string = "";
  lastName: string = "";
  username: string = "";
}

export default User;
```

Most of the file will be unchanged, except for line 4 above. If you use the current text of the code file as your prediction, you can regenerate the entire file with lower latency. These time savings add up quickly for larger files.

Below is an example of using the `prediction` parameter in our SDKs to predict that the final output of the model will be very similar to our original code file, which we use as the prediction text.

Refactor a TypeScript class with a Predicted Output

```javascript
import OpenAI from "openai";

const code = `
class User {
  firstName: string = "";
  lastName: string = "";
  username: string = "";
}

export default User;
`.trim();

const openai = new OpenAI();

const refactorPrompt = `
Replace the "username" property with an "email" property. Respond only 
with code, and with no markdown formatting.
`;

const completion = await openai.chat.completions.create({
  model: "gpt-4o",
  messages: [
    {
      role: "user",
      content: refactorPrompt
    },
    {
      role: "user",
      content: code
    }
  ],
  store: true,
  prediction: {
    type: "content",
    content: code
  }
});

// Inspect returned data
console.log(completion);
console.log(completion.choices[0].message.content);
```

```python
from openai import OpenAI

code = """
class User {
  firstName: string = "";
  lastName: string = "";
  username: string = "";
}

export default User;
"""

refactor_prompt = """
Replace the "username" property with an "email" property. Respond only 
with code, and with no markdown formatting.
"""

client = OpenAI()

completion = client.chat.completions.create(
    model="gpt-4o",
    messages=[
        {
            "role": "user",
            "content": refactor_prompt
        },
        {
            "role": "user",
            "content": code
        }
    ],
    prediction={
        "type": "content",
        "content": code
    }
)

print(completion)
print(completion.choices[0].message.content)
```

```bash
curl https://api.openai.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "gpt-4o",
    "messages": [
      {
        "role": "user",
        "content": "Replace the username property with an email property. Respond only with code, and with no markdown formatting."
      },
      {
        "role": "user",
        "content": "$CODE_CONTENT_HERE"
      }
    ],
    "prediction": {
        "type": "content",
        "content": "$CODE_CONTENT_HERE"
    }
  }'
```

In addition to the refactored code, the model response will contain data that looks something like this:

```javascript
{
  id: 'chatcmpl-xxx',
  object: 'chat.completion',
  created: 1730918466,
  model: 'gpt-4o-2024-08-06',
  choices: [ /* ...actual text response here... */],
  usage: {
    prompt_tokens: 81,
    completion_tokens: 39,
    total_tokens: 120,
    prompt_tokens_details: { cached_tokens: 0, audio_tokens: 0 },
    completion_tokens_details: {
      reasoning_tokens: 0,
      audio_tokens: 0,
      accepted_prediction_tokens: 18,
      rejected_prediction_tokens: 10
    }
  },
  system_fingerprint: 'fp_159d8341cc'
}
```

Note both the `accepted_prediction_tokens` and `rejected_prediction_tokens` in the `usage` object. In this example, 18 tokens from the prediction were used to speed up the response, while 10 were rejected.

Note that any rejected tokens are still billed like other completion tokens generated by the API, so Predicted Outputs can introduce higher costs for your requests.

Streaming example
-----------------

The latency gains of Predicted Outputs are even greater when you use streaming for API responses. Here is an example of the same code refactoring use case, but using streaming in the OpenAI SDKs instead.

Predicted Outputs with streaming

```javascript
import OpenAI from "openai";

const code = `
class User {
  firstName: string = "";
  lastName: string = "";
  username: string = "";
}

export default User;
`.trim();

const openai = new OpenAI();

const refactorPrompt = `
Replace the "username" property with an "email" property. Respond only 
with code, and with no markdown formatting.
`;

const completion = await openai.chat.completions.create({
  model: "gpt-4o",
  messages: [
    {
      role: "user",
      content: refactorPrompt
    },
    {
      role: "user",
      content: code
    }
  ],
  store: true,
  prediction: {
    type: "content",
    content: code
  },
  stream: true
});

// Inspect returned data
for await (const chunk of stream) {
  process.stdout.write(chunk.choices[0]?.delta?.content || "");
}
```

```python
from openai import OpenAI

code = """
class User {
  firstName: string = "";
  lastName: string = "";
  username: string = "";
}

export default User;
"""

refactor_prompt = """
Replace the "username" property with an "email" property. Respond only 
with code, and with no markdown formatting.
"""

client = OpenAI()

stream = client.chat.completions.create(
    model="gpt-4o",
    messages=[
        {
            "role": "user",
            "content": refactor_prompt
        },
        {
            "role": "user",
            "content": code
        }
    ],
    prediction={
        "type": "content",
        "content": code
    },
    stream=True
)

for chunk in stream:
    if chunk.choices[0].delta.content is not None:
        print(chunk.choices[0].delta.content, end="")
```

Position of predicted text in response
--------------------------------------

When providing prediction text, your prediction can appear anywhere within the generated response, and still provide latency reduction for the response. Let's say your predicted text is the simple [Hono](https://hono.dev/) server shown below:

```typescript
import { serveStatic } from "@hono/node-server/serve-static";
import { serve } from "@hono/node-server";
import { Hono } from "hono";

const app = new Hono();

app.get("/api", (c) => {
  return c.text("Hello Hono!");
});

// You will need to build the client code first `pnpm run ui:build`
app.use(
  "/*",
  serveStatic({
    rewriteRequestPath: (path) => `./dist${path}`,
  })
);

const port = 3000;
console.log(`Server is running on port ${port}`);

serve({
  fetch: app.fetch,
  port,
});
```

You could prompt the model to regenerate the file with a prompt like:

```text
Add a get route to this application that responds with 
the text "hello world". Generate the entire application 
file again with this route added, and with no other 
markdown formatting.
```

The response to the prompt might look something like this:

```typescript
import { serveStatic } from "@hono/node-server/serve-static";
import { serve } from "@hono/node-server";
import { Hono } from "hono";

const app = new Hono();

app.get("/api", (c) => {
  return c.text("Hello Hono!");
});

app.get("/hello", (c) => {
  return c.text("hello world");
});

// You will need to build the client code first `pnpm run ui:build`
app.use(
  "/*",
  serveStatic({
    rewriteRequestPath: (path) => `./dist${path}`,
  })
);

const port = 3000;
console.log(`Server is running on port ${port}`);

serve({
  fetch: app.fetch,
  port,
});
```

You would still see accepted prediction tokens in the response, even though the prediction text appeared both before and after the new content added to the response:

```javascript
{
  id: 'chatcmpl-xxx',
  object: 'chat.completion',
  created: 1731014771,
  model: 'gpt-4o-2024-08-06',
  choices: [ /* completion here... */],
  usage: {
    prompt_tokens: 203,
    completion_tokens: 159,
    total_tokens: 362,
    prompt_tokens_details: { cached_tokens: 0, audio_tokens: 0 },
    completion_tokens_details: {
      reasoning_tokens: 0,
      audio_tokens: 0,
      accepted_prediction_tokens: 60,
      rejected_prediction_tokens: 0
    }
  },
  system_fingerprint: 'fp_9ee9e968ea'
}
```

This time, there were no rejected prediction tokens, because the entire content of the file we predicted was used in the final response. Nice! 🔥

Limitations
-----------

When using Predicted Outputs, you should consider the following factors and limitations.

*   Predicted Outputs are only supported with the GPT-4o and GPT-4o-mini series of models.
*   When providing a prediction, any tokens provided that are not part of the final completion are still charged at completion token rates. See the [`rejected_prediction_tokens` property of the `usage` object](/docs/api-reference/chat/object#chat/object-usage) to see how many tokens are not used in the final response.
*   The following [API parameters](/docs/api-reference/chat/create) are not supported when using Predicted Outputs:
    *   `n`: values higher than 1 are not supported
    *   `logprobs`: not supported
    *   `presence_penalty`: values greater than 0 are not supported
    *   `frequency_penalty`: values greater than 0 are not supported
    *   `audio`: Predicted Outputs are not compatible with [audio inputs and outputs](/docs/guides/audio)
    *   `modalities`: Only `text` modalities are supported
    *   `max_completion_tokens`: not supported
    *   `tools`: Function calling is not currently supported with Predicted Outputs

Was this page useful?
Model selection
===============

Choose the best model for performance and cost.

Choosing the right model, whether GPT-4o or a smaller option like GPT-4o-mini, requires balancing **accuracy**, **latency**, and **cost**. This guide explains key principles to help you make informed decisions, along with a practical example.

Core principles
---------------

The principles for model selection are simple:

*   **Optimize for accuracy first:** Optimize for accuracy until you hit your accuracy target.
*   **Optimize for cost and latency second:** Then aim to maintain accuracy with the cheapest, fastest model possible.

### 1\. Focus on accuracy first

Begin by setting a clear accuracy goal for your use case, where you're clear on the accuracy that would be "good enough" for this use case to go to production. You can accomplish this through:

*   **Setting a clear accuracy target:** Identify what your target accuracy statistic is going to be.
    *   For example, 90% of customer service calls need to be triaged correctly at the first interaction.
*   **Developing an evaluation dataset:** Create a dataset that allows you to measure the model's performance against these goals.
    *   To extend the example above, capture 100 interaction examples where we have what the user asked for, what the LLM triaged them to, what the correct triage should be, and whether this was correct or not.
*   **Using the most powerful model to optimize:** Start with the most capable model available to achieve your accuracy targets. Log all responses so we can use them for distillation of a smaller model.
    *   Use retrieval-augmented generation to optimize for accuracy
    *   Use fine-tuning to optimize for consistency and behavior

During this process, collect prompt and completion pairs for use in evaluations, few-shot learning, or fine-tuning. This practice, known as **prompt baking**, helps you produce high-quality examples for future use.

For more methods and tools here, see our [Accuracy Optimization Guide](https://platform.openai.com/docs/guides/optimizing-llm-accuracy).

#### Setting a realistic accuracy target

Calculate a realistic accuracy target by evaluating the financial impact of model decisions. For example, in a fake news classification scenario:

*   **Correctly classified news:** If the model classifies it correctly, it saves you the cost of a human reviewing it - let's assume **$50**.
*   **Incorrectly classified news:** If it falsely classifies a safe article or misses a fake news article, it may trigger a review process and possible complaint, which might cost us **$300**.

Our news classification example would need **85.8%** accuracy to cover costs, so targeting 90% or more ensures an overall return on investment. Use these calculations to set an effective accuracy target based on your specific cost structures.

### 2\. Optimize cost and latency

Cost and latency are considered secondary because if the model can’t hit your accuracy target then these concerns are moot. However, once you’ve got a model that works for your use case, you can take one of two approaches:

*   **Compare with a smaller model zero- or few-shot:** Swap out the model for a smaller, cheaper one and test whether it maintains accuracy at the lower cost and latency point.
*   **Model distillation:** Fine-tune a smaller model using the data gathered during accuracy optimization.

Cost and latency are typically interconnected; reducing tokens and requests generally leads to faster processing.

The main strategies to consider here are:

*   **Reduce requests:** Limit the number of necessary requests to complete tasks.
*   **Minimize tokens:** Lower the number of input tokens and optimize for shorter model outputs.
*   **Select a smaller model:** Use models that balance reduced costs and latency with maintained accuracy.

To dive deeper into these, please refer to our guide on [latency optimization](https://platform.openai.com/docs/guides/latency-optimization).

#### Exceptions to the rule

Clear exceptions exist for these principles. If your use case is extremely cost or latency sensitive, establish thresholds for these metrics before beginning your testing, then remove the models that exceed those from consideration. Once benchmarks are set, these guidelines will help you refine model accuracy within your constraints.

Practical example
-----------------

To demonstrate these principles, we'll develop a fake news classifier with the following target metrics:

*   **Accuracy:** Achieve 90% correct classification
*   **Cost:** Spend less than $5 per 1,000 articles
*   **Latency:** Maintain processing time under 2 seconds per article

### Experiments

We ran three experiments to reach our goal:

1.  **Zero-shot:** Used `GPT-4o` with a basic prompt for 1,000 records, but missed the accuracy target.
2.  **Few-shot learning:** Included 5 few-shot examples, meeting the accuracy target but exceeding cost due to more prompt tokens.
3.  **Fine-tuned model:** Fine-tuned `GPT-4o-mini` with 1,000 labeled examples, meeting all targets with similar latency and accuracy but significantly lower costs.

|ID|Method|Accuracy|Accuracy target|Cost|Cost target|Avg. latency|Latency target|
|---|---|---|---|---|---|---|---|
|1|gpt-4o zero-shot|84.5%||$1.72||< 1s||
|2|gpt-4o few-shot (n=5)|91.5%|✓|$11.92||< 1s|✓|
|3|gpt-4o-mini fine-tuned w/ 1000 examples|91.5%|✓|$0.21|✓|< 1s|✓|

Conclusion
----------

By switching from `gpt-4o` to `gpt-4o-mini` with fine-tuning, we achieved **equivalent performance for less than 2%** of the cost, using only 1,000 labeled examples.

This process is important - you often can’t jump right to fine-tuning because you don’t know whether fine-tuning is the right tool for the optimization you need, or you don’t have enough labeled examples. Use `gpt-4o` to achieve your accuracy targets, and curate a good training set - then go for a smaller, more efficient model with fine-tuning.

Was this page useful?
Latency optimization
====================

Improve latency across a wide variety of LLM-related use cases.

This guide covers the core set of principles you can apply to improve latency across a wide variety of LLM-related use cases. These techniques come from working with a wide range of customers and developers on production applications, so they should apply regardless of what you're building – from a granular workflow to an end-to-end chatbot.

While there's many individual techniques, we'll be grouping them into **seven principles** meant to represent a high-level taxonomy of approaches for improving latency.

At the end, we'll walk through an [example](#example) to see how they can be applied.

### Seven principles

1.  [Process tokens faster.](#process-tokens-faster)
2.  [Generate fewer tokens.](#generate-fewer-tokens)
3.  [Use fewer input tokens.](#use-fewer-input-tokens)
4.  [Make fewer requests.](#make-fewer-requests)
5.  [Parallelize.](#parallelize)
6.  [Make your users wait less.](#make-your-users-wait-less)
7.  [Don't default to an LLM.](#don-t-default-to-an-llm)

Process tokens faster
---------------------

**Inference speed** is probably the first thing that comes to mind when addressing latency (but as you'll see soon, it's far from the only one). This refers to the actual **rate at which the LLM processes tokens**, and is often measured in TPM (tokens per minute) or TPS (tokens per second).

The main factor that influences inference speed is **model size** – smaller models usually run faster (and cheaper), and when used correctly can even outperform larger models. To maintain high quality performance with smaller models you can explore:

*   using a longer, [more detailed prompt](/docs/guides/prompt-engineering#tactic-specify-the-steps-required-to-complete-a-task),
*   adding (more) [few-shot examples](/docs/guides/prompt-engineering#tactic-provide-examples), or
*   [fine-tuning](/docs/guides/fine-tuning) / distillation.

You can also employ inference optimizations like our [**Predicted outputs**](/docs/guides/predicted-outputs) feature. Predicted outputs let you significantly reduce latency of a generation when you know most of the output ahead of time, such as code editing tasks. By giving the model a prediction, the LLM can focus more on the actual changes, and less on the content that will remain the same.

Deep dive

Compute capacity & additional inference optimizations

Generate fewer tokens
---------------------

Generating tokens is almost always the highest latency step when using an LLM: as a general heuristic, **cutting 50% of your output tokens may cut ~50% your latency**. The way you reduce your output size will depend on output type:

If you're generating **natural language**, simply **asking the model to be more concise** ("under 20 words" or "be very brief") may help. You can also use few shot examples and/or fine-tuning to teach the model shorter responses.

If you're generating **structured output**, try to **minimize your output syntax** where possible: shorten function names, omit named arguments, coalesce parameters, etc.

Finally, while not common, you can also use `max_tokens` or `stop_tokens` to end your generation early.

Always remember: an output token cut is a (milli)second earned!

Use fewer input tokens
----------------------

While reducing the number of input tokens does result in lower latency, this is not usually a significant factor – **cutting 50% of your prompt may only result in a 1-5% latency improvement**. Unless you're working with truly massive context sizes (documents, images), you may want to spend your efforts elsewhere.

That being said, if you _are_ working with massive contexts (or you're set on squeezing every last bit of performance _and_ you've exhausted all other options) you can use the following techniques to reduce your input tokens:

*   **Fine-tuning the model**, to replace the need for lengthy instructions / examples.
*   **Filtering context input**, like pruning RAG results, cleaning HTML, etc.
*   **Maximize shared prompt prefix**, by putting dynamic portions (e.g. RAG results, history, etc) later in the prompt. This makes your request more [KV cache](https://medium.com/@joaolages/kv-caching-explained-276520203249)\-friendly (which most LLM providers use) and means fewer input tokens are processed on each request.

Check out our docs to learn more about how [prompt caching](/docs/guides/prompt-engineering#prompt-caching) works.

Make fewer requests
-------------------

Each time you make a request you incur some round-trip latency – this can start to add up.

If you have sequential steps for the LLM to perform, instead of firing off one request per step consider **putting them in a single prompt and getting them all in a single response**. You'll avoid the additional round-trip latency, and potentially also reduce complexity of processing multiple responses.

An approach to doing this is by collecting your steps in an enumerated list in the combined prompt, and then requesting the model to return the results in named fields in a JSON. This way you can easily parse out and reference each result!

Parallelize
-----------

Parallelization can be very powerful when performing multiple steps with an LLM.

If the steps **are _not_ strictly sequential**, you can **split them out into parallel calls**. Two shirts take just as long to dry as one.

If the steps **_are_ strictly sequential**, however, you might still be able to **leverage speculative execution**. This is particularly effective for classification steps where one outcome is more likely than the others (e.g. moderation).

1.  Start step 1 & step 2 simultaneously (e.g. input moderation & story generation)
2.  Verify the result of step 1
3.  If result was not the expected, cancel step 2 (and retry if necessary)

If your guess for step 1 is right, then you essentially got to run it with zero added latency!

Make your users wait less
-------------------------

There's a huge difference between **waiting** and **watching progress happen** – make sure your users experience the latter. Here are a few techniques:

*   **Streaming**: The single most effective approach, as it cuts the _waiting_ time to a second or less. (ChatGPT would feel pretty different if you saw nothing until each response was done.)
*   **Chunking**: If your output needs further processing before being shown to the user (moderation, translation) consider **processing it in chunks** instead of all at once. Do this by streaming to your backend, then sending processed chunks to your frontend.
*   **Show your steps**: If you're taking multiple steps or using tools, surface this to the user. The more real progress you can show, the better.
*   **Loading states**: Spinners and progress bars go a long way.

Note that while **showing your steps & having loading states** have a mostly psychological effect, **streaming & chunking** genuinely do reduce overall latency once you consider the app + user system: the user will finish reading a response sooner.

Don't default to an LLM
-----------------------

LLMs are extremely powerful and versatile, and are therefore sometimes used in cases where a **faster classical method** would be more appropriate. Identifying such cases may allow you to cut your latency significantly. Consider the following examples:

*   **Hard-coding:** If your **output** is highly constrained, you may not need an LLM to generate it. Action confirmations, refusal messages, and requests for standard input are all great candidates to be hard-coded. (You can even use the age-old method of coming up with a few variations for each.)
*   **Pre-computing:** If your **input** is constrained (e.g. category selection) you can generate multiple responses in advance, and just make sure you never show the same one to a user twice.
*   **Leveraging UI:** Summarized metrics, reports, or search results are sometimes better conveyed with classical, bespoke UI components rather than LLM-generated text.
*   **Traditional optimization techniques:** An LLM application is still an application; binary search, caching, hash maps, and runtime complexity are all _still_ useful in a world of LLMs.

Example
-------

Let's now look at a sample application, identify potential latency optimizations, and propose some solutions!

We'll be analyzing the architecture and prompts of a hypothetical customer service bot inspired by real production applications. The [architecture and prompts](#architecture-and-prompts) section sets the stage, and the [analysis and optimizations](#analysis-and-optimizations) section will walk through the latency optimization process.

You'll notice this example doesn't cover every single principle, much like real-world use cases don't require applying every technique.

### Architecture and prompts

The following is the **initial architecture** for a hypothetical **customer service bot**. This is what we'll be making changes to.

![Assistants object architecture diagram](https://cdn.openai.com/API/docs/images/diagram-latency-customer-service-0.png)

At a high level, the diagram flow describes the following process:

1.  A user sends a message as part of an ongoing conversation.
2.  The last message is turned into a **self-contained query** (see examples in prompt).
3.  We determine whether or not **additional (retrieved) information is required** to respond to that query.
4.  **Retrieval** is performed, producing search results.
5.  The assistant **reasons** about the user's query and search results, and **produces a response**.
6.  The response is sent back to the user.

Below are the prompts used in each part of the diagram. While they are still only hypothetical and simplified, they are written with the same structure and wording that you would find in a production application.

Places where you see placeholders like "**\[user input here\]**" represent dynamic portions, that would be replaced by actual data at runtime.

Query contextualization prompt

Re-writes user query to be a self-contained search query.

SYSTEM

Given the previous conversation, re-write the last user query so it contains all necessary context. # Example History: \[{user: "What is your return policy?"},{assistant: "..."}\] User Query: "How long does it cover?" Response: "How long does the return policy cover?" # Conversation \[last 3 messages of conversation\] # User Query \[last user query\]

USER

\[JSON-formatted input conversation here\]

Retrieval check prompt

Determines whether a query requires performing retrieval to respond.

SYSTEM

Given a user query, determine whether it requires doing a realtime lookup to respond to. # Examples User Query: "How can I return this item after 30 days?" Response: "true" User Query: "Thank you!" Response: "false"

USER

\[input user query here\]

Assistant prompt

Fills the fields of a JSON to reason through a pre-defined set of steps to produce a final response given a user conversation and relevant retrieved information.

SYSTEM

You are a helpful customer service bot. Use the result JSON to reason about each user query - use the retrieved context. # Example User: "My computer screen is cracked! I want it fixed now!!!" Assistant Response: { "message\_is\_conversation\_continuation": "True", "number\_of\_messages\_in\_conversation\_so\_far": "1", "user\_sentiment": "Aggravated", "query\_type": "Hardware Issue", "response\_tone": "Validating and solution-oriented", "response\_requirements": "Propose options for repair or replacement.", "user\_requesting\_to\_talk\_to\_human": "False", "enough\_information\_in\_context": "True", "response": "..." }

USER

\# Relevant Information \` \` \` \[retrieved context\] \` \` \`

USER

\[input user query here\]

### Analysis and optimizations

#### Part 1: Looking at retrieval prompts

Looking at the architecture, the first thing that stands out is the **consecutive GPT-4 calls** - these hint at a potential inefficiency, and can often be replaced by a single call or parallel calls.

![Assistants object architecture diagram](https://cdn.openai.com/API/docs/images/diagram-latency-customer-service-2.png)

In this case, since the check for retrieval requires the contextualized query, let's **combine them into a single prompt** to [make fewer requests](#make-fewer-requests).

![Assistants object architecture diagram](https://cdn.openai.com/API/docs/images/diagram-latency-customer-service-3.png)

Combined query contextualization and retrieval check prompt

**What changed?** Before, we had one prompt to re-write the query and one to determine whether this requires doing a retrieval lookup. Now, this combined prompt does both. Specifically, notice the updated instruction in the first line of the prompt, and the updated output JSON:

```jsx
{
  query:"[contextualized query]",
  retrieval:"[true/false - whether retrieval is required]"
}
```

SYSTEM

Given the previous conversation, re-write the last user query so it contains all necessary context. Then, determine whether the full request requires doing a realtime lookup to respond to. Respond in the following form: { query:"\[contextualized query\]", retrieval:"\[true/false - whether retrieval is required\]" } # Examples History: \[{user: "What is your return policy?"},{assistant: "..."}\] User Query: "How long does it cover?" Response: {query: "How long does the return policy cover?", retrieval: "true"} History: \[{user: "How can I return this item after 30 days?"},{assistant: "..."}\] User Query: "Thank you!" Response: {query: "Thank you!", retrieval: "false"} # Conversation \[last 3 messages of conversation\] # User Query \[last user query\]

USER

\[JSON-formatted input conversation here\]

  

Actually, adding context and determining whether to retrieve are very straightforward and well defined tasks, so we can likely use a **smaller, fine-tuned model** instead. Switching to GPT-3.5 will let us [process tokens faster](#process-tokens-faster).

![Assistants object architecture diagram](https://cdn.openai.com/API/docs/images/diagram-latency-customer-service-4.png)

#### Part 2: Analyzing the assistant prompt

Let's now direct our attention to the Assistant prompt. There seem to be many distinct steps happening as it fills the JSON fields – this could indicate an opportunity to [parallelize](#parallelize).

![Assistants object architecture diagram](https://cdn.openai.com/API/docs/images/diagram-latency-customer-service-5.png)

However, let's pretend we have run some tests and discovered that splitting the reasoning steps in the JSON produces worse responses, so we need to explore different solutions.

**Could we use a fine-tuned GPT-3.5 instead of GPT-4?** Maybe – but in general, open-ended responses from assistants are best left to GPT-4 so it can better handle a greater range of cases. That being said, looking at the reasoning steps themselves, they may not all require GPT-4 level reasoning to produce. The well defined, limited scope nature makes them and **good potential candidates for fine-tuning**.

```jsx
{
  "message_is_conversation_continuation": "True", // <-
  "number_of_messages_in_conversation_so_far": "1", // <-
  "user_sentiment": "Aggravated", // <-
  "query_type": "Hardware Issue", // <-
  "response_tone": "Validating and solution-oriented", // <-
  "response_requirements": "Propose options for repair or replacement.", // <-
  "user_requesting_to_talk_to_human": "False", // <-
  "enough_information_in_context": "True", // <-
  "response": "..." // X -- benefits from GPT-4
}
```

This opens up the possibility of a trade-off. Do we keep this as a **single request entirely generated by GPT-4**, or **split it into two sequential requests** and use GPT-3.5 for all but the final response? We have a case of conflicting principles: the first option lets us [make fewer requests](#make-fewer-requests), but the second may let us [process tokens faster](#1-process-tokens-faster).

As with many optimization tradeoffs, the answer will depend on the details. For example:

*   The proportion of tokens in the `response` vs the other fields.
*   The average latency decrease from processing most fields faster.
*   The average latency _increase_ from doing two requests instead of one.

The conclusion will vary by case, and the best way to make the determiation is by testing this with production examples. In this case let's pretend the tests indicated it's favorable to split the prompt in two to [process tokens faster](#process-tokens-faster).

![Assistants object architecture diagram](https://cdn.openai.com/API/docs/images/diagram-latency-customer-service-6.png)

**Note:** We'll be grouping `response` and `enough_information_in_context` together in the second prompt to avoid passing the retrieved context to both new prompts.

Assistants prompt - reasoning

This prompt will be passed to GPT-3.5 and can be fine-tuned on curated examples.

**What changed?** The "enough\_information\_in\_context" and "response" fields were removed, and the retrieval results are no longer loaded into this prompt.

SYSTEM

You are a helpful customer service bot. Based on the previous conversation, respond in a JSON to determine the required fields. # Example User: "My freaking computer screen is cracked!" Assistant Response: { "message\_is\_conversation\_continuation": "True", "number\_of\_messages\_in\_conversation\_so\_far": "1", "user\_sentiment": "Aggravated", "query\_type": "Hardware Issue", "response\_tone": "Validating and solution-oriented", "response\_requirements": "Propose options for repair or replacement.", "user\_requesting\_to\_talk\_to\_human": "False", }

Assistants prompt - response

This prompt will be processed by GPT-4 and will receive the reasoning steps determined in the prior prompt, as well as the results from retrieval.

**What changed?** All steps were removed except for "enough\_information\_in\_context" and "response". Additionally, the JSON we were previously filling in as output will be passed in to this prompt.

SYSTEM

You are a helpful customer service bot. Use the retrieved context, as well as these pre-classified fields, to respond to the user's query. # Reasoning Fields \` \` \` \[reasoning json determined in previous GPT-3.5 call\] \` \` \` # Example User: "My freaking computer screen is cracked!" Assistant Response: { "enough\_information\_in\_context": "True", "response": "..." }

USER

\# Relevant Information \` \` \` \[retrieved context\] \` \` \`

  

In fact, now that the reasoning prompt does not depend on the retrieved context we can [parallelize](#parallelize) and fire it off at the same time as the retrieval prompts.

![Assistants object architecture diagram](https://cdn.openai.com/API/docs/images/diagram-latency-customer-service-6b.png)

#### Part 3: Optimizing the structured output

Let's take another look at the reasoning prompt.

![Assistants object architecture diagram](https://cdn.openai.com/API/docs/images/diagram-latency-customer-service-7b.png)

Taking a closer look at the reasoning JSON you may notice the field names themselves are quite long.

```jsx
{
  "message_is_conversation_continuation": "True", // <-
  "number_of_messages_in_conversation_so_far": "1", // <-
  "user_sentiment": "Aggravated", // <-
  "query_type": "Hardware Issue", // <-
  "response_tone": "Validating and solution-oriented", // <-
  "response_requirements": "Propose options for repair or replacement.", // <-
  "user_requesting_to_talk_to_human": "False", // <-
}
```

By making them shorter and moving explanations to the comments we can [generate fewer tokens](#generate-fewer-tokens).

```jsx
{
  "cont": "True", // whether last message is a continuation
  "n_msg": "1", // number of messages in the continued conversation
  "tone_in": "Aggravated", // sentiment of user query
  "type": "Hardware Issue", // type of the user query
  "tone_out": "Validating and solution-oriented", // desired tone for response
  "reqs": "Propose options for repair or replacement.", // response requirements
  "human": "False", // whether user is expressing want to talk to human
}
```

![Assistants object architecture diagram](https://cdn.openai.com/API/docs/images/diagram-latency-customer-service-8b.png)

This small change removed 19 output tokens. While with GPT-3.5 this may only result in a few millisecond improvement, with GPT-4 this could shave off up to a second.

![Assistants object architecture diagram](https://cdn.openai.com/API/docs/images/token-counts-latency-customer-service-large.png)

You might imagine, however, how this can have quite a significant impact for larger model outputs.

We could go further and use single chatacters for the JSON fields, or put everything in an array, but this may start to hurt our response quality. The best way to know, once again, is through testing.

#### Example wrap-up

Let's review the optimizations we implemented for the customer service bot example:

![Assistants object architecture diagram](https://cdn.openai.com/API/docs/images/diagram-latency-customer-service-11b.png)

1.  **Combined** query contextualization and retrieval check steps to [make fewer requests](#make-fewer-requests).
2.  For the new prompt, **switched to a smaller, fine-tuned GPT-3.5** to [process tokens faster](process-tokens-faster).
3.  Split the assistant prompt in two, **switching to a smaller, fine-tuned GPT-3.5** for the reasoning, again to [process tokens faster](#process-tokens-faster).
4.  [Parallelized](#parallelize) the retrieval checks and the reasoning steps.
5.  **Shortened reasoning field names** and moved comments into the prompt, to [generate fewer tokens](#generate-fewer-tokens).

Was this page useful?
Optimizing LLM Accuracy
=======================

Maximize correctness and consistent behavior when working with LLMs.

### How to maximize correctness and consistent behavior when working with LLMs

Optimizing LLMs is hard.

We've worked with many developers across both start-ups and enterprises, and the reason optimization is hard consistently boils down to these reasons:

*   Knowing **how to start** optimizing accuracy
*   **When to use what** optimization method
*   What level of accuracy is **good enough** for production

This paper gives a mental model for how to optimize LLMs for accuracy and behavior. We’ll explore methods like prompt engineering, retrieval-augmented generation (RAG) and fine-tuning. We’ll also highlight how and when to use each technique, and share a few pitfalls.

As you read through, it's important to mentally relate these principles to what accuracy means for your specific use case. This may seem obvious, but there is a difference between producing a bad copy that a human needs to fix vs. refunding a customer $1000 rather than $100. You should enter any discussion on LLM accuracy with a rough picture of how much a failure by the LLM costs you, and how much a success saves or earns you - this will be revisited at the end, where we cover how much accuracy is “good enough” for production.

LLM optimization context
------------------------

Many “how-to” guides on optimization paint it as a simple linear flow - you start with prompt engineering, then you move on to retrieval-augmented generation, then fine-tuning. However, this is often not the case - these are all levers that solve different things, and to optimize in the right direction you need to pull the right lever.

It is useful to frame LLM optimization as more of a matrix:

![Accuracy mental model diagram](https://cdn.openai.com/API/docs/images/diagram-optimizing-accuracy-01.png)

The typical LLM task will start in the bottom left corner with prompt engineering, where we test, learn, and evaluate to get a baseline. Once we’ve reviewed those baseline examples and assessed why they are incorrect, we can pull one of our levers:

*   **Context optimization:** You need to optimize for context when 1) the model lacks contextual knowledge because it wasn’t in its training set, 2) its knowledge is out of date, or 3) it requires knowledge of proprietary information. This axis maximizes **response accuracy**.
*   **LLM optimization:** You need to optimize the LLM when 1) the model is producing inconsistent results with incorrect formatting, 2) the tone or style of speech is not correct, or 3) the reasoning is not being followed consistently. This axis maximizes **consistency of behavior**.

In reality this turns into a series of optimization steps, where we evaluate, make a hypothesis on how to optimize, apply it, evaluate, and re-assess for the next step. Here’s an example of a fairly typical optimization flow:

![Accuracy mental model journey diagram](https://cdn.openai.com/API/docs/images/diagram-optimizing-accuracy-02.png)

In this example, we do the following:

*   Begin with a prompt, then evaluate its performance
*   Add static few-shot examples, which should improve consistency of results
*   Add a retrieval step so the few-shot examples are brought in dynamically based on the question - this boosts performance by ensuring relevant context for each input
*   Prepare a dataset of 50+ examples and fine-tune a model to increase consistency
*   Tune the retrieval and add a fact-checking step to find hallucinations to achieve higher accuracy
*   Re-train the fine-tuned model on the new training examples which include our enhanced RAG inputs

This is a fairly typical optimization pipeline for a tough business problem - it helps us decide whether we need more relevant context or if we need more consistent behavior from the model. Once we make that decision, we know which lever to pull as our first step toward optimization.

Now that we have a mental model, let’s dive into the methods for taking action on all of these areas. We’ll start in the bottom-left corner with Prompt Engineering.

### Prompt engineering

Prompt engineering is typically the best place to start\*\*. It is often the only method needed for use cases like summarization, translation, and code generation where a zero-shot approach can reach production levels of accuracy and consistency.

This is because it forces you to define what accuracy means for your use case - you start at the most basic level by providing an input, so you need to be able to judge whether or not the output matches your expectations. If it is not what you want, then the reasons **why** will show you what to use to drive further optimizations.

To achieve this, you should always start with a simple prompt and an expected output in mind, and then optimize the prompt by adding **context**, **instructions**, or **examples** until it gives you what you want.

#### Optimization

To optimize your prompts, I’ll mostly lean on strategies from the [Prompt Engineering guide](https://platform.openai.com/docs/guides/prompt-engineering) in the OpenAI API documentation. Each strategy helps you tune Context, the LLM, or both:

|Strategy|Context optimization|LLM optimization|
|---|---|---|
|Write clear instructions||X|
|Split complex tasks into simpler subtasks|X|X|
|Give GPTs time to "think"||X|
|Test changes systematically|X|X|
|Provide reference text|X||
|Use external tools|X||

These can be a little difficult to visualize, so we’ll run through an example where we test these out with a practical example. Let’s use gpt-4-turbo to correct Icelandic sentences to see how this can work.

Prompt engineering for language corrections

The [Icelandic Errors Corpus](https://repository.clarin.is/repository/xmlui/handle/20.500.12537/105) contains combinations of an Icelandic sentence with errors, and the corrected version of that sentence. We’ll use the baseline GPT-4 model to try to solve this task, and then apply different optimization techniques to see how we can improve the model’s performance.

Given an Icelandic sentence, we want the model to return a corrected version of the sentence. We’ll use Bleu score to measure the relative quality of the translation.

|system|user|ground_truth|assistant|BLEU|
|---|---|---|---|---|
|The following sentences contain Icelandic sentences which may include errors. Please correct these errors using as few word changes as possible.|Sörvistölur eru nær hálsi og skartgripir kvenna á brjótsti.|Sörvistölur eru nær hálsi og skartgripir kvenna á brjósti.|Sörvistölur eru nær hálsi og skartgripir kvenna á brjósti.|1.0|

We perform a first attempt with GPT-4 with no examples, and it performs decently, getting a BLEU score of 62. We’ll now add some few-shot examples and see whether we can teach the model the style we’re looking for by showing rather than telling. An example looks like this:

SYSTEM

The following sentences contain Icelandic sentences which may include errors. Please correct these errors using as few word changes as possible. # Examples

USER

"Stofnendurnir séu margir og eru fulltrúar hennar frá Englandi, Grikklandi, Rússlandi, Svíþjóð og fleiri löndum Evrópu."

ASSISTANT

"Hann segir að stofnendur leynireglunnar séu margir og að fulltrúar hennar séu frá Englandi, Grikklandi, Rússlandi, Svíþjóð og fleiri löndum Evrópu."

USER

"Helsta fæða bjúgorma eru hægfara lífverur sem eru á sama búsvæði og bjúgormarnir, oft smærri ormar eins og burstormar (fræðiheiti: Polychatete)."

ASSISTANT

"Helsta fæða bjúgorma eru hægfara lífverur sem eru á sama búsvæði og bjúgormarnir, oft smærri ormar eins og burstaormar (fræðiheiti: Polychatete)."

USER

"Sörvistölur eru nær hálsi og skartgripir kvenna á brjótsti."

ASSISTANT

"Sörvistölur eru nær hálsi og skartgripir kvenna á brjósti."

USER

\[input user query here\]

The overall translation quality is better, showing an improvement to a Bleu score of **70 (+8%)**. This is pretty good, and shows us that giving the model examples of the task is helping it to learn.

This tells us that it is the **behavior** of the model that we need to optimize - it already has the knowledge that it needs to solve the problem, so providing many more examples may be the optimization we need.

We’ll revisit this later in the paper to test how our more advanced optimization methods play with this use case.

We’ve seen that prompt engineering is a great place to start, and that with the right tuning methods we can push the performance pretty far.

However, the biggest issue with prompt engineering is that it often doesn’t scale - we either need dynamic context to be fed to allow the model to deal with a wider range of problems than we can deal with through adding content to the context, or we need more consistent behavior than we can achieve with few-shot examples.

Deep dive

Using long context to scale prompt engineering

So how far can you really take prompt engineering? The answer is that it depends, and the way you make your decision is through evaluations.

### Evaluation

This is why **a good prompt with an evaluation set of questions and ground truth answers** is the best output from this stage. If we have a set of 20+ questions and answers, and we have looked into the details of the failures and have a hypothesis of why they’re occurring, then we’ve got the right baseline to take on more advanced optimization methods.

Before you move on to more sophisticated optimization methods, it's also worth considering how to automate this evaluation to speed up your iterations. Some common practices we’ve seen be effective here are:

*   Using approaches like [ROUGE](https://aclanthology.org/W04-1013/) or [BERTScore](https://arxiv.org/abs/1904.09675) to provide a finger-in-the-air judgment. This doesn’t correlate that closely with human reviewers, but can give a quick and effective measure of how much an iteration changed your model outputs.
*   Using [GPT-4](https://arxiv.org/pdf/2303.16634.pdf) as an evaluator as outlined in the G-Eval paper, where you provide the LLM a scorecard to assess the output as objectively as possible.

If you want to dive deeper on these, check out [this cookbook](https://cookbook.openai.com/examples/evaluation/how_to_eval_abstractive_summarization) which takes you through all of them in practice.

Understanding the tools
-----------------------

So you’ve done prompt engineering, you’ve got an eval set, and your model is still not doing what you need it to do. The most important next step is to diagnose where it is failing, and what tool works best to improve it.

Here is a basic framework for doing so:

![Classifying memory problem diagram](https://cdn.openai.com/API/docs/images/diagram-optimizing-accuracy-03.png)

You can think of framing each failed evaluation question as an **in-context** or **learned** memory problem. As an analogy, imagine writing an exam. There are two ways you can ensure you get the right answer:

*   You attend class for the last 6 months, where you see many repeated examples of how a particular concept works. This is **learned** memory - you solve this with LLMs by showing examples of the prompt and the response you expect, and the model learning from those.
*   You have the textbook with you, and can look up the right information to answer the question with. This is **in-context** memory - we solve this in LLMs by stuffing relevant information into the context window, either in a static way using prompt engineering, or in an industrial way using RAG.

These two optimization methods are **additive, not exclusive** - they stack, and some use cases will require you to use them together to use optimal performance.

Let’s assume that we’re facing a short-term memory problem - for this we’ll use RAG to solve it.

### Retrieval-augmented generation (RAG)

RAG is the process of **R**etrieving content to **A**ugment your LLM’s prompt before **G**enerating an answer. It is used to give the model **access to domain-specific context** to solve a task.

RAG is an incredibly valuable tool for increasing the accuracy and consistency of an LLM - many of our largest customer deployments at OpenAI were done using only prompt engineering and RAG.

![RAG diagram](https://cdn.openai.com/API/docs/images/diagram-optimizing-accuracy-04.png)

In this example we have embedded a knowledge base of statistics. When our user asks a question, we embed that question and retrieve the most relevant content from our knowledge base. This is presented to the model, which answers the question.

RAG applications introduce a new axis we need to optimize against, which is retrieval. For our RAG to work, we need to give the right context to the model, and then assess whether the model is answering correctly. I’ll frame these in a grid here to show a simple way to think about evaluation with RAG:

![RAG evaluation diagram](https://cdn.openai.com/API/docs/images/diagram-optimizing-accuracy-05.png)

You have two areas your RAG application can break down:

|Area|Problem|Resolution|
|---|---|---|
|Retrieval|You can supply the wrong context, so the model can’t possibly answer, or you can supply too much irrelevant context, which drowns out the real information and causes hallucinations.|Optimizing your retrieval, which can include:- Tuning the search to return the right results.- Tuning the search to include less noise.- Providing more information in each retrieved resultThese are just examples, as tuning RAG performance is an industry into itself, with libraries like LlamaIndex and LangChain giving many approaches to tuning here.|
|LLM|The model can also get the right context and do the wrong thing with it.|Prompt engineering by improving the instructions and method the model uses, and, if showing it examples increases accuracy, adding in fine-tuning|

The key thing to take away here is that the principle remains the same from our mental model at the beginning - you evaluate to find out what has gone wrong, and take an optimization step to fix it. The only difference with RAG is you now have the retrieval axis to consider.

While useful, RAG only solves our in-context learning issues - for many use cases, the issue will be ensuring the LLM can learn a task so it can perform it consistently and reliably. For this problem we turn to fine-tuning.

### Fine-tuning

To solve a learned memory problem, many developers will continue the training process of the LLM on a smaller, domain-specific dataset to optimize it for the specific task. This process is known as **fine-tuning**.

Fine-tuning is typically performed for one of two reasons:

*   **To improve model accuracy on a specific task:** Training the model on task-specific data to solve a learned memory problem by showing it many examples of that task being performed correctly.
*   **To improve model efficiency:** Achieve the same accuracy for less tokens or by using a smaller model.

The fine-tuning process begins by preparing a dataset of training examples - this is the most critical step, as your fine-tuning examples must exactly represent what the model will see in the real world.

Many customers use a process known as **prompt baking**, where you extensively log your prompt inputs and outputs during a pilot. These logs can be pruned into an effective training set with realistic examples.

![Fine-tuning process diagram](https://cdn.openai.com/API/docs/images/diagram-optimizing-accuracy-06.png)

Once you have this clean set, you can train a fine-tuned model by performing a **training** run - depending on the platform or framework you’re using for training you may have hyperparameters you can tune here, similar to any other machine learning model. We always recommend maintaining a hold-out set to use for **evaluation** following training to detect overfitting. For tips on how to construct a good training set you can check out the [guidance](/docs/guides/fine-tuning#analyzing-your-fine-tuned-model) in our Fine-tuning documentation. Once training is completed, the new, fine-tuned model is available for inference.

For optimizing fine-tuning we’ll focus on best practices we observe with OpenAI’s model customization offerings, but these principles should hold true with other providers and OSS offerings. The key practices to observe here are:

*   **Start with prompt-engineering:** Have a solid evaluation set from prompt engineering which you can use as a baseline. This allows a low-investment approach until you’re confident in your base prompt.
*   **Start small, focus on quality:** Quality of training data is more important than quantity when fine-tuning on top of a foundation model. Start with 50+ examples, evaluate, and then dial your training set size up if you haven’t yet hit your accuracy needs, and if the issues causing incorrect answers are due to consistency/behavior and not context.
*   **Ensure your examples are representative:** One of the most common pitfalls we see is non-representative training data, where the examples used for fine-tuning differ subtly in formatting or form from what the LLM sees in production. For example, if you have a RAG application, fine-tune the model with RAG examples in it so it isn’t learning how to use the context zero-shot.

### All of the above

These techniques stack on top of each other - if your early evals show issues with both context and behavior, then it's likely you may end up with fine-tuning + RAG in your production solution. This is ok - these stack to balance the weaknesses of both approaches. Some of the main benefits are:

*   Using fine-tuning to **minimize the tokens** used for prompt engineering, as you replace instructions and few-shot examples with many training examples to ingrain consistent behaviour in the model.
*   **Teaching complex behavior** using extensive fine-tuning
*   Using RAG to **inject context**, more recent content or any other specialized context required for your use cases

Using these tools to improve language translation

We’ll continue building on the Icelandic correction example we used above. We’ll test out the following approaches:

*   Our original hypothesis was that this was a behavior optimization problem, so our first step will be to fine-tune a model. We’ll try both gpt-3.5-turbo and gpt-4 here.
*   We’ll also try RAG - in this instance our hypothesis is that relevant examples might give additional context which could help the model solve the problem, but this is a lower confidence optimization.

#### Fine-tuning

To fine-tune for our use-case we’ll use a dataset of 1000 examples similar to our few-shot examples above:

SYSTEM

The following sentences contain Icelandic sentences which may include errors. Please correct these errors using as few word changes as possible.

USER

"Hið sameinaða fyrirtæki verður einn af stærstu bílaframleiðendum í heiminum."

ASSISTANT

"Hið sameinaða fyrirtæki verður einn af stærstu bílaframleiðendum heims."

We use these 1000 examples to train both gpt-3.5-turbo and gpt-4 fine-tuned models, and rerun our evaluation on our validation set. This confirmed our hypothesis - we got a meaningful bump in performance with both, with even the 3.5 model outperforming few-shot gpt-4 by 8 points:

|Run|Method|Bleu Score|
|---|---|---|
|1|gpt-4 with zero-shot|62|
|2|gpt-4 with 3 few-shot examples|70|
|3|gpt-3.5-turbo fine-tuned with 1000 examples|78|
|4|gpt-4 fine-tuned with 1000 examples|87|

Great, this is starting to look like production level accuracy for our use case. However, let's test whether we can squeeze a little more performance out of our pipeline by adding some relevant RAG examples to the prompt for in-context learning.

#### RAG + Fine-tuning

Our final optimization adds 1000 examples from outside of the training and validation sets which are embedded and placed in a vector database. We then run a further test with our gpt-4 fine-tuned model, with some perhaps surprising results:

![Icelandic case study diagram](https://cdn.openai.com/API/docs/images/diagram-optimizing-accuracy-07.png) _Bleu Score per tuning method (out of 100)_

RAG actually **decreased** accuracy, dropping four points from our GPT-4 fine-tuned model to 83.

This illustrates the point that you use the right optimization tool for the right job - each offers benefits and risks that we manage with evaluations and iterative changes. The behavior we witnessed in our evals and from what we know about this question told us that this is a behavior optimization problem where additional context will not necessarily help the model. This was borne out in practice - RAG actually confounded the model by giving it extra noise when it had already learned the task effectively through fine-tuning.

We now have a model that should be close to production-ready, and if we want to optimize further we can consider a wider diversity and quantity of training examples.

Now you should have an appreciation for RAG and fine-tuning, and when each is appropriate. The last thing you should appreciate with these tools is that once you introduce them there is a trade-off here in our speed to iterate:

*   For RAG you need to tune the retrieval as well as LLM behavior
*   With fine-tuning you need to rerun the fine-tuning process and manage your training and validation sets when you do additional tuning.

Both of these can be time-consuming and complex processes, which can introduce regression issues as your LLM application becomes more complex. If you take away one thing from this paper, let it be to squeeze as much accuracy out of basic methods as you can before reaching for more complex RAG or fine-tuning - let your accuracy target be the objective, not jumping for RAG + FT because they are perceived as the most sophisticated.

How much accuracy is “good enough” for production
-------------------------------------------------

Tuning for accuracy can be a never-ending battle with LLMs - they are unlikely to get to 99.999% accuracy using off-the-shelf methods. This section is all about deciding when is enough for accuracy - how do you get comfortable putting an LLM in production, and how do you manage the risk of the solution you put out there.

I find it helpful to think of this in both a **business** and **technical** context. I’m going to describe the high level approaches to managing both, and use a customer service help-desk use case to illustrate how we manage our risk in both cases.

### Business

For the business it can be hard to trust LLMs after the comparative certainties of rules-based or traditional machine learning systems, or indeed humans! A system where failures are open-ended and unpredictable is a difficult circle to square.

An approach I’ve seen be successful here was for a customer service use case - for this, we did the following:

First we identify the primary success and failure cases, and assign an estimated cost to them. This gives us a clear articulation of what the solution is likely to save or cost based on pilot performance.

*   For example, a case getting solved by an AI where it was previously solved by a human may save **$20**.
*   Someone getting escalated to a human when they shouldn’t might cost **$40**
*   In the worst case scenario, a customer gets so frustrated with the AI they churn, costing us **$1000**. We assume this happens in 5% of cases.

|Event|Value|Number of cases|Total value|
|---|---|---|---|
|AI success|+20|815|$16,300|
|AI failure (escalation)|-40|175.75|$7,030|
|AI failure (churn)|-1000|9.25|$9,250|
|Result|||+20|
|Break-even accuracy|||81.5%|

The other thing we did is to measure the empirical stats around the process which will help us measure the macro impact of the solution. Again using customer service, these could be:

*   The CSAT score for purely human interactions vs. AI ones
*   The decision accuracy for retrospectively reviewed cases for human vs. AI
*   The time to resolution for human vs. AI

In the customer service example, this helped us make two key decisions following a few pilots to get clear data:

1.  Even if our LLM solution escalated to humans more than we wanted, it still made an enormous operational cost saving over the existing solution. This meant that an accuracy of even 85% could be ok, if those 15% were primarily early escalations.
2.  Where the cost of failure was very high, such as a fraud case being incorrectly resolved, we decided the human would drive and the AI would function as an assistant. In this case, the decision accuracy stat helped us make the call that we weren’t comfortable with full autonomy.

### Technical

On the technical side it is more clear - now that the business is clear on the value they expect and the cost of what can go wrong, your role is to build a solution that handles failures gracefully in a way that doesn’t disrupt the user experience.

Let’s use the customer service example one more time to illustrate this, and we’ll assume we’ve got a model that is 85% accurate in determining intent. As a technical team, here are a few ways we can minimize the impact of the incorrect 15%:

*   We can prompt engineer the model to prompt the customer for more information if it isn’t confident, so our first-time accuracy may drop but we may be more accurate given 2 shots to determine intent.
*   We can give the second-line assistant the option to pass back to the intent determination stage, again giving the UX a way of self-healing at the cost of some additional user latency.
*   We can prompt engineer the model to hand off to a human if the intent is unclear, which costs us some operational savings in the short-term but may offset customer churn risk in the long term.

Those decisions then feed into our UX, which gets slower at the cost of higher accuracy, or more human interventions, which feed into the cost model covered in the business section above.

You now have an approach to breaking down the business and technical decisions involved in setting an accuracy target that is grounded in business reality.

Taking this forward
-------------------

This is a high level mental model for thinking about maximizing accuracy for LLMs, the tools you can use to achieve it, and the approach for deciding where enough is enough for production. You have the framework and tools you need to get to production consistently, and if you want to be inspired by what others have achieved with these methods then look no further than our customer stories, where use cases like [Morgan Stanley](https://openai.com/customer-stories/morgan-stanley) and [Klarna](https://openai.com/customer-stories/klarna) show what you can achieve by leveraging these techniques.

Best of luck, and we’re excited to see what you build with this!

Was this page useful?
Advanced usage
==============

Use advanced techniques for reproducibility and parameter tuning.

OpenAI's text generation models (often called generative pre-trained transformers or large language models) have been trained to understand natural language, code, and images. The models provide text outputs in response to their inputs. The text inputs to these models are also referred to as "prompts". Designing a prompt is essentially how you “program” a large language model model, usually by providing instructions or some examples of how to successfully complete a task.

Reproducible outputs
--------------------

Chat Completions are non-deterministic by default (which means model outputs may differ from request to request). That being said, we offer some control towards deterministic outputs by giving you access to the [seed](/docs/api-reference/chat/create#chat-create-seed) parameter and the [system\_fingerprint](/docs/api-reference/completions/object#completions/object-system_fingerprint) response field.

To receive (mostly) deterministic outputs across API calls, you can:

*   Set the [seed](/docs/api-reference/chat/create#chat-create-seed) parameter to any integer of your choice and use the same value across requests you'd like deterministic outputs for.
*   Ensure all other parameters (like `prompt` or `temperature`) are the exact same across requests.

Sometimes, determinism may be impacted due to necessary changes OpenAI makes to model configurations on our end. To help you keep track of these changes, we expose the [system\_fingerprint](/docs/api-reference/chat/object#chat/object-system_fingerprint) field. If this value is different, you may see different outputs due to changes we've made on our systems.

[

Deterministic outputs

Explore the new seed parameter in the OpenAI cookbook

](https://cookbook.openai.com/examples/reproducible_outputs_with_the_seed_parameter)

Managing tokens
---------------

Language models read and write text in chunks called tokens. In English, a token can be as short as one character or as long as one word (e.g., `a` or `apple`), and in some languages tokens can be even shorter than one character or even longer than one word.

As a rough rule of thumb, 1 token is approximately 4 characters or 0.75 words for English text.

Check out our [Tokenizer tool](https://platform.openai.com/tokenizer) to test specific strings and see how they are translated into tokens.

For example, the string `"ChatGPT is great!"` is encoded into six tokens: `["Chat", "G", "PT", " is", " great", "!"]`.

The total number of tokens in an API call affects:

*   How much your API call costs, as you pay per token
*   How long your API call takes, as writing more tokens takes more time
*   Whether your API call works at all, as total tokens must be below the model's maximum limit (4097 tokens for `gpt-3.5-turbo`)

Both input and output tokens count toward these quantities. For example, if your API call used 10 tokens in the message input and you received 20 tokens in the message output, you would be billed for 30 tokens. Note however that for some models the price per token is different for tokens in the input vs. the output (see the [pricing](https://openai.com/api/pricing) page for more information).

To see how many tokens are used by an API call, check the `usage` field in the API response (e.g., `response['usage']['total_tokens']`).

Chat models like `gpt-3.5-turbo` and `gpt-4-turbo-preview` use tokens in the same way as the models available in the completions API, but because of their message-based formatting, it's more difficult to count how many tokens will be used by a conversation.

Deep dive

Counting tokens for chat API calls

To see how many tokens are in a text string without making an API call, use OpenAI’s [tiktoken](https://github.com/openai/tiktoken) Python library. Example code can be found in the OpenAI Cookbook’s guide on [how to count tokens with tiktoken](https://cookbook.openai.com/examples/how_to_count_tokens_with_tiktoken).

Each message passed to the API consumes the number of tokens in the content, role, and other fields, plus a few extra for behind-the-scenes formatting. This may change slightly in the future.

If a conversation has too many tokens to fit within a model’s maximum limit (e.g., more than 4097 tokens for `gpt-3.5-turbo` or more than 128k tokens for `gpt-4o`), you will have to truncate, omit, or otherwise shrink your text until it fits. Beware that if a message is removed from the messages input, the model will lose all knowledge of it.

Note that very long conversations are more likely to receive incomplete replies. For example, a `gpt-3.5-turbo` conversation that is 4090 tokens long will have its reply cut off after just 6 tokens.

Parameter details
-----------------

### Frequency and presence penalties

The frequency and presence penalties found in the [Chat Completions API](/docs/api-reference/chat/create) and [Legacy Completions API](/docs/api-reference/completions) can be used to reduce the likelihood of sampling repetitive sequences of tokens.

Deep dive

Penalties behind the scenes

Reasonable values for the penalty coefficients are around 0.1 to 1 if the aim is to just reduce repetitive samples somewhat. If the aim is to strongly suppress repetition, then one can increase the coefficients up to 2, but this can noticeably degrade the quality of samples. Negative values can be used to increase the likelihood of repetition.

### Token log probabilities

The [logprobs](/docs/api-reference/chat/create#chat-create-logprobs) parameter found in the [Chat Completions API](/docs/api-reference/chat/create) and [Legacy Completions API](/docs/api-reference/completions), when requested, provides the log probabilities of each output token, and a limited number of the most likely tokens at each token position alongside their log probabilities. This can be useful in some cases to assess the confidence of the model in its output, or to examine alternative responses the model might have given.

### Other parameters

See the full [API reference documentation](https://platform.openai.com/docs/api-reference/chat) to learn more.

Was this page useful?
Responses vs. Chat Completions
==============================

Compare the Responses API and Chat Completions API.

The [Responses API](https://platform.openai.com/docs/api-reference/responses) and [Chat Completions API](https://platform.openai.com/docs/api-reference/chat) are two different ways to interact with OpenAI's models. This guide explains the key differences between the two APIs.

Why the Responses API?
----------------------

The Responses API is our newest core API and an agentic API primitive, combining the simplicity of Chat Completions with the ability to do more agentic tasks. As model capabilities evolve, the Responses API is a flexible foundation for building action-oriented applications, with built-in tools:

*   [Web search](/docs/guides/tools-web-search)
*   [File search](/docs/guides/tools-file-search)
*   [Computer use](/docs/guides/tools-computer-use)

If you're a new user, we recommend using the Responses API.

|Capabilities|Chat Completions API|Responses API|
|---|---|---|
|Text generation|||
|Audio||Coming soon|
|Vision|||
|Structured Outputs|||
|Function calling|||
|Web search|||
|File search|||
|Computer use|||
|Code interpreter||Coming soon|

### The Chat Completions API is not going away

The Chat Completions API is an industry standard for building AI applications, and we intend to continue supporting this API indefinitely. We're introducing the Responses API to simplify workflows involving tool use, code execution, and state management. We believe this new API primitive will allow us to more effectively enhance the OpenAI platform into the future.

### A stateful API and semantic events

Events are simpler with the Responses API. It has a predictable, event-driven architecture, whereas the Chat Completions API continuously appends to the content field as tokens are generated—requiring you to manually track differences between each state. Multi-step conversational logic and reasoning are easier to implement with the Responses API.

The Responses API clearly emits semantic events detailing precisely what changed (e.g., specific text additions), so you can write integrations targeted at specific emitted events (e.g., text changes), simplifying integration and improving type safety.

### Model availability in each API

Whenever possible, all new models will be added to both the Chat Completions API and Responses API. Some models may only be available through Responses API if they use built-in tools (e.g. our computer use models), or trigger multiple model generation turns behind the scenes (e.g. o1-pro) . The detail pages for each [model](/docs/models) will indicate if they support Chat Completions, Responses, or both.

Compare the code
----------------

The following examples show how to make a basic API call to the [Chat Completions API](https://platform.openai.com/docs/api-reference/chat) and the [Responses API](https://platform.openai.com/docs/api-reference/responses).

### Text generation example

Both APIs make it easy to generate output from our models. A completion requires a `messages` array, but a response requires an `input` (string or array, as shown below).

Chat Completions API

```python
from openai import OpenAI
client = OpenAI()

completion = client.chat.completions.create(
  model="gpt-4o",
  messages=[
      {
          "role": "user",
          "content": "Write a one-sentence bedtime story about a unicorn."
      }
  ]
)

print(completion.choices[0].message.content)
```

Responses API

```python
from openai import OpenAI
client = OpenAI()

response = client.responses.create(
  model="gpt-4o",
  input=[
      {
          "role": "user",
          "content": "Write a one-sentence bedtime story about a unicorn."
      }
  ]
)

print(response.output_text)
```

When you get a response back from the Responses API, the fields differ slightly. Instead of a `message`, you receive a typed `response` object with its own `id`. Responses are stored by default. Chat completions are stored by default for new accounts. To disable storage when using either API, set `store: false`.

Chat Completions API

```json
[
{
  "index": 0,
  "message": {
    "role": "assistant",
    "content": "Under the soft glow of the moon, Luna the unicorn danced through fields of twinkling stardust, leaving trails of dreams for every child asleep.",
    "refusal": null
  },
  "logprobs": null,
  "finish_reason": "stop"
}
]
```

Responses API

```json
[
{
  "id": "msg_67b73f697ba4819183a15cc17d011509",
  "type": "message",
  "role": "assistant",
  "content": [
    {
      "type": "output_text",
      "text": "Under the soft glow of the moon, Luna the unicorn danced through fields of twinkling stardust, leaving trails of dreams for every child asleep.",
      "annotations": []
    }
  ]
}
]
```

### Other noteworthy differences

*   The Responses API returns `output`, while the Chat Completions API returns a `choices` array.
*   Structured Outputs API shape is different. Instead of `response_format`, use `text.format` in Responses. Learn more in the [Structured Outputs](/docs/guides/structured-outputs) guide.
*   Function calling API shape is different—both for the function config on the request and function calls sent back in the response. See the full difference in the [function calling guide](/docs/guides/function-calling).
*   Reasoning is different. Instead of `reasoning_effort` in Chat Completions, use `reasoning.effort` with the Responses API. Read more details in the [reasoning](/docs/guides/reasoning) guide.
*   The Responses SDK has an `output_text` helper, which the Chat Completions SDK does not have.
*   Conversation state: You have to manage conversation state yourself in Chat Completions, while Responses has `previous_response_id` to help you with long-running conversations.
*   Responses are stored by default. Chat completions are stored by default for new accounts. To disable storage, set `store: false`.

What this means for existing APIs
---------------------------------

### Chat Completions

The Chat Completions API remains our most widely used API. We'll continue supporting it with new models and capabilities. If you don't need built-in tools for your application, you can confidently continue using Chat Completions.

We'll keep releasing new models to Chat Completions whenever their capabilities don't depend on built-in tools or multiple model calls. When you're ready for advanced capabilities designed specifically for agent workflows, we recommend the Responses API.

Assistants
----------

Based on developer feedback from the [Assistants API](/docs/api-reference/assistants) beta, we've incorporated key improvements into the Responses API to make it more flexible, faster, and easier to use. The Responses API represents the future direction for building agents on OpenAI.

We're working to achieve full feature parity between the Assistants and the Responses API, including support for Assistant-like and Thread-like objects and the Code Interpreter tool. When complete, we plan to formally announce the deprecation of the Assistants API with a target sunset date in the first half of 2026.

Upon deprecation, we will provide a clear migration guide from the Assistants API to the Responses API that allows developers to preserve all their data and migrate their applications. Until we formally announce the deprecation, we'll continue delivering new models to the Assistants API.

Was this page useful?

