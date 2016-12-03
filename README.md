# style-book
Generate style guide based on your css components as a Mithril SPA

## Ideea
**postcss-style-book** aims to be a tool that generates visual style guides for your CSS components, out of your CSS files.

## Research

1. there will be an interface that will parse the css file and it's associated source map file
2. main issue, of how to parse colors / vars

eg.

```css
/* less variable */
$color : red

/* post css variable handled by postcss-color-function */
--color: color(red shade(50%))
```

in order to not depend on any of postcss, less, etc, having in mind  #1 (that a compiled css file with comments will be used as the input) there should be a way to keep traking the vars ... maybe **source maps** is a viable solution; this way will have `style.css.map` that stores comments and variable names and `styles.css` that holds values. all we have to do is to ping-pong between these two.


## Example
having a the following css component named **list.css**

```css
:root {
  /*
  ---
  section: Colors
  title: Default brand colors
  ---
  Here should go **relevant** component description.
  */
  
  /* @start color */
  --color-brand: indianred; 
  --color-accent: lime;
  /* @end color */
}

/*
---
section: Components
title: List
data: fakeData-list.json
---
Default component to display a list of items.

<dl class="List">
  <dt class="List-Header u-paddingAs">{@listTitle || 'My List'}</dt>
  
  @iterable
    <dd class="List-Item">
      <span>{{@name || 'John Doe'}}</span>
      <strong>{{@score || '13'}}</strong>
    </dd>
  @iterable
</dl>

*/

.List {
   border-radius: 4px;
   background-color: var(--color-brand);
}

.List-Header {
  font-weight: 700;
}

.List-Item {
  padding:0;
  margin:0;
}

.List-Item:nth-child(even) {
  background-color:rgba(255, 255, 255, .6);
}

.List-Item:nth-child(odd) {
  background-color:rgba(255, 255, 255, .8);
}

/*Utility classes */
.u-paddingAs {
  padding: 4px;
}
```

**fakeData-list.json**

```json
{
	"title": "User List",
	"users": [{
		"id": 1,
		"name": "John Doe",
		"score": 99
	}, {
		"id": 2,
		"name": "John Doe's brother",
		"score": 999
	},
  {
		"id": 3,
		"name": "John Doe's sister",
		"score": 100
	}]
}
```


## Output 
*this should be usefull for both BE and FE programers.*
i intent to generate a *Mithil* based SPA (with routing), something, that visually, will look like this.

<img src="postcss-style-book.png" alt="PostCSS Style Book"/>

output should contain:

0. colors
1. typography / fonts used
2. icons (font icons or svgs)

this is a good example

<img src="https://dribbble.com/shots/2341689-UI-Styleguide/attachments/446967" alt="Dribble example"/>

## Other tools doing kind of the same work ..
* [a list with styleguide generators](https://github.com/davidhund/styleguide-generators)
* [styledown](https://github.com/styledown/styledown/tree/master)
* [postcss-styleguide](https://github.com/mdings/postcss-styleguide)  
* [postcss-style-guide](https://github.com/morishitter/postcss-style-guide)
