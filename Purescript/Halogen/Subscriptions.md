20200712201143
# Subscriptions
Components can subscribe to event sources which can either be time-based events or an event that happens on a DOM element outside of what is rendered such as the browser window. An event source can be thought of as a stream of actions that when subscribed is evaluated by the component. Subscribing to an event usually happen as part of the [initialize lifecycle event](20200711124011). When subscribing an id will be returned that lets you unsubscribe from the event. A component automatically unsubcribes from all subscriptions when running the `[finalize` lifecycle event](20200711124011).  There are also other ways to unsubscribe from a subscription such as:

```purescript
timer :: forall m. MonadAff m => EventSource m Action
timer = EventSource.affEventSource \\emitter -> do
  fiber <- Aff.forkAff $ forever do
    Aff.delay $ Milliseconds 1000.0
    EventSource.emit emitter Tick

  pure $ EventSource.Finalizer do
    Aff.killFiber (error "Event source finalized") fiber
```

> Event sources are usually created with one of these functions:

> 1.  `effectEventSource` and`affEventSource` let you produce an event source from an `Effect` or `Aff` function, respectively.
> 2.  `eventListenerEventSource` lets you produce an event source by attaching an event listener to the DOM, like attaching a resize event to the browser window.

#subscriptions #event-source #event-sources

