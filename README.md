---
title: ChatGPT endpoint
keywords: 
last_updated: May 18, 2023
tags: []
summary: "Detailed description of the API of the ChatGPT endpoint."
---

## Overview

The ChatGPT endpoint has the following features:
 
- Authorization with API Token

Please make sure you take a look at the documentation from ChatGPT as features are based on its API:

- [API Reference](https://platform.openai.com/docs/introduction)

## Quick start

Once you configured the endpoint, you can list current models with this call:

```js
for(var model of app.endpoints.chatgpt.models.get().data)
{ 
    log(JSON.stringify(model))
}
```

Or you can generate a completion with this call:

```js
var res = app.endpoitns.chatgpt.completions.post({
    prompt: "Once upon a time",
    model: "text-davinci-003",
    max_tokens: 5
})
```

## Configuration

Before configuring the endpoint you will need to create an account in OpenAI:
[OpenAI login](https://platform.openai.com/signup?launch)

Once you have your account you will be able to configure the endpoint.

### API Token

The API token of the account. This field is required. [API Token list](https://platform.openai.com/account/api-keys)

### Organization ID

The organization ID of the account. This field is optional. [Organization ID](https://platform.openai.com/account/org-settings)

# Javascript API

The Javascript API of the chatgpt endpoint has three pieces:

- **HTTP requests**: These allow to make regular HTTP requests.
- **Shortcuts**: These are helpers to make HTTP request to the API in a more convenient way.
- **Additional Helpers**: These helpers provide additional features that facilitate or improves the endpoint usage in SLINGR.

## HTTP requests
You can make `GET`,`POST` requests to the [chatgpt API](API_URL_HERE) like this:
```javascript
var response = app.endpoints.chatgpt.get('/v1/models')
var response = app.endpoints.chatgpt.post('/v1/edits', body)
var response = app.endpoints.chatgpt.post('/v1/edits')
```

Please take a look at the documentation of the [HTTP endpoint](https://github.com/slingr-stack/http-endpoint#javascript-api)
for more information about generic requests.

## Shortcuts

Instead of having to use the generic HTTP methods, you can (and should) make use of the helpers provided in the endpoint:
<details>
    <summary>Click here to see all the helpers</summary>

<br>

* API URL: '/v1/models'
* HTTP Method: 'GET'
* More info: https://platform.openai.com/docs/api-reference
```javascript
app.endpoints.chatgpt.models.get()
```
---
* API URL: '/v1/models/:model'
* HTTP Method: 'GET'
* More info: https://platform.openai.com/docs/api-reference
```javascript
app.endpoints.chatgpt.models.get()
```
---
* API URL: '/v1/completions'
* HTTP Method: 'POST'
* More info: https://platform.openai.com/docs/api-reference
```javascript
app.endpoints.chatgpt.completions.post(body)
```
---
* API URL: '/v1/chat/completions'
* HTTP Method: 'POST'
* More info: https://platform.openai.com/docs/api-reference
```javascript
app.endpoints.chatgpt.chat.completions.post(body)
```
---
* API URL: '/v1/edits'
* HTTP Method: 'POST'
* More info: https://platform.openai.com/docs/api-reference
```javascript
app.endpoints.chatgpt.edits.post(body)
```
---
* API URL: '/v1/moderations'
* HTTP Method: 'POST'
* More info: https://platform.openai.com/docs/api-reference
```javascript
app.endpoints.chatgpt.moderations.post(body)
```
---

</details>

## Flow Step

As an alternative option to using scripts, you can make use of Flows and Flow Steps specifically created for the endpoint:
<details>
    <summary>Click here to see the Flow Steps</summary>

<br>



### Generic Flow Step

Generic flow step for full use of the entire endpoint and its services.

<h3>Inputs</h3>

<table>
    <thead>
    <tr>
        <th>Label</th>
        <th>Type</th>
        <th>Required</th>
        <th>Default</th>
        <th>Visibility</th>
        <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>URL (Method)</td>
        <td>choice</td>
        <td>yes</td>
        <td> - </td>
        <td>Always</td>
        <td>
            This is the http method to be used against the endpoint. <br>
            Possible values are: <br>
            <i><strong>GET,POST</strong></i>
        </td>
    </tr>
    <tr>
        <td>URL (Path)</td>
        <td>choice</td>
        <td>yes</td>
        <td> - </td>
        <td>Always</td>
        <td>
            The url to which this endpoint will send the request. This is the exact service to which the http request will be made. <br>
            Possible values are: <br>
            <i><strong>/v1/models<br>/v1/models/{model}<br>/v1/completions<br>/v1/chat/completions<br>/v1/edits<br>/v1/moderations<br></strong></i>
        </td>
    </tr>
    <tr>
        <td>Headers</td>
        <td>keyValue</td>
        <td>no</td>
        <td> - </td>
        <td>Always</td>
        <td>
            Used when you want to have a custom http header for the request.
        </td>
    </tr>
    <tr>
        <td>Query Params</td>
        <td>keyValue</td>
        <td>no</td>
        <td> - </td>
        <td>Always</td>
        <td>
            Used when you want to have a custom query params for the http call.
        </td>
    </tr>
    <tr>
        <td>Body</td>
        <td>json</td>
        <td>no</td>
        <td> - </td>
        <td>Always</td>
        <td>
            A payload of data can be sent to the server in the body of the request.
        </td>
    </tr>
    <tr>
        <td>Override Settings</td>
        <td>boolean</td>
        <td>no</td>
        <td> false </td>
        <td>Always</td>
        <td></td>
    </tr>
    <tr>
        <td>Follow Redirect</td>
        <td>boolean</td>
        <td>no</td>
        <td> false </td>
        <td> overrideSettings </td>
        <td>Indicates that the resource has to be downloaded into a file instead of returning it in the response.</td>
    </tr>
    <tr>
        <td>Download</td>
        <td>boolean</td>
        <td>no</td>
        <td> false </td>
        <td> overrideSettings </td>
        <td>If true the method won't return until the file has been downloaded, and it will return all the information of the file.</td>
    </tr>
    <tr>
        <td>File name</td>
        <td>text</td>
        <td>no</td>
        <td></td>
        <td> overrideSettings </td>
        <td>If provided, the file will be stored with this name. If empty the file name will be calculated from the URL.</td>
    </tr>
    <tr>
        <td>Full response</td>
        <td> boolean </td>
        <td>no</td>
        <td> false </td>
        <td> overrideSettings </td>
        <td>Include extended information about response</td>
    </tr>
    <tr>
        <td>Connection Timeout</td>
        <td> number </td>
        <td>no</td>
        <td> 5000 </td>
        <td> overrideSettings </td>
        <td>Connect timeout interval, in milliseconds (0 = infinity).</td>
    </tr>
    <tr>
        <td>Read Timeout</td>
        <td> number </td>
        <td>no</td>
        <td> 60000 </td>
        <td> overrideSettings </td>
        <td>Read timeout interval, in milliseconds (0 = infinity).</td>
    </tr>
    </tbody>
</table>

<h3>Outputs</h3>

<table>
    <thead>
    <tr>
        <th>Name</th>
        <th>Type</th>
        <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>response</td>
        <td>object</td>
        <td>
            Object resulting from the response to the endpoint call.
        </td>
    </tr>
    </tbody>
</table>


</details>

For more information about how shortcuts or flow steps works, and how they are generated, take a look at the [slingr-helpgen tool](https://github.com/slingr-stack/slingr-helpgen).

## Additional Flow Step


<details>
    <summary>Click here to see the Customs Flow Steps</summary>

<br>



### Chat Completion

This flow step is used to get a chat completion for a prompt with messages.

<h3>Inputs</h3>

<table>
    <thead>
    <tr>
        <th>Label</th>
        <th>Type</th>
        <th>Required</th>
        <th>Default</th>
        <th>Visibility</th>
        <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>Model</td>
        <td>choice</td>
        <td>yes</td>
        <td> - </td>
        <td>Always</td>
        <td>
            This are the models currently available: <br>
            Possible values are: <br>
            <i><strong>gpt-4, gpt-4-0314, gpt-4-32k, gpt-4-32k-0314, gpt-3.5-turbo, gpt-3.5-turbo-0301</strong></i>
        </td>
    </tr>
    <tr>
        <td>Messages</td>
        <td>json</td>
        <td>yes</td>
        <td> - </td>
        <td>Always</td>
        <td>
            A list of messages describing the conversation so far.
            Must contain: <br>
                Role: The role of the author of this message. One of system, user, or assistant.
                Content: The contents of the message.
                I.E.: {"role": "user", "content": "Hi"}
        </td>
    </tr>
    <tr>
        <td>Max Tokens</td>
        <td> number </td>
        <td>no</td>
        <td> - </td>
        <td>Always</td>
        <td>
            The maximum number of tokens to generate in the chat completion. The total length of input tokens and generated tokens is limited by the model's context length.
        </td>
    </tr>
    <tr>
        <td>Temperature</td>
        <td> number </td>
        <td>no</td>
        <td> - </td>
        <td>Always</td>
        <td>
            What sampling temperature to use, between 0 and 2. Higher values like 0.8 will make the output more random, while lower values like 0.2 will make it more focused and deterministic. We generally recommend altering this or top_p but not both.
        </td>
    </tr>
    <tr>
        <td>Top P</td>
        <td> number </td>
        <td>no</td>
        <td> - </td>
        <td>Always</td>
        <td>
            An alternative to sampling with temperature, called nucleus sampling, where the model considers the results of the tokens with top_p probability mass. So 0.1 means only the tokens comprising the top 10% probability mass are considered. We generally recommend altering this or temperature but not both.
        </td>
    </tr>
    <tr>
        <td>N</td>
        <td> number </td>
        <td>no</td>
        <td> - </td>
        <td>Always</td>
        <td>How many chat completion choices to generate for each input message.</td>
    </tr>
    <tr>
        <td>User</td>
        <td>text</td>
        <td>no</td>
        <td> - </td>
        <td>Always</td>
        <td>A unique identifier representing your end-user, which can help OpenAI to monitor and detect abuse.</td>
    </tr>
    <tr>
        <td>Override Settings</td>
        <td>boolean</td>
        <td>no</td>
        <td> false </td>
        <td>Always</td>
        <td></td>
    </tr>
    <tr>
        <td>Full response</td>
        <td> boolean </td>
        <td>no</td>
        <td> false </td>
        <td> overrideSettings </td>
        <td>Include extended information about response</td>
    </tr>
    <tr>
        <td>Connection Timeout</td>
        <td> number </td>
        <td>no</td>
        <td> 5000 </td>
        <td> overrideSettings </td>
        <td>Connect timeout interval, in milliseconds (0 = infinity).</td>
    </tr>
    <tr>
        <td>Read Timeout</td>
        <td> number </td>
        <td>no</td>
        <td> 60000 </td>
        <td> overrideSettings </td>
        <td>Read timeout interval, in milliseconds (0 = infinity).</td>
    </tr>
    </tbody>
</table>

<h3>Outputs</h3>

<table>
    <thead>
    <tr>
        <th>Name</th>
        <th>Type</th>
        <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>response</td>
        <td>object</td>
        <td>
            Object resulting from the response to the endpoint call.
        </td>
    </tr>
    </tbody>
</table>


### Completions

This flow step is used to get a completion for a prompt.

<h3>Inputs</h3>

<table>
    <thead>
    <tr>
        <th>Label</th>
        <th>Type</th>
        <th>Required</th>
        <th>Default</th>
        <th>Visibility</th>
        <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>Model</td>
        <td>choice</td>
        <td>yes</td>
        <td> - </td>
        <td>Always</td>
        <td>
            This are the models currently available: <br>
            Possible values are: <br>
            <i><strong>text-davinci-003, text-davinci-002, text-curie-001, text-babbage-001, text-ada-001</strong></i>
        </td>
    </tr>
    <tr>
        <td>Prompt</td>
        <td>text</td>
        <td>no</td>
        <td> - </td>
        <td>Always</td>
        <td>
            The prompt(s) to generate completions for, encoded as a string, array of strings, array of tokens, or array of token arrays.
        </td>
    </tr>
    <tr>
        <td>Suffix</td>
        <td> number </td>
        <td>no</td>
        <td> - </td>
        <td>Always</td>
        <td>
            The suffix that comes after a completion of inserted text.
        </td>
    </tr>
    <tr>
        <td>Max Tokens</td>
        <td> number </td>
        <td>no</td>
        <td> - </td>
        <td>Always</td>
        <td>
            The maximum number of tokens to generate in the chat completion. The total length of input tokens and generated tokens is limited by the model's context length.
        </td>
    </tr>
    <tr>
        <td>Temperature</td>
        <td> number </td>
        <td>no</td>
        <td> - </td>
        <td>Always</td>
        <td>
            What sampling temperature to use, between 0 and 2. Higher values like 0.8 will make the output more random, while lower values like 0.2 will make it more focused and deterministic. We generally recommend altering this or top_p but not both.
        </td>
    </tr>
    <tr>
        <td>Top P</td>
        <td> number </td>
        <td>no</td>
        <td> - </td>
        <td>Always</td>
        <td>
            An alternative to sampling with temperature, called nucleus sampling, where the model considers the results of the tokens with top_p probability mass. So 0.1 means only the tokens comprising the top 10% probability mass are considered. We generally recommend altering this or temperature but not both.
        </td>
    </tr>
    <tr>
        <td>N</td>
        <td> number </td>
        <td>no</td>
        <td> - </td>
        <td>Always</td>
        <td>How many chat completion choices to generate for each input message.</td>
    </tr>
    <tr>
        <td>User</td>
        <td>text</td>
        <td>no</td>
        <td> - </td>
        <td>Always</td>
        <td>A unique identifier representing your end-user, which can help OpenAI to monitor and detect abuse.</td>
    </tr>
    <tr>
        <td>Override Settings</td>
        <td>boolean</td>
        <td>no</td>
        <td> false </td>
        <td>Always</td>
        <td></td>
    </tr>
    <tr>
        <td>Full response</td>
        <td> boolean </td>
        <td>no</td>
        <td> false </td>
        <td> overrideSettings </td>
        <td>Include extended information about response</td>
    </tr>
    <tr>
        <td>Connection Timeout</td>
        <td> number </td>
        <td>no</td>
        <td> 5000 </td>
        <td> overrideSettings </td>
        <td>Connect timeout interval, in milliseconds (0 = infinity).</td>
    </tr>
    <tr>
        <td>Read Timeout</td>
        <td> number </td>
        <td>no</td>
        <td> 60000 </td>
        <td> overrideSettings </td>
        <td>Read timeout interval, in milliseconds (0 = infinity).</td>
    </tr>
    </tbody>
</table>

<h3>Outputs</h3>

<table>
    <thead>
    <tr>
        <th>Name</th>
        <th>Type</th>
        <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>response</td>
        <td>object</td>
        <td>
            Object resulting from the response to the endpoint call.
        </td>
    </tr>
    </tbody>
</table>


### Edits

This flow step is used to get an edit for a prompt and an instruction.

<h3>Inputs</h3>

<table>
    <thead>
    <tr>
        <th>Label</th>
        <th>Type</th>
        <th>Required</th>
        <th>Default</th>
        <th>Visibility</th>
        <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>Model</td>
        <td>choice</td>
        <td>yes</td>
        <td> - </td>
        <td>Always</td>
        <td>
            This are the models currently available: <br>
            Possible values are: <br>
            <i><strong>text-davinci-edit-001, code-davinci-edit-001</strong></i>
        </td>
    </tr>
    <tr>
        <td>Input</td>
        <td>text</td>
        <td>no</td>
        <td> - </td>
        <td>Always</td>
        <td>
            The input text to use as a starting point for the edit.
        </td>
    </tr>
    <tr>
        <td>Instruction</td>
        <td>text</td>
        <td>no</td>
        <td> - </td>
        <td>Always</td>
        <td>
            The instruction that tells the model how to edit the prompt.
        </td>
    </tr>
    <tr>
        <td>Max Tokens</td>
        <td> number </td>
        <td>no</td>
        <td> - </td>
        <td>Always</td>
        <td>
            The maximum number of tokens to generate in the chat completion. The total length of input tokens and generated tokens is limited by the model's context length.
        </td>
    </tr>
    <tr>
        <td>Temperature</td>
        <td> number </td>
        <td>no</td>
        <td> - </td>
        <td>Always</td>
        <td>
            What sampling temperature to use, between 0 and 2. Higher values like 0.8 will make the output more random, while lower values like 0.2 will make it more focused and deterministic. We generally recommend altering this or top_p but not both.
        </td>
    </tr>
    <tr>
        <td>Top P</td>
        <td> number </td>
        <td>no</td>
        <td> - </td>
        <td>Always</td>
        <td>
            An alternative to sampling with temperature, called nucleus sampling, where the model considers the results of the tokens with top_p probability mass. So 0.1 means only the tokens comprising the top 10% probability mass are considered. We generally recommend altering this or temperature but not both.
        </td>
    </tr>
    <tr>
        <td>N</td>
        <td> number </td>
        <td>no</td>
        <td> - </td>
        <td>Always</td>
        <td>How many chat completion choices to generate for each input message.</td>
    </tr>
    <tr>
        <td>User</td>
        <td>text</td>
        <td>no</td>
        <td> - </td>
        <td>Always</td>
        <td>A unique identifier representing your end-user, which can help OpenAI to monitor and detect abuse.</td>
    </tr>
    <tr>
        <td>Override Settings</td>
        <td>boolean</td>
        <td>no</td>
        <td> false </td>
        <td>Always</td>
        <td></td>
    </tr>
    <tr>
        <td>Full response</td>
        <td> boolean </td>
        <td>no</td>
        <td> false </td>
        <td> overrideSettings </td>
        <td>Include extended information about response</td>
    </tr>
    <tr>
        <td>Connection Timeout</td>
        <td> number </td>
        <td>no</td>
        <td> 5000 </td>
        <td> overrideSettings </td>
        <td>Connect timeout interval, in milliseconds (0 = infinity).</td>
    </tr>
    <tr>
        <td>Read Timeout</td>
        <td> number </td>
        <td>no</td>
        <td> 60000 </td>
        <td> overrideSettings </td>
        <td>Read timeout interval, in milliseconds (0 = infinity).</td>
    </tr>
    </tbody>
</table>

<h3>Outputs</h3>

<table>
    <thead>
    <tr>
        <th>Name</th>
        <th>Type</th>
        <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>response</td>
        <td>object</td>
        <td>
            Object resulting from the response to the endpoint call.
        </td>
    </tr>
    </tbody>
</table>



</details>

## Additional Helpers
*MANUALLY ADD THE DOCUMENTATION OF THESE HELPERS HERE...*


## About SLINGR

SLINGR is a low-code rapid application development platform that accelerates development, with robust architecture for integrations and executing custom workflows and automation.

[More info about SLINGR](https://slingr.io)

## License

This endpoint is licensed under the Apache License 2.0. See the `LICENSE` file for more details.
