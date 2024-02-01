# Solution
First off we can try a simple standard payload of `<script>alert('xss')</script>.`
We can then open the inspect element and look and see that it stores the input as code and not text like it should.
![image](https://github.com/rpulber/Web-Security-Playground/assets/95892479/4722793c-f753-4f6c-a9d5-15fe0b67ac18)

However, we don't see the alert actually pop up when we press the button. This is because we are still 
