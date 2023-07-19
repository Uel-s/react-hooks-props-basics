# PROPS

`React Component` => is a _function_ that takes _props_ as an argument and returns _JSX_

### Making Components Dynamic


```jsx
function BlogContent(props) {
  return <div>{props.articleText}</div>;
}
```

where does `props.articleText` come from?


### Passing Information

info is passed from parent component to child component, this is called `props.`

**passing info from `BlogPost` down to `BlogContent`

```jsx
function BlogPost() {
  return (
    <div>
      <BlogContent articleText="Dear Reader: Bjarne Stroustrup has the perfect lecture oration." />
    </div>
  );
}
```
This value is accessible from within the `BlogContent` component as `props.articleText`!

`it should be like this;`

```jsx
// BlogPost.js
// PARENT COMPONENT
function BlogPost() {
  return (
    <div>
      {/* BlogContent is being returned from BlogPost */}
      {/* Therefore, BlogContent is a child of BlogPost */}
      <BlogContent articleText="Dear Reader: Bjarne Stroustrup has the perfect lecture oration." />
    </div>
  );
}

// BlogContent.js
// CHILD COMPONENT
function BlogContent(props) {
  return <div>{props.articleText}</div>;
}
```


To assign a **prop** to a **component** we use attributes just like in `html`


```jsx
function ParentComponent() {
  // passing prop to ChildComponent
  return <ChildComponent text="Hello!" number={2} />;
}

`passing down to child`

function ChildComponent(props) {
  // using the values of the text and number props
  return (
    <div>
      {props.text} {props.number}
    </div>
  );
}
```

`But remember, this is JSX and not HTML!`

**props** => Can be any data type.

for parent component to pass info to child component we use **props**

If we add a `console.log` in the `BlogContent` component to inspect the props:

```jsx
// BlogContent.js
function BlogContent(props) {
  console.log(props);
  return <div>{props.articleText}</div>;
}
```
I'll see the article content.

`more info can be added`

```jsx
<BlogContent
  articleText="Dear Reader: Bjarne Stroustrup has the perfect lecture oration."
  isPublished={true}
  minutesToRead={1}
/>
```
**carly braces {} are used in all data type expect strings**

## expanding BlogContent components 

```jsx
function BlogContent(props) {
  console.log(props);

  if (!props.isPublished) {
    // hide unpublished content
    // return null means "don't display any DOM elements here"
    return null;
  } else {
    // show published content
    return (
      <div>
        <h1>{props.articleText}</h1>
        <p>{props.minutesToRead} minutes to read</p>
      </div>
    );
  }
}
```
`here we are using conditional rendering to display blog content if published`

### Expanding our Application.

The `Comment Component`

```jsx
function Comment(props) {
  return <div>{props.commentText}</div>;
}
```
```jsx
function BlogPost() {
  return (
    <div>
      <BlogContent articleText="Dear Reader: Bjarne Stroustrup has the perfect lecture oration." />
      <Comment commentText="I agree with this statement. - Angela Merkel" />
      <Comment commentText="A universal truth. - Noam Chomsky" />
      <Comment commentText="Truth is singular. Its ‘versions’ are mistruths. - Sonmi-451" />
    </div>
  );
}
```

`in html it should lok like this`


```html
<div>
  <div>Dear Reader: Bjarne Stroustrup has the perfect lecture oration.</div>

  <div>I agree with this statement. - Angela Merkel</div>

  <div>A universal truth. - Noam Chomsky</div>

  <div>Truth is singular. Its ‘versions’ are mistruths - Sonmi-451</div>
</div>
```

**********************************************************************************************************************************

`BlogPost.js`
```js
import React from "react";
import BlogContent from "./BlogContent";
import Comment from "./Comment";

function BlogPost() {
  return (
    <div id="blog-post">
      <BlogContent articleText="Dear Reader: Bjarne Stroustrup has the perfect lecture oration." />
      <Comment commentText="I agree with this statement. - Angela Merkel" />
      <Comment commentText="A universal truth. - Noam Chomsky" />
      <Comment commentText="Truth is singular. Its ‘versions’ are mistruths. - Sonmi-451" />
    </div>
  );
}

export default BlogPost;

```

`Comment.js`

```js

import React from "react";

function Comment(props) {
  return <div className="comment">{props.commentText}</div>;
}

export default Comment;
```


`BlogContent.js`

```js
import React from "react";

function BlogContent(props) {
  return <div id="blog-content">{props.articleText}</div>;
}

export default BlogContent;
```


`App.js`

```js
import React from "react";
import BlogPost from "./BlogPost";

function App() {
  return <BlogPost />;
}

export default App;

```








