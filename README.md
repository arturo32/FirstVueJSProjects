# FirstVueJSProjects
Learning and practicing VueJS

## Comments
First project in VueJS. I followed <a href="https://www.youtube.com/watch?v=cSa-SMVMGsE">this video</a> to make it both using CDN (all project in a single HMTL file) and CLI (complete project with separate component files) versions. You can add comments to a list with or without author (Anonymous) and delete them later. <br/>
![Comments site](https://github.com/arturo32/FirstVueJSProjects/blob/master/images/comments.gif)

## Converter
I got inspired by <a href="https://www.youtube.com/watch?v=tIEa3MRBpI0&t=1820s">this video</a> to make this currency converter. I made it show the value converted instantly as the user types in the input boxes. I also made a main input box with a dropdown list ("stole" and adapted from <a href="https://github.com/arturo32/arturo32.github.io">my other project</a>) for the user to be able to choose a base currency that it's present in every other "converter box". Data is from https://exchangeratesapi.io/ API.<br/>
![Converter site](https://github.com/arturo32/FirstVueJSProjects/blob/master/images/converter.gif)

## Calculator
Other project inspired by other <a href="https://www.youtube.com/watch?v=m1_ih43p24s">video</a>. A complete basic calculator. This one I wasn't very happy with the logic used in the video, so I made some changes like showing the operations in the display. I plan to remade this code entirely in the future as its core logic is too close to the view component (as some of the comments of the video have pointed out). <br/>

![Calculator site](https://github.com/arturo32/FirstVueJSProjects/blob/master/images/calculator.gif)


##To-do Manager
My study on Vuex. This time it comes from <a href="">this video</a>. I find amazing the similarity with Redux from React. It has actions and functions that use the actions to change the state of a component (called reducers in Redux and mutations in Vuex). <br/>
There are three components: Todos, that stores the list of to-dos, AddTodo, the form for adding the to-dos and FilterTodos, the dropdown list for choosing how many to-dos are shown. They all share the same state by using Vuex. The initial state, i.e., the to-dos that appears when you first enter the site, is fetched from https://jsonplaceholder.typicode.com/, a "fake" API. <br/>
I really liked the style that the author of video applied in the site and I made small changes to make it a little better. It is also delightfully responsive! <br/>

![To-do Manager site](https://github.com/arturo32/FirstVueJSProjects/blob/master/images/vuex-todo-manager.gif)