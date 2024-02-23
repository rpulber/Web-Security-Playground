# Solution
In Level One, we were able to use a payload containing the <img> tag. While the recommended fix was to change innerHtml to innerText, the developers decided to take the route of blacklisting certain characters to ensure that the payload would not work. Using the .replace() function they replaced every "<", ">", and "img" to a blank space removing it from the user input. This can be seen on line 24:
![image](https://github.com/rpulber/Web-Security-Playground/assets/95892479/fd03fe94-151e-419e-8883-b7de7a3abb7d)

This meant that if we tried to do our previous payload of:
```<img src=non_existant_image onerror=alert('xss')>```
it would not work but instead would show us:
![image](https://github.com/rpulber/Web-Security-Playground/assets/95892479/eaec948d-e1f8-4ea0-92fb-29597c60bb9c)

From this, we can see that it just completely filtered out the <img> tag making it no longer code but just regular text. Now to get around this we have to understand how the replace function works. When you use the replace function such as `.replace(/img/,"")` it  will only replace the first instance of 'img' text that it sees.  Consequently, if two 'img' instances are present in our input text, only the first one will be filtered. So if we do the payload: <img src=non_existant_image onerror=alert('xss')> but instead add '<img>' at the start of it we would get XSS because it would only get rid of the first '<img>' evading the filter. So our final payload would look like this: 
```<img><img src=non_existant_image onerror=alert('xss')>```

# Remediation 
The problem with the replace function is that by default it only replaces the first instance of whatever it's filtering. There is a simple code adjustment that would change this so that it would filter every single instance of the character. This would be using the g capability and putting it into the function. So if you instead change the code of line 24 to:
![image](https://github.com/rpulber/Web-Security-Playground/assets/95892479/87f5cf43-baa9-4048-b737-03f2c9bb0005)
Now if you can tell we added a g to every function and it will now filter every instance of whatever it is called to replace. Now this does not completely patch all issues as we will see in future levels!
