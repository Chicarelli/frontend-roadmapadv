# Web Components

It consists of three main technologies:

- Custom Elements
    - Set of Javascript APIs to define custom elements
- Shadow DOM
    - Javascript APIs for attaching an encapsulated shadow DOM to an element. Which is rendered separately from the main document.
- HTML templates
    - Elements that enable you to write markup templates that are not displayed in the rendered page.


# Custom Elements

There are two types:

- Autonomous Custom Elements
    - Inherits from the HTML element base class
    Have to implement it's behavior from scratch.
- Customized built-in elements
    - Inherits from standard HTML elements, eg HTMLImageElement
    - It extends the behavior of specific instances of the standard element.

## Difference in implementation:

```javascript
//Customized built-in elements.
class WordCount extends HTMLParagraphElement {
    constructor() {
        super();
    }

    //...
}
```

```javascript
//Autonomous custom elements

class PopupInfo extends HTMLElement {
    constructor() {
        super();
    }

    //...
}
```

## Lifecycle callbacks

- *connectedCallback()*
    - Called each time the element is added to the document.
    Devs should implement custom elements setup in this callback rather than the constructor.
- *disconnectedCallback()*
    - Called when the element is removed from the document.
- *adoptedCallback()*
    - Called when it is moved to a new document.
- *attributeChangedCallback*
    - Called when attributes are changed, added, removed or replaced.

See the _logging-lifecycle-events.html_ to an example of using the above callbacks

## Defining a custom element.

```javascript
// Defining the custom element
    customElements.define("my-custom-element", MyCustomElement);
```
The **define()** method takes the following arguments:

- *name*: The name of element. Must start with lowercase, contain a hyphen, and satisfy some other rules: https://html.spec.whatwg.org/multipage/custom-elements.html#valid-custom-element-name
- *constructor*: The custom element's constructor function.
- *options*: Only for customized built-in function. Is an object containing a single property extends. 
```javascript
customElements.define('word-count', WordCount, {extends: 'p'});
```

## Using
```html
<!-- For customized built-int element -->
<p is="word-count"></p>
<!-- <word-count></word-count> will not work if it's a custom built in element. -->

<!-- or autonomous custom element -->
<popup-info></popup-info>
```

TODO: Custom states and custom state pseudo-class CSS selectors
