20200705202807
# Components
Halogen uses a component architecture that lets you split up UI into independent reusable pieces. A component in contrast to elements maintains an internal state that is possible to update and may react on effects such as values changing over time and network requests. Think of a component architecture like small individual elm applications that you are able to stitch together.

### Building a Basic Component (With Types)
>A typical Halogen component accepts input, maintains an internal state, produces Halogen HTML from that state, and updates its state or performs effects in response to events.

##### Input
If your component thats an input then that is expressed through a type such as: `type Input = Int`
If a component does not take any input it is most commonly expressed with a type variable: `forall i. ...`

##### Component
A component maintains an internal state which is expressed through a type, for example: `type State = Int`
A component also requires an `initialState` which takes the `Input` and procuces the `State`: `Input -> State`
A component that does not take any input will then be: `forall i. i -> State`

##### Actions
A component can update state, react to events and perform effects. Halogen uses `Actions` to determine how to handle internal events. For example in a counter example the actions may look like the following: `type Actions = Increment | Decrement`

An action type should be paired with a function: `handleAction :: forall o m. Action -> H.HalogenM State Action () o m Unit`

>* The type `()` means our component has no child components. We could also leave it open as a type variable because we aren't using it -- `slots`, by convention -- but `()` is so short you'll see this type commonly used instead.
>* The `o` type parameter is only used when your component communicates with a parent.
>* The `m` type parameter is only relevant when your component performs effects.

Halogen provides several ways to update the internal state inside a component.
 * `modify` updates the state given the previous state and gives back the new state
 * `modify_`same as the previous but it doesn't return the new state which and underscore typically indicates by convention.
 * `get` retrieves the current state
 * `gets` retrieves the current state and applies a function to it

#action #handle-action

##### Render
A component uses a `render` function to produce the HTML. This function is pure, meaning that it will not create any effects it will only take the internal state and based on the render the HTML. Halogen handles the re-rendering of the component when the internal state is updated. The `render` function has the following type signature: `render :: froall m. State -> H.ComponentHTML Action () m`

`H.ComponentHTML` is a more specialized version of `HTML` meant for components since they also specify action, child components and the monad which represent the effects that can run inside the component.


 
