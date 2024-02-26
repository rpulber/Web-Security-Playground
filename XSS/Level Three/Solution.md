This website was created to simulate a reddirect website which uses a parameter which would tell the website what subdomain to target.

# Solution
With the above in mind our first step would be to try and find this parameter so that we could try and inject payloads into it. Now when we look through the code we see on line 27 a function called parameterLink(). When investigating this function we can tell what it really is doing. on line 28-29 it creates the parameter that we are going to exploit. It creates the parameter using the `new URLSearchPrams` function and then its function also passes into the variable which is urlParams which we can then call using `.get()` which now creates the parameter `link`. 

Now that we know what the parameter is, we can also see that in line 31 it appends whatever is in the parameter to the a tag and more specifically its href attribute. This means we have dirrect access to change the href attribute in line 12. So now we can try to escape the href tag by injecting code into the parameter. 
