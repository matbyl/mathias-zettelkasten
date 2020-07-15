20200710163523
# Performing effects

## HalogenM
[HalogenM](https://pursuit.purescript.org/search?q=HalogenM) also called the eval monad is an important part of Halogen. It lets you access Halogen specific features to update state (i.e. `modify`), forking threads, starting subscriptions amongst others. This monad only handles Halogen specific features and does not concern itself with effects. The monad lets you specifiy the other capabilties you want by defining the type variable `m`. Typically this is done by constraining the monad instead of defining the monad directly which gives the user more flexibility.

Example of defining the monad directly:
```purescript
handleAction :: forall output. Action -> HalogenM State Action () output Aff Unit
```

Example of putting constraints on the monad `m`:
```purescript
handleAction :: forall output m. MonadAff m => Action -> HalogenM State Action () output m Unit
```

#HalogenM #type-constraints #type-constraint


## handleAction

The `handleAction` function which is part of a Halogen components [eval](20200711124408) function and handles all the impure actions that the component depends on. It is usually a good idea to do batch updates on the component state when possible to avoid unecessarray re-rendering.