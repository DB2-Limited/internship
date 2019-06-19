# Lecture 3

### HTML5 & CSS3 intro
###### HTML 5
- **New Doctype:** HTML5 has a new doctype function where you only need to write and you are ready to go. There is no struggle of memorizing complicated and difficult codes. The declaration is very simple in this version and it allows browsers to render page in the standard mode.
- **Media Support:** HTML5 brings you an outstanding audio and video support. You can easily add audio and video files to make your website look lively and engaging.
- **Flawless content editing:** The current HTML version has an attribute called contenteditable that helps you edit content quickly and easily. This can help in taking advantage of local storage and various other uses.
- **Article and Section:** The HTML5 is provided with two semantic tags `<article>` and `<section>` to help you increase your search engine visibility. This will facilitate users to compose an article into multiple sections and integrate multiple articles into a single section.
- **The Figure element:** The previous versions of HTML lack the ability to provide any caption for the image. The previous HTML versions did not provide any way to associate the caption to make it more informative and comprehensive. However, in HTML5 there is new figure element which can be combined with element in order to easily associate caption with the other elements of an image.

###### CSS 3

- **Box Shadows:** This is a new feature that allows a content slide beneath are such as footer and it gives an appearance as if it is coming out or sinking into the website. This process is pretty simple and there is no need for the developer to create a new image using JavaScript plugin.
- **Border Images:** CSS3 has introduced a new feature that is border images. This feature allows you to exchange a border with an image. It helps you specify an image in place of a plain solid coloured border.
- **CSS3 selectors:** CSS selectors are more updated and improved in CSS3 version. With these selectors, DOM elements can be chosen on the bases of their attributes easily. There is no need to specify classes and ID’s for each and every element. You can use the field elements to perform styling functions.
- **Font Additions:** Adding fonts is easy in CSS3 and all you need to do is just upload the file to your server, link to the CSS file and add fonts as per your choice.
- **Opacity levels:** In previous versions, designers had to create a new image or make use of CSS filters. But in CSS3, you simply have to provide an input that will get the desirable effects.

### Semantic HTML
- The semantic elements added in HTML5 are:
    - `<article>`
    - `<aside>`
    - `<details>`
    - `<figcaption>`
    - `<figure>`
    - `<footer>`
    - `<header>`
    - `<main>`
    - `<mark>`
    - `<nav>`
    - `<section>`
    - `<summary>`
    - `<time>`
- Elements such as `<header>`, `<nav>`, `<section>`, `<article>`, `<aside>`, and `<footer>` act more or less like `<div>` elements. They group other elements together into page sections. However where a `<div>` tag could contain any type of information, it is easy to identify what sort of information would go in a semantic `<header>` region.
- https://www.w3schools.com/html/html5_semantic_elements.asp
![semantic first example](./semantic1.jpg)

```html
<header></header>
<section>
    <article>
        <figure>
            <img>
            <figcaption></figcaption>
        </figure>
    </article>
</section>
<footer></footer>
```
```html
<div id="header"></div>
<div class="section">
    <div class="article">
        <div class="figure">
            <img>
            <div class="figcaption"></div>
        </div>
    </div>
</div>
<div id="footer"></div>
```

### CSS Frameworks
- Bootstrap - https://getbootstrap.com/
- Foundation - https://foundation.zurb.com/
- Bulma - https://bulma.io/
- Semantic UI - https://semantic-ui.com/
- Materialize - https://materializecss.com/
- Pure - https://purecss.io/
- Skeleton - http://getskeleton.com/
- ... *many more*
- https://saravanakumargn.github.io/css-frameworks-compare/ *compare css frameworks*
- https://youtu.be/FEs2jgZBaQA?t=860 *why you don`t need css framework*
- https://medium.com/magnetcoop/do-you-really-need-a-css-framework-767a8434eb76

### TBD
