# https-git.generalassemb.ly-WebDev-Connected-Classroom-react-blog-lab-blob-master-README.md

# React.js Blog App


In this lab, you will be creating a simple blog app using what you learned in the React Intro lesson. 

## Initial Setup

First, let's set up our blog app:

```bash
$ create-react-app blog-app
$ cd blog-app
$ npm run start
```
## 1. Create a blog Post component
* Tell react to render a `<Post...>` component inside of the `App` component
* Give that component the below properties, and pass some data to those properties.
  1. `title`
  2. `author`
  3. `body`
  4. `comments` (array of strings)
* The HTML (or more accurately, JSX) composition of your Post is up to you.

**Hint:** To avoid errors, you can either delete CSS files, or change them to reflect that we are using Post instead of App.

## 2. Add Nested components to blog

### Nested Components 

It would be a pain to have to explicitly define every comment inside of `<Post/>`, especially if each comment itself had multiple properties.
* This problem is a tell tale sign that our separation of concerns is being stretched, and its time to break things into a new component.

We can nest Comment components within a Post component.
* We create these comments the same way we did with posts: `extends Component` and `.render`
* Then we can reference a comment using `<Comment />` inside of Post's render method.

Let's create a new file for our Comment component, `src/Comment.js`...

```js
import React, {Component} from 'react'

class Comment extends Component {
  render () {
    return (
      <div>
        <p>{this.props.body}</p>
      </div>
    )
  }
}

export default Comment
```

Then in `src/Post.js`, we need to load in our `Comment` component and render it inside of our `Post` component...

```js
import React, { Component } from 'react';
// Load in Comment component
import Comment from './Comment.js'
import './App.css';


class Post extends Component {
  render() {
    return (
      <div>
        <h1>{this.props.title}</h1>
        <p>By {this.props.author}</p>
        <div>
          <p>{this.props.body}</p>
        </div>
        <h3>Comments:</h3>
        // Render Comment component, passing in data
        <Comment body={this.props.comments[0]} />
      </div>
    );
  }
}

export default Post;
```

> **Note**: We could put all of our code in one file, but it's considered a good practice to break components outs into different files to help practice separation of concerns. The only downside is we have to be extra conscious of remembering to **export / import** each component to where its rendered.


## 3. More hints for adding comments

Using what you've just learned, amend your `Post`'s render method to include reference to a variable, `comments`, that is equal to the return value of generating multiple `<Comment />` elements. Make sure to pass in the `comment` body as an argument to each `Comment` component. Then render the `comments` some where inside the UI for a `Post`.

> **NOTE:** You can use `.map` in `Post`'s `render` method to avoid having to hard-code all your `Comment`'s. Read more about it [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) and [here](http://cryto.net/~joepie91/blog/2015/05/04/functional-programming-in-javascript-map-filter-reduce/), and of course probably the best example the [React Docs](https://reactjs.org/docs/lists-and-keys.html)
>
> **HINT I:** You should only have to return one `<Comment />` inside of `.map`.
>
> **HINT II:** Remember that whenever you write vanilla Javascript inside of JSX, you need to surround it with single brackets (`{}`).

> **HINT III:** Read your erros, and google them!

## 4. Implement State 

Implement `state` in our Blog by making `body` a mutable value.

1. Initialize a state using a `constructor()` method for our `Post` to set a initial state. It should create a state value called `body`. Set it to the `body` of your hard-coded `post`.
2. Modify `Post`'s `render` method so that `body` comes from `state`, not `props`.
3. Add a button to `Post`'s `render` method that triggers `handleClick`.

## 5. Change state with user input
  * Create a `edit` method inside `Post` that updates `body` based on a user input, `onClick`.
  * You should use `setState` somewhere in this method.
  * How can you get a user input? Keep it simple and start with `prompt`.
