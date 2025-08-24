# IMPORTANT!
this is mainly just speculation, based on the hackathon teaser image. almost none of this is confirmed, and is absolutely opinionated slightly by me. along with this, there is no defined types for any of these, so assume most of these are type `any` as of when i'm writing this (aug 23rd, 2025) if anyone involved in the project wants to give input for this, i will happily edit this to be more accurate

## gurt browser things
- `gurt.body`
    returns the body element
- `gurt.log(message)`
    logs a message to console
- `gurt.select(selector)`
    returns an element based on the selector (selector most likely being an ID or className)
- `gurt.selectAll(selector)`
    returns a table of elements based on the selector
- `gurt.create(tagName, attributes)`
    creates and returns an element based on the tag name, with the attributes table defining its attributes (duh)
### crumbs
assuming these act similar to standard web cookies. unsure if they're sandboxed, though they absolutely should be.
- `gurt.crumbs.set({name, value, lifetime})`
    sets crumb `name` to `value`, expiring after `lifetime`. unsure if `lifetime` is a number, or string for different length formatting. needs more info
- `gurt.crumbs.get(name)`
    returns value of crumb `name`. unsure if it returns crumb lifetime, needs more info
- `gurt.crumbs.delete(name)`
    deletes crumb `name`.
- `gurt.crumbs.getAll()`
    returns a table (or dictionary? not sure) of all the current active crumbs. needs more info
    i swear if this isn't sandboxed this will cause MANY issues

## standard library
prob similar to `gurt` but not directly browser related
- `setInterval(callback, time)`
    repeatedly runs `callback` every `time` seconds (unconfirmed), returns an `id`
- `clearInterval(id)`
    stops interval `id` from running
- `setTimeout(callback, time)`
    runs `callback` after `time` seconds (unconfirmed), returns an `id`
- `clearTimeout(id)`
    stops timeout `id`
- `fetch(url, options)`
    fetches data from `url` with the specified options (possibly being a table or custom object)
    
## Element
there are a LOT of items in this list, some of which i'm not 100% sure how they work. hopefully helps with the general idea?
- `element.text`
    string, the text of said element. likely only available on elements that have a text value, like `<h1>hi</h1>`
- `element.value`
    best guess, returns all attributes as a table. more info needed
- `element.visible`
    boolean, determines whether or not the element is being rendered
- `element.children`
    table of elements, which are the children of the element
- `element.parent`
    parent of the element
- `element.nextSibling`
    element after this element
    ```
    <div>
        <div></div> -- element.previousSibling
        <h1></h1> -- the element the value is being grabbed from
        <p>test</p> -- element.nextSilbing
    </div>
    ```
- `element.previousSibling`
    similar to element.nextSibling, but backwards.
- `element.firstChild`
    the first element that is a child of this element
    ```
    <div>
        <div></div> -- element.firstChild
        <h1></h1>
        <p>test</p> -- element.lastChlid
    </div>
    ```
- `element.lastChild`
    the last element that is a child of this element
- `element:append(chlid)`
    adds element `child` as a child of this element
- `element:remove()`
    removes this element from the DOM
- `element:insertBefore(newChild, referenceChild)`
    inserts `newChild` before `referenceChild` in this element's children
- `element:insertAfter(newChild, referenceChild)`
    inserts `newChild` after `referenceChild` in this element's children
- `element:replace(newChild, oldChild)`
    replaces `oldChild` with `newChild` in this element's children
- `element:clone(deep)`
    returns a clone of this element, `deep` determining whether or not it clones children as well
- `element:getAttribute(name)`
    returns attribute `name`'s value
- `element:setAttribute(name, value)`
    sets attribute `name` to `value`
- `element:show()`
    sets this element's visibility to true
- `element:hide()`
    sets this element's visibility to false
- `element:createTween()`
    returns a Tween, which can be customized and controlled.
- `element:on(eventName, callback)`
    calls `callback` whenever event `eventName` is fired inside this element. returns a `Subscription`, which can be unsubscribed from.
    most likely used for things like mouse hovering, or onClick stuff with buttons.
- `subscription:unsubscribe()`
    disconnects said subscription, stopping it from calling its callback on an event.
### classList
what i've gathered from this so far, classList is a list of classes that can be used for styling with CSS.
- `element.classList:add(className)`
    adds a class named `className` to the classList.
- `element.classList:remove(className)`
    removes class `className` from the classList.
- `element.classList:toggle(className)`
    toggles whether or not `className` is active/usable. needs more info
- `element.classList:contains(className)`
    returns a boolean, true if `className` is found within the classList, false otherwise.
- `element.classList:item(index)`
    returns the className at index `index`. needs more info
- `element.classList.length`
    int, the current length of classList

## Tween
- `tween:to(property, targetValue, duration, easing)`
    defines tween to property `property` of the parent element to `targetValue`, over `duration` seconds. easing can be applied, unknown exactly what `easing` is though
- `tween:from(property, startValue, duration, easing)`
    defines tween to property `property` of the parent element from `startValue` to its current value, over `duration` seconds, with `easing` easing applied.
- `tween:parallel()`
    returns a tween that will run in parallel with the parent tween. needs more info
- `tween:chain()`
    returns a tween that will run after the parent tween completes. needs more info
- `tween:stops(count)`
    tells the tween to repeat `count` times. harder to read, most likely incorrect. needs more info
- `tween:callback(function)`
    calls `function` once the tween is completed.
- `tween:play()`
    causes the tween to start playing. most likely stops any currently playing tweens if they're not parallel or chained. unsure if it starts the tween from the current position or from the start
- `tween:stop()`
    causes the tween to stop playing. most likely sets it back to start or final position. also likely stops any chained or parallel tweens from playing.
- `tween:pause()`
    pauses the tween, likely where it currently was. unsure how parallel tweens are affected, most likely not at all.
- `tween:resume()`
    resumes the tween. also unsure how parallel tweens are affected.

## Properties
- `opacity`
    how opaque the element is. likely on a scale of `0` to `1`, with 0 being invisible and 1 being fully opaque.
- `backgroundColor`
    background color, self explanatory. unsure whether or not it's a custom color object, or if it's just a table.
- `color`
    color, most likely for tinting things like images. needs more info
- `textColor`
    text color, color of text. self explanatory
- `width`
    width of element. unsure if it's like web, using a string that can have different endings like `px` or `%`, or if it's like Roblox, with an offset and scale. most likely web-like. needs more info
- `height`
    height of element. same issues as above
- `x`
    x position of element. same issues as above
- `y`
    y position of element. same issues as above
- `scale`
    the scale of the element. assuming it is a number, since scaling with anything besides a scale would be strange lol
- `rotation`
    the rotation of the element. unsure if it's in degrees or radians. needs more info

## Signal
- `Signal.new()`
    returns a `Signal` object.
- `signal:connect(callback)`
    returns a `Connection`, calls `callback` whenever the signal is fired.
- `connection:disconnect()`
    stops the callback from being called when the event is fired, also freeing up memory.
- `signal:fire(...)`
    fires all connections, giving the callback function `...` arguments.
- `signal:disconnect()` 
    not sure why this is here, assuming it acts as a "disconnect all connections". needs more info

## WebSockets
heads up, i don't know websockets very well. i'm just assuming how Gurted handles them through these functions
- `WebSocket.new(url)`
    returns a `WebSocket`, connected to url `url`.
- `ws:send(data)`
    sends `data` to its url. not sure about specifics, such as whether or not `data` is a json string, or a table, or just a value. needs more info
- `ws:close()`
    closes the WebSocket, stopping any data from being sent or received.
- `ws:on(event, callback)`
    calls `callback` whenever event `event` is fired. unsure on what the events are or could be, needs more info

## Time
- `Time.now()`
    likely returns a number of the current Unix time. needs more info
- `Time.format(timestamp, format)`
    returns a string, formatting `timestamp` based on `format`. unsure on what or how it's formatted, needs more info
