In Level One, we were able to use a payload containing the <img> tag. While the recommended fix was to change innerHtml to innerText, the developers decided to take the route of blacklisting certain characters to ensure that the payload would not work. Using the .replace() function they replaced every "<", ">", and "img" to a blank space removing it from the user input. This can be seen on line 24:
![image](https://github.com/rpulber/Web-Security-Playground/assets/95892479/7cb5b5c5-48d4-4a66-b289-11a8abd7f471)


