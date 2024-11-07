+++
title = "Intro to Langchain.rb"
+++

For the past few months, I have been working with an AI travel startup where we use LLM API calls to power parts of our application. It's been a lot of fun to build AI-powered applications, and it's exciting to see how fast this space is changing. While the app I am working on doesn’t use this gem, Langchain.rb provides many great tools that are worth checking out if you want to build with AI in your Ruby applications. I would definitely consider using it in the future for several reasons.

1. Encourages experimentation
2. Assistants and tools
3. RAG, vectorized databases, and more

### Encourages Experimentation

The first reason is that it makes experimentation and development much easier and faster than if you were making calls directly to an LLM provider such as OpenAI, Anthropic, or Google. At its most basic level, Langchain.rb is a layer on top of these LLMs that allows us to interact with them from one interface. This means we can easily swap out LLMs by changing just a couple of lines of code.

```rb
openai = Langchain::LLM::OpenAI.new(api_key: ENV["OPENAI_API_KEY"])
```

Instantiating an LLM is as simple as the code above, and swapping it out for a different one is just as easy:

```rb
anthropic = Langchain::LLM::Anthropic.new(api_key: ENV["Anthropic_API_KEY"])
```

This way, you can explore how different LLMs perform in your application. With the landscape changing as rapidly as it is, where one model may outperform another on a month-by-month basis, it's nice to be able to try all available options.

### Assistants & Tools

Assistants and tools are another exciting aspect of Langchain.rb. Assistants allow you to create an instance of your LLM interface with instructions and access to various tools. There are built-in tools such as a calculator, weather, Google search, and more. When you create an assistant, you can simply specify the tools that you want it to have access to.

```rb
assistant = Langchain::Assistant.new(
  llm: openai,
  instructions: "You are a travel Assistant that is able to give directions and weather for given locations",
  tools: [
    Langchain::Tool::DirectionsGateway.new,
    Langchain::Tool::WeatherGateway.new
  ]
)
```

Here, I gave my assistant access to a weather tool and a directions tool. These tools make API calls to fetch relevant information. Back at Turing, I worked on a project called "Sweater Weather" where we used similar APIs to get weather and directions data, providing directions from point A to B and forecasting weather upon arrival. The app could then let you know if it was sweater weather or not. I wanted to see if I could give an assistant access to these APIs to achieve a similar function—and it turns out, it works. When asked for directions, the assistant makes the appropriate calls, retrieves the directions, calculates the time of arrival, and provides the corresponding weather!

```rb
assistant.add_message_and_run content: user_message, auto_tool_execution: true
```
This line runs the user’s message in the Langchain.rb playground, allowing the assistant to automatically execute tools as needed.

### RAG, Vectorized Databases, and more

Langchain.rb offers much more, and I’m excited about the possibilities of using Retrieval-Augmented Generation (RAG) and vectorized data storage. If you’d like to learn more, I encourage you to check out the project on GitHub, where you’ll find a folder of examples. You can also check out my repo for this small exploration.
