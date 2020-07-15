20200705170512
# Rendering Halogen HTML
The Halogen **HTML module** is the smallest elements of an halogen application. They are not components but they need to be within a component to be rendered. The elements **can be thought of as DOM elements** although they actually are abstractions provided by the Halogen library which handles creating, updating and removing the DOM elements under the hood.

HTML elements accepts two arguments:
 * An array of attribtues, events and properties
 * An array of child elements

> Some HTML elements and properties clash with reserved keywords in PureScript or with common functions from the Prelude, so Halogen adds an underscore to them. That's why you see `type_` instead of `type` in the example above.

It is common to write helpers functions for the HTML module such as headers, lists, buttons and event a full design framework. Another common usecase is to only render HTML given a certain condition this could be achieved by writing abstractions such as:

```purescript

maybeElem :: forall w i a. Maybe a -> (a -> HH.HTML w i) -> HH.HTML w i
maybeElem val f =
  case val of
    Just x -> f x
    _ -> HH.text ""

whenElem :: forall w i. Boolean -> (Unit -> HH.HTML w i) -> HH.HTML w i
whenElem cond f = if cond then f unit else HH.text ""

```

#### IProp
The IProp type is typically used within the `Halogen.HTML.Properties` and `Halogen.HTML.Events` modules. IProp is a row type so that it is possible to uniquely  define events and properties given you more type safety. This helpt to ensure well formed HTML. For example a div does not support a placeholder property and thus Halogen will give us a compile-time error if we tried to add it to the array of properties.

#halogen #purescript #halogen-html #halogen-html-properties #halogen-html-events #iprop #row-type #row-types