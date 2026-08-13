react notes
virtual dom helps for easier loading
single type - only updates affected parts

component based writing allows for reusable components to be written
jsx - javascript xml - allows html like code to be written in jsx
html -

class were used before hooks, they used this. shit
functions can manage states after hooks were introduced

stateless component do no manage data and receive data via props
state component manage their data and update the data on the basis of the user requirements
functions can be state or stateless

properties or props are way to pass data from parent to child, this is read only
child cannot update data

difference between state and props
state is dynamic, mutable, can be modified by its own component
props are immutable, need to be modified in the parent

control and uncontrolled
controlled are accessed thru state attributes
uncontrolled means u do not mean to validate the input, accessed thru ref

key attribute in react
used to identify which key has been updated instead of re rendering the complete list

fragments
used to avoid unnecessary div tags
grouping and reducing of dom

virtual DOM
reconciliation

react life cycle methods
mounting updating unmounting
creation update and removal of a component

mounting - initialise, render
updating- handles state prop changes, re renders, updates
unmounting - cleans up before removal

use effect hook - functional components to perform side effects such as fetching data, subscribing to services, or directly manipulating the DOM
The hook accepts two arguments: a callback function containing the side effect logic and an optional dependency array that controls when the effect runs. 

No Dependency Array: The effect runs after every render. 
Empty Dependency Array []: The effect runs only once after the initial mount. 
Specific Dependencies: The effect runs after the initial mount and re-runs whenever any value in the array changes

Prop drilling occurs when data is passed through multiple nested React components, even if intermediate components don’t use it, creating unnecessary chains of props.

Leads to harder-to-maintain code as the component hierarchy grows.
Can be avoided using state management tools like Context API or Redux.
bsaiucally to pass a prop from a parent to a granchchild u have to unnecessarily go thru the chil component
this can beavoided by using the usecontext hook

use context hook
create context
wrap parent in teh context provider
use the data being passed in other components by using use context

react router dom
strict mode in react




