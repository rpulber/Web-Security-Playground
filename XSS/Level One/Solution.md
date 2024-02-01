# Solution
First off we can try a simple standard payload of `<script>alert('xss')</script>.`
We can then open the inspect element and look and see that it stores the input as code and not text like it should:


![image](https://github.com/rpulber/Web-Security-Playground/assets/95892479/4722793c-f753-4f6c-a9d5-15fe0b67ac18)

The issue really is in the built-in functionality of the website. If we look at the code on line 25 we see:
```
message.innerHTML = `Your name is ${userInput}`
```
Here, the message variable crafts the message displayed on the screen after hitting the button. The usage of innerHTML implies that the content undergoes parsing and interpretation as HTML. To execute JavaScript code, we must navigate the challenge of either escaping the HTML or utilizing an HTML tag to facilitate code execution. Attempts to escape HTML by closing the `<h1>` tag are futile as the system automatically removes the closing tag.

However, we find a clever workaround by harnessing the `<img>` HTML tag, known for enabling JavaScript code execution. The <img> tag boasts an onerror function, triggering JavaScript code if it can't locate the specified image. By providing a nonexistent image source, we ingeniously prompt our desired code execution:
`<img src=non_existant_image onerror=alert('xss')>`


# Remediation
The primary concern with the existing code lies in its use of .innerHTML, a known risky coding practice susceptible to both HTML injection and DOM-based Cross-Site Scripting (DOM XSS) vulnerabilities. To address this issue, a more secure alternative is recommended, such as using either .textContent or innerText. By adopting these alternatives, the input is treated strictly as text without any interpretation as HTML, eliminating the risks associated with potential code injection and ensuring a safer interaction with the Document Object Model (DOM). This mitigates the likelihood of security vulnerabilities stemming from user input manipulation and strengthens the overall robustness of the code.
Code:
```
message.textContent = `Your name is ${userInput}`
```
```
message.innertext = `Your name is ${userInput}`
```
