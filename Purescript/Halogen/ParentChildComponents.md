20200712203345
# Parent Child component
Halogen does not dictate a certain architecture in contrast to [elm](20200705164508). It is possible to use Halogen in a component style where the application is defined by many components. It's also possible to have the whole application in a single component by which you get an elm like architecture. When using several components though it is necesarry to be able to communicate between the components.

There are three means of communication between a parent and a child component, Input, Output and Query.

## Input
The most common way of communication is Input. The Input type is defined by the child and the value is given to the child by the parent. The input value is updated everytime the parent i re-rendered.

## Output
To communicate from the child to the parent it is possible to emit some output. This can make a component more flexible since parent components may act differently from one another. An example of when it might be good to use Output instead of input is when closing a modal this way the parent can decide what should happen when the modal is closed.

## Query
Yet another way to communicate between the child and the parent is to perform queries. This may be in a tell-style, where the parent is telling the child to do something, or in request-style where the parent requests something from the child.