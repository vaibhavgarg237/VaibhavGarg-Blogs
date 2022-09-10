## Why I'm in love with Tailwind-CSS!!!


![vaibhavtailwindcss.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1662809981477/5yRCqkCcN.gif align="center")
*Have a little appreciation of memes? Scroll Down!😁😂*

There was a time when I didn't like writing CSS because of so many properties &  navigation between various files causing lots of friction and a bad development experience. Then I came across [Tailwind CSS](https://tailwindcss.com/) which made the development experience so easy and convenient because now we don't need to navigate between CSS and other files. I usually forgot those classes which I declared in JSX/HTML which lead to constantly navigating back to those files and then writing CSS. 

Tailwind CSS is a utility-first CSS framework packed with various classes that can be used to write any design directly in the markup. 
- Complete control of unopinionated styling 
- Highly customizable
- CSS is independent of each other
- No risk of breaking existing templates
- Only those classes shipped which are used making the complete bundle tiny and faster
- Has common utility patterns
- Don't have to invent complex class names
- Development speed 🚀🚀🚀

We can control the layout, color, spacing, typography, shadows, and more to create a completely custom component design without even leaving HTML / JSX(react) or writing a single line of custom CSS.


PS: [Documentation](https://tailwindcss.com/docs/installation) is amazing!

![explosion-boom.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1662809724105/LU323fP4L.gif align="center")


### Square Bracket notation 
There are predefined classes like below but what if we want to specify that value? For that, we can use the square notation [ ] for dynamic values.
```
Predefined Classes
h-4 for 1rem
h-5 for 1.25rem
h-6 for 1.5rem
h-7 for 1.75rem
h-8 for 2rem

Customized Class
h-[1.3rem]
```


### Intellisense for VS-Code

Now don't sweat it, thinking you will have to remember those classes. We don't need to remember any Tailwind class because we have got one special VS-Code extension [Intellisense for VS-Code](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss ) which makes the development experience so convenient and easy because of its accurate suggestions. Install [this](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss ) extension now!

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662807358221/GISl0Agpm.png align="center") Here you can notice suggestions made by this extension. One more thing you can use Ctrl + Spacebar to check existing suggestions for tailwind classes




### Let's see one simple example to make a Pay Now button...

```
<button class="h-10 px-6 font-semibold rounded-md bg-black text-white" type="submit">Buy Now</button>
``` 
![Button.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1662807756173/FRwFiFjk7.jpg align="center")

That's it! Now you can see how easy it becomes to use Tailwind CSS, we just need to specify classes and in all this extension really helps to make the development experience better and faster. 
Here,
   
> - h-10 -> fixed height of 10 units ( 2.5rem )
- px-6 -> padding along x-axis 
- rounded-md -> Medium rounded corners
- bg-black -> black background
- text-white -> White text
You would have noticed that classes are so intuitive.


<br><hr>
![one tailwindcss over other styling.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1662809258096/4mjrX4dwR.jpg align="center")

![two tailwindcsstony.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1662809365800/hNV4thmKY.jpg align="center")

*But yeah Mr. Stark is also right!*