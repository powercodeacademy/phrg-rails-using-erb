# Sinatra Views: Using ERB

## Overview

We'll look at the benefits of view templating and learn how to write erb tags to do more than just display data.

## Objectives

1. Define and explain the benefits of view templating
2. Use ERB substitution and scripting tags to modify the content and structure of HTML code
3. Incorporate logic and iteration using ERB. 


## Overview

Most major web frameworks provide some means of view templating, i.e. allowing the view, in our case an HTML document, to be constructed using a combination of HTML and Ruby code.

This allows us to greatly reduce duplication of HTML, as well as generate HTML that can change based on the data that is available. This is how Facebook can support 2 billion users - they create one template for the profile page which gets filled in with data from their servers representing each user. 

For this lesson, we will be using the ERB templating engine, which comes standard with every Ruby installation.

## Embedding Ruby

ERB and other templating engines allow us to modify the content and structure of our HTML code. With ERB, we do this using two different types of tags - the substitution, or `<%=` tag, and the scripting tag, or `<%` tag. 

### Substitution Tags

The substitution tag evaluates ruby code and then displays the results into the view. It opens with `<%=` and closes with `%>`. Inside of these tags, you can write any valid Ruby code that you want. 

In our `index.erb` file, add the following code: 

```erb
<%= "I love " + "Ruby!!" %>
```

This should render as: 

```
I love Ruby!!
```

The strings are concatenated first, then displayed on the page. Below this, add the following lines of code: 

```erb
<%= 1 + 1 %>
```

What do you think will be displayed? If you guessed `2`, you're right! In general, we use the substitution tags when we want to display some evaluation on the page.

We can wrap the substitution tags in any other HTML tags that we like. The code below will output: 

```erb
<h1><%= "I love " + "Ruby!!" %></h1>
```
 <h1>I love Ruby!!</h1>


### Scripting Tags

Scripting tags open with `<%` and close with `%>`. They evaluate, but do not actually display, ruby code. Add the following lines of code to index.erb:  

```erb
  <% if 1 == 2 %>
    <p>1 equals 2.</p>
  <% else %>
    <p>1 does not equal 2.</p>
  <% end %>
```

As you can see, only the second `p` tag was sent to the browser. This example is a little bit silly, because 1 will never be equal to 2. However, imagine if you were Facebook, and you had a method called `logged_in?` which returns true if a user is logged in, and false if they're not. You could then show different content based on whether or not a user was logged in. 

```erb
  <% if logged_in? %>
    <a href="/logout">Click here to Log Out</a>
  <% else %>
    <a href="/login">Click here to Log In</a>
  <% end %>
```

### Iteration

We can also use iteration to manage lists of items. For instance, given an array `squares = [1,2,4,8]`:

```erb
<ul>
<% squares.each do |square| %>
  <li><%= square %></li>
<% end %>
</ul>
```

Would produce:

```html
<ul>
  <li>1</li>
  <li>2</li>
  <li>4</li>
  <li>8</li>
</ul>
```

Notice that we use the substitution tag to display the value of the inner `square` variable. Again, imagine that Facebook wants to print out all of your wall posts on your profile page. They could store the posts in an array called `wall_posts`. Add the following line of code to your `index.erb` file: 

```erb
<% wall_posts = ["First post!", "Second post!", "Hello, it's your mother, why don't you ever call me?"] %>
```

Here, we're defining a variable called `wall_posts` and assigning its value to an array of strings. Now we can iterate through our wall_posts array and create a new `li` for each one. 

```erb
<ul>
<% wall_posts.each do |post| %>
  <li><%= post %></li>
<% end %>
</ul>
```

This should display: 

```html
<ul>
  <li>First Post!</li>
  <li>Second Post!</li>
  <li>Hello, it's your mother, why don't you ever call me?</li>
</ul>
```

## Video Review

* [Video Review- Forms](https://github.com/learn-co-curriculum/sinatra-video-review-forms) 

## Resources
[An Introduction to ERB Templating - Stuart Ellis](http://www.stuartellis.eu/articles/erb/)


<p data-visibility='hidden'>View <a href='https://learn.co/lessons/sinatra-using-erb'>Using ERB</a> on Learn.co and start learning to code for free.</p>

<p class='util--hide'>View <a href='https://learn.co/lessons/sinatra-using-erb'>Using ERB</a> on Learn.co and start learning to code for free.</p>
