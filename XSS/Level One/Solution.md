# Solution
First off we can try a simple standard payload of `<script>alert('xss')</script>.`
We can then open the inspect element and look and see that it stores the input as code and not text like it should:


![image](https://github.com/rpulber/Web-Security-Playground/assets/95892479/4722793c-f753-4f6c-a9d5-15fe0b67ac18)

The issue really is in the built-in functionality of the website. If we look at the code on line 25 we see:
```
message.innerHTML = `Your name is ${userInput}`
```
The message variable is responsible for the message we see popping on the screen when we press the button which means thats what we're injecting into. As we can see it is followed by a innerHTML property which means it is parsing and interpreting the HTML. This means that in order for us to get any javascript code execution we would either have to escape the HTML or use a HTML tag to get javascript code execution.
Now we can't escape the HTML because every time we try to end the `<h1>` it just gets rid of it. 

We can however use the `<img>` HTML tag which could allow us to run javascript. The img tag has a onerror function in which it will run javascript if it can't find the img its looking for. So we are going to give it a nonexistent image which when it won't be able to find it will run our code.
`<img src=non_existant_image onerror=alert('xss')>`



