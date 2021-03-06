---
title: "Swagger UI tutorial"
permalink: /pubapis_swagger.html
course: "Documenting REST APIs"
sidebar: docapis
weight: 4.5
section: restapispecifications
path1: /restapispecifications.html
redirect_from:
- https://idratherbewriting.com/pubapis_swagger/
glossary_keys:
- swagger
- openapi
- swagger_editor
- swagger_ui
- swagger_codegen
---

[Swagger UI](https://github.com/swagger-api/swagger-ui) provides a display framework that reads an [OpenAPI specification document](https://github.com/OAI/OpenAPI-Specification) and generates an interactive documentation website. This tutorial shows you how to use the Swagger UI interface and how to integrate an OpenAPI specification document into the standalone distribution of Swagger UI.

For a more detailed conceptual overview of OpenAPI and Swagger, see [Introduction to the OpenAPI specification and Swagger](pubapis_swagger_intro.html).

{: .tip}
For a step-by-step tutorial on creating an OpenAPI specification document, see the [OpenAPI tutorial](pubapis_openapi_tutorial_overview.html). In the tutorial, I showed how the OpenAPI specification gets rendered by the Swagger UI display that is built into the [Swagger Editor](https://editor.swagger.io/). Here I explain how to use Swagger UI as a standalone output.  

{% if site.format == "web" %}
* TOC
{:toc}
{% endif %}

## Swagger UI overview

Swagger UI is one of the most popular tools for generating interactive documentation from your OpenAPI document. Swagger UI generates an interactive API console for users to quickly learn about and try the API. Additionally, Swagger UI is an [actively managed project](https://github.com/swagger-api/swagger-ui) (with an Apache 2.0 license) that supports the latest version of the OpenAPI spec (3.x) and integrates with other Swagger tools.

In the following tutorial, I'll show you how to Swagger UI works and how to integrate an OpenAPI specification document into it.

{% include random_ad2.html %}

Before we dive into Swagger, it might help to clarify some key terms.

{% if site.format == "web" %}

{% include glossary_limited.html file="glossary" %}

{% elsif site.format == "pdf" or site.format == "kindle" %}


{% endif %}

## The Swagger UI Petstore example

To get a better understanding of Swagger UI, let's explore the <a href="http://petstore.swagger.io/">Swagger Petstore example</a>. In the Petstore example, the site is generated using [Swagger UI](https://github.com/swagger-api/swagger-ui).

<a href="http://petstore.swagger.io/" class="noExtIcon"><img src="images/swaggerpetstoreui.png" alt="Petstore UI" /></a>

The endpoints are grouped as follows:

* [pet](http://petstore.swagger.io/#/pet)
* [store](http://petstore.swagger.io/#/store)
* [user](http://petstore.swagger.io/#/user).

### Authorize your requests

Before making any requests, you would normally authorize your session by clicking the **Authorize** button and completing the information required in the Authorization modal pictured below:

<a href="http://petstore.swagger.io/" class="noExtIcon"><img class="medium" src="images/swaggerui_authorize.png" alt="Authorization modal in Swagger UI" /></a>

The Petstore example has an OAuth 2.0 security model. However, the authorization code is just for demonstration purposes. There isn't any real logic authorizing those requests, so you can simply close the Authorization modal.

### Make a request

Now let's make a request:

1.  Expand the [**POST Pet** endpoint](http://petstore.swagger.io/#/pet/addPet).
2.  Click **Try it out**.

    <a href="http://petstore.swagger.io/" class="noExtIcon"><img src="images/swaggerui_petendpoint.png" alt="Try it out button in Swagger UI" /></a>

    After you click Try it out, the example value in the Request Body field becomes editable.

3.  In the Example Value field, change the first `id` value to a random integer, such as `193844`. Change the second `name` value to something you'd recognize (your pet's name).
4.  Click **Execute**.

    {% include course_image.html url="http://petstore.swagger.io/" size="large" filename="swaggerui_execute" ext_print="png" ext_web="png" alt="Executing a sample Petstore request" caption="Executing a sample Petstore request" %}

    Swagger UI submits the request and shows the [curl that was submitted](docapis_make_curl_call.html). The Responses section shows the [response](docapis_doc_sample_responses_and_schema.html). (If you select JSON rather than XML in the "Response content type" drop-down box, the response's format will be JSON.)

    <a href="http://petstore.swagger.io/" class="noExtIcon"><img src="images/swaggerui_response.png" alt="Response from Swagger Petstore get pet request" /></a>

    {% include important.html content="The Petstore is a functioning API, and you have actually created a pet. You now need to take responsibility for your pet and begin feeding and caring for it! All joking aside, most users don't realize they're playing with real data when they execute responses in an API (especially when using their own API key). This test data may be something you have to wipe clean when you transition from exploring and learning about the API to eventually using the API for production use." %}

### Verify that your pet was created

1.  Expand the [**GET /pet/{petId}** endpoint](http://petstore.swagger.io/#/pet/getPetById).
2.  Click **Try it out**.
3.  Enter the pet ID you used in the previous operation. (If you forgot it, look back in the **POST Pet** endpoint to check the value.)
4.  Click **Execute**. You should see your pet's name returned in the Response section.

{% include random_ad.html %}

## Some sample Swagger UI doc sites

Before we get into this Swagger tutorial with another API (other than Petstore), check out a few Swagger implementations:

* [Reverb](https://reverb.com/swagger#/articles)
* [VocaDB](http://vocadb.net/swagger/ui/index)
* [Watson Developer Cloud](https://watson-api-explorer.mybluemix.net/)
* [The Movie Database API](https://developers.themoviedb.org/3/account)
* [Zomato API](https://developers.zomato.com/documentation)

Some of these sites look the same, but others, such as The Movie Database API and Zomato, have been integrated seamlessly into the rest of their documentation website.

Looking at the examples, you'll notice the documentation is short and sweet in a Swagger implementation. This brevity is because the Swagger display is meant to be an interactive experience where you can try out calls and see responses &mdash; using your own API key to see your own data. It's the learn-by-doing-and-seeing-it approach. Also, Swagger UI only covers the [reference topics](docendpoints.html) of your documentation. The [non-reference topics](docnonref.html) are usually covered in a separate guide.

{% include content/activities/create_swaggerui_display.md %}

## Configuring Swagger UI parameters

Swagger UI provides various [configuration parameters](https://github.com/swagger-api/swagger-ui/blob/master/docs/usage/configuration.md) (unrelated to your [OpenAPI parameters](pubapis_openapi_step4_paths_object.html#parameters)) you can use to customize the interactive display. For example, you can set whether each endpoint is expanded or collapsed, how tags and operations are sorted, whether to show request headers in the response, whether to include the Model section, and more.

We won't get too much into the details of these configuration parameters in the tutorial. I just want to call attention to these parameters here for awareness.

If you look at the [source of the Swagger UI demo](https://idratherbewriting.com/learnapidoc/assets/files/swagger/) (go to View > Source), you'll see the parameters listed in the `// Build a system` section:

```js
  // Build a system
const ui = SwaggerUIBundle({
  url: "openapi_openweathermap.yml",
  dom_id: '#swagger-ui',
  defaultModelsExpandDepth: -1,
  deepLinking: true,
  presets: [
    SwaggerUIBundle.presets.apis,
    SwaggerUIStandalonePreset
  ],
  plugins: [
    SwaggerUIBundle.plugins.DownloadUrl
  ],
  layout: "StandaloneLayout"
})
```

The parameters there (e.g., `deepLinking`, `dom_id`, etc.) are defaults. However, I've added `defaultModelsExpandDepth: -1` to hide the "Models" section at the bottom of the Swagger UI display (since I think that section is unnecessary).

You can also learn about the Swagger UI configuration parameters in the [Swagger documentation](https://swagger.io/docs/open-source-tools/swagger-ui/usage/configuration/).

## Challenges with Swagger UI

As you explore Swagger UI, you may notice a few limitations:

* There's not much room to describe in detail the workings of the endpoints in Swagger. If you have several paragraphs of details and gotchas about a parameter, it's best to link out from the description to another page in your docs. The OpenAPI spec provides a way to link to external documentation in both the [paths object](pubapis_openapi_step4_paths_object.html), the [info object](pubapis_openapi_step2_info_object.html), and the [externalDocs object](pubapis_openapi_step8_externaldocs_object.html)
* The Swagger UI looks mostly the same for each output. You can [customize Swagger UI](https://swagger.io/docs/swagger-tools/#customization-36) with your own branding, but it will some more in-depth UX skills. It is, however, relatively easy to change the color and image in the top navigation bar.
* The Swagger UI might be a separate site from your other documentation. This separate output means that in your regular docs, you'll probably need to link to Swagger as the reference for your endpoints. You don't want to duplicate your parameter descriptions and other details in two different sites. See [Integrating Swagger UI with the rest of your docs](pubapis_combine_swagger_and_guide.html) for strategies to unify your two sites (reference docs and user guide).

## Troubleshooting issues with Swagger UI {#troubleshooting_swagger}

When you're setting up Swagger UI, you might run into some issues. The following are the most common:

**CORS issues:**

If you have security correctly configured, but the requests are rejected, it could be due to a CORS (cross-origin resource sharing) issue. CORS is a security measure that websites implement to make sure other scripts and processes cannot take their content through requests from remote servers. See [CORS Support](https://github.com/swagger-api/swagger-ui#cors-support) in Swagger UI's documentation for details.

If the requests aren't working, open your browser's JavaScript console (in Chrome, View > Developer > Javascript Console) when you make the request and see if the error relates to cross-origin requests. If so, ask your developers to enable CORS on the endpoints.

**Host URL issues:**

The host for your test server might be another reason that requests are rejected. Some APIs (like Aeris Weather) require you to create an App ID that is based on the host URL where you'll be executing requests. If the host URL you registered is `http://mysite.com`, but you're submitting the test from `https://editor.swagger.io/`, the API server will reject the requests.

## Embedding Swagger UI within an existing site

In addition to publishing your Swagger UI output as a [standalone site](https://idratherbewriting.com/learnapidoc/assets/files/swagger/), you can also [embed the Swagger file within an existing site](pubapis_swagger_demo.html). Since the Swagger UI site is responsive, it resizes well to fit into most any space.
