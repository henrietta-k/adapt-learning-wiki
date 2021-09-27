To understand the ChildView API it is helpful to review how rendering works in Adapt.

After a view is rendered it continues by rendering its immediate children. Once the immediate children have been rendered, the first of these children renders its immediate children, then the second child renders its immediate children and so on. The order can be described as an immediate children first approach. The process continues until all descendents have been rendered or the process is halted. When rendering a page the effect, then, is to first render articles, then blocks, then components.

Before each view is rendered an event is dispatched allowing listeners to halt the process. The process can be halted either immediately, which prevents the render of the view, or immediately _after_ the view is rendered. In either case no _descendents_ of the view are rendered.

Rendering can be halted by calling `stop` on the `ChildEvent` instance.

If rendering is halted subsequent rendering can be performed by calling `addChildren`.

`ContentObjectView` provides a `renderTo` function which will force rendering up to the given view, ignoring any requests to halt the process. This function returns a promise that will resolve when the necessary views have rendered.

## Event overview

The following events are triggered on the global `Adapt` object during the rendering process.

Event | Argument | Description
----- | -------- | -----------
`view:addChild` | `ChildEvent` | Triggered by the parent view prior to adding an immediate child view. Listeners may use this event to prevent the child from being rendered or just prevent the child's descendents being rendered.
`view:childAdded` | `parentView`, `childView` | Triggered by the parent view after a child is rendered.
`view:requestChild` | `ChildEvent` | When the parent view reaches the end of the list of its available children it will trigger this event (if permitted). Listeners can respond by supplying a model to be rendered via the event object.

## ChildEvent class

Function | Argument | Description
----- | -------- | -----------
`model`&nbsp;`(get/set)` | `AdaptModel` | A listener responding to `view:requestChild` should use this function to specify which model should be rendered next by the parent view.
`reset` | | Use this function to cancel any calls to `stop` that may have happened up to the present time.
`force` | | This function when called will tell the parent view to disregard any calls to `stop`.
`stop` | `immediate=true` | Halt the render of the current view. If `immediate` is set to `true` the view will not be rendered, if `false` only its descendents will not be rendered.
`stopNext` | | Shorthand for calling `stop(false)`.
`close` | | When called this indicates that no further processing of the event will take place and the final decision of what, if anything, is to be rendered.
