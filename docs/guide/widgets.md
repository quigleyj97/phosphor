# Phosphor Widgets

Widgets are the underpinning of Phosphor's component framework. Widgets use
message passing to communicate with one another, and can have other widgets as
their children. These children are maintained by a Layout.

## Hello World

Creating a hello world in Phosphor is very simple:

```ts
import { Widget } from "@phosphor/widgets";

class HelloPhosphor extends Widget {
    constructor() {
        super();
        this.node.innerText = "Hello, Phosphor!";
    }
}
```

Here, we've created a `Widget` that simply displays `Hello, Phosphor!`.
`this.node` is the DOM node of the Widget- you can pass this directly to other
libraries like jQuery or D3.

Adding event handlers is also straight-forward:

```ts
class InteractiveHello extends HelloPhosphor {
    public handleEvent(ev: Event) {
        if (ev.type === "click") {
            alert("Hello again!");
        }
    }

    protected onAfterAttatch() {
        this.node.addEventListener("click", this);
    }

    protected onBeforeDetatch() {
        this.node.removeEventListener("click", this);
    }
}
```

What we've done here is add some _message handlers_- these are a core part of
how Phosphor works. `onAfterAttatch` is called when a widget is attached to the
DOM, and `onBeforeDetatch` is called just before the widget will be detatched.
[`#handleEvent()`](https://developer.mozilla.org/en-US/docs/Web/API/EventListener)
is part of the HTML EventListener API, and makes adding and removing event
handlers more convenient when working with classes.