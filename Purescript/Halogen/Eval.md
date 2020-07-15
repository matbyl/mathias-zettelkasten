20200711124408
# Eval
The eval function descripes all the ways a component can evaluate [HalogenM](20200710163523) code in response to an event. An eval function is typically created when calling `mkEval` which takes an `EvalSpec` that is fully defined as:

```purescript
type EvalSpec state query action slots input output m =
  { handleAction :: action -> HalogenM state action slots output m Unit
  , handleQuery :: forall a. query a -> HalogenM state action slots output m (Maybe a)
  , initialize :: Maybe action
  , receive :: input -> Maybe action
  , finalize :: Maybe action
  }
```

For convinience Halogen also supplies you with a `defaultEval` record which does nothing by itself as can be seen below when looking at the definition:

```purescript
defaultEval =
  { handleAction: const (pure unit)
  , handleQuery: const (pure Nothing) -- we'll learn about this when we cover child components
  , initialize: Nothing
  , receive: const Nothing -- we'll learn about this when we cover child components
  , finalize: Nothing
  }
```