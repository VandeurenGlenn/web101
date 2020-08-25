```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
    
  </body>
  
  <script>
  
    // but js code in here for now
    
  </script>
</html>
```

```js
class PubsubButton extends HTMLElement {
  
  static get observedAttributes() {
    return ['event', 'value']
  }
  
  constructor() {
    super(); // always call super() first in the constructor.
    // TIP: Bindings happen in the constructor (best practice)
    // example
    // this.ondoubleclick = this.ondoubleclick.bind(this)
  }
  
  connectedCallback() {
    // TODO: add eventListener and publish on click
    // put this inside the listener callback -> pubsub.publish(this.event, this.value)
    
    // TIP: Create a function for the callback and bind it in the constructor,
    // Creating a function/method makes it possible to removeEventlistener,
    // after diconnect (left the DOM)
    
    // TIP: before adding the pubsub.publish code, add a console.log('click') instead
  }
  
  disconnectedCallback() {
    // removeEventlistener
  }
  
  /**
   * called whenever an observed attribute changes
   */
  attributeChangedCallback(name, oldValue, value) {
    this[name] = value
  }
}
```