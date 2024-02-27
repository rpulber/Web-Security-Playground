This website was created to simulate a redirect website which uses a parameter which would tell the website what subdomain to target.

# Solution
With the above in mind, our first step would be to try and find this parameter so that we could try and inject payloads into it. Now when we look through the code we see on line 27 a function called parameterLink(). When investigating this function we can tell what it is doing. On lines 28-29, it creates the parameter that we are going to exploit. It creates the parameter using the `new URLSearchPrams` function and then its function also passes into the variable which is urlParams which we can then call using `.get()` which now creates the parameter `link`. 

Now that we know what the parameter is, we can also see that in line 31 it appends whatever is in the parameter to the <a> tag and more specifically its href attribute. This means we have direct access to change the href attribute in line 12. So now we can try to escape the href tag by injecting code into the parameter. We can inject code into the parameter like so:`https://www.page_source.html/?link=<code we want to inject>`. Your actual URL will be different but it's going to be the exact one that is in your browser so after it you will add `/?link=` to start testing the parameter like so:

![image](https://github.com/rpulber/Web-Security-Playground/assets/95892479/dbb014c3-a920-402c-b9c3-e7c56f3bf33d)

At first, we want to see where our input is reflected in the code so we try `INJECTED_CODE`. We see this input INJECTED_CODE into our href tag on line 12. Now that we see where it's reflected we can attempt to escape the href and <a> tag to inject code. However when we try to escape the href by doing something like `">` we see that it is added to the href tag purely as text:

![image](https://github.com/rpulber/Web-Security-Playground/assets/95892479/ca65b254-b9e7-42e1-b560-c70f5c4a2aa8)

This presents us with an issue, since our input is purely seen as text we can't escape the href tag and inject code. One way we can get the browser to see our input as code is by using the `javascript:` function. Anytime the browser sees this input it knows that it is code and will execute whatever follows. So if we do `javascript:alert('xss')` this would lead the browser to see the input as code and inject the payload into the href but since it automatically clicks on the href it would automatically execute our code giving us XSS!
