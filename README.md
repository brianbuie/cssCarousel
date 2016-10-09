cssCarousel
==========

A simple CSS-only item carousel

<p align="center">
	<img src="http://i.imgur.com/F0j1ubY.png" />
</p>

## Installation

- Include the CSS stylesheet:

	```html
	<link rel="stylesheet" href="csscarousel.css" />
	```            
- copy the following code and edit where necessary:
	
	```html
<section class="cssCarousel">

	<!-- radio id="" & label for="" are used only to link together, feel free to rename. -->

	<input type="radio" name="carousel-1" id="first-movie" />
	<input type="radio" name="carousel-1" id="arbitrary" />
	<input type="radio" name="carousel-1" id="unique-id" />
	<input type="radio" name="carousel-1" id="item-4" checked />
	<input type="radio" name="carousel-1" id="item-5" />
	<input type="radio" name="carousel-1" id="item-6" />
	<input type="radio" name="carousel-1" id="item-7" />
	<input type="radio" name="carousel-1" id="item-8" />
	<input type="radio" name="carousel-1" id="item-9" />
	<input type="radio" name="carousel-1" id="last-movie" />

	<div class="cssCarousel__viewport">
		<ul class="cssCarousel--7-items">
			<li>
				<label for="first-movie">
					<img src="" />
				</label>
				<div class="cssCarousel--showOnFocus">
				</div>
			</li>
			<li>
				<label for="arbitrary">
					<img src="" />
				</label>
				<div class="cssCarousel--showOnFocus">
				</div>
			</li>
			<li>
				<label for="unique-id">
					Any Content can go in here
				</label>
				<div class="cssCarousel--showOnFocus">
					Any Content in here too
				</div>
			</li>
			<li>
				<label for="item-4">
					<img src="" />
				</label>
				<div class="cssCarousel--showOnFocus">
					image size doesn't dictate carousel item size, use any image you want!
				</div>
			</li>
			<li>
				<label for="item-5">
				</label>
				<div class="cssCarousel--showOnFocus">
					Leave the item empty, It doesn't matter!
				</div>
			</li>
			<li>
				<label for="item-6">
					<img src="https://image.tmdb.org/t/p/original/vXjVd0Vu0MXRZnga7wEnHIIhO5B.jpg" />
				</label>
				<div class="cssCarousel--showOnFocus">
					<h1>Groundhog Day is a good movie</h1>
				</div>
			</li>
			<li>
				<label for="item-7">
					No need to add a "cssCarousel--showOnFocus" under the label, it's optional.
				</label>
			</li>
		</ul>
	</div> <!-- /cssCarousel__viewport -->
</section> <!-- /cssCarousel -->
	```

## Using more than 10 items
You can use any number of items (at least 2). edit the ul element class to reflect the number of items you have
```html
<ul class="cssCarousel--7-items">
```
deleting additional radio inputs is not necessary.

in order to use more than 10 elements, you'll need to create a few css rules, but they're pretty intuitive.

note: if you need 15 items, you'll need to create the appropriate rules and radio elements for 11, 12, 13, 14, and 15

On this section, every new item's definition is +100%
```css
/*
 * Carousel width based on number of items
*/
.cssCarousel--2-items{ width: 200%; }
.cssCarousel--3-items{ width: 300%; }
.cssCarousel--4-items{ width: 400%; }
.cssCarousel--5-items{ width: 500%; }
.cssCarousel--6-items{ width: 600%; }
.cssCarousel--7-items{ width: 700%; }
.cssCarousel--8-items{ width: 800%; }
.cssCarousel--9-items{ width: 900%; }
.cssCarousel--10-items{ width: 1000%; }
/* next item - width: 1100% */
```

Every new rule in this block adds +1 to inside both "nth-of-type" pseudo-class selectors and then -100% on the margin-left
```css
.cssCarousel > input:nth-of-type(1):checked ~ .cssCarousel__viewport > ul{ margin-left: 0; }
.cssCarousel > input:nth-of-type(2):checked ~ .cssCarousel__viewport > ul{ margin-left: -100%; }
.cssCarousel > input:nth-of-type(3):checked ~ .cssCarousel__viewport > ul{ margin-left: -200%; }
.cssCarousel > input:nth-of-type(4):checked ~ .cssCarousel__viewport > ul{ margin-left: -300%; }
.cssCarousel > input:nth-of-type(5):checked ~ .cssCarousel__viewport > ul{ margin-left: -400%; }
.cssCarousel > input:nth-of-type(6):checked ~ .cssCarousel__viewport > ul{ margin-left: -500%; }
.cssCarousel > input:nth-of-type(7):checked ~ .cssCarousel__viewport > ul{ margin-left: -600%; }
.cssCarousel > input:nth-of-type(8):checked ~ .cssCarousel__viewport > ul{ margin-left: -700%; }
.cssCarousel > input:nth-of-type(9):checked ~ .cssCarousel__viewport > ul{ margin-left: -800%; }
.cssCarousel > input:nth-of-type(10):checked ~ .cssCarousel__viewport > ul{ margin-left: -900%; }
/* next item -  margin-left: -1000% */
```

Last block to create, copy this to a new line and replace the number inside nth-of-type() 

```css
/* item 10 selected */
.cssCarousel > input:nth-of-type(10):checked ~ .cssCarousel__viewport > ul > li:nth-of-type(10) > label{
	transform: scale(1,1);
	opacity: 1;
}
.cssCarousel > input:nth-of-type(10):checked ~ .cssCarousel__viewport > ul > li:nth-of-type(10) .cssCarousel--showOnFocus{
	opacity: 1;
	top: 0;
}
```

and lastly, you'll have to add the appropriate radio element and item with label to the html:

```html
<input type="radio" name="slider2" id="matchingId" />
```

and the label for it on the 11th item:

```html
<label for="matchingId">
```

you can name the id whatever you want, just make sure the appropriate item label has a matching 'for' attribute

## Changing the carousel item size
in the css
```css
.cssCarousel__viewport{
	width: 60%;
	margin: 0 auto;
}
```
the viewport determines the width of all items

## Changing the item aspect ratio
cssCarousel uses the padding trick from bootstrap's responsive video container:
```css
.cssCarousel__viewport > ul > li > label{
	height: 0;
	/* 2:3 movie poster aspect ratio */
	padding-bottom: 150%;
}
```
The padding-bottom is calculated by using (height/width) multiplied by 100.
movie posters are 2:3, so (3/2) multiplied by 100 = 150

For a perfect square, you would use

```css
.cssCarousel__viewport > ul > li > label{
	/* (1/1)*100 = 100 */
	padding-bottom: 100%;
}
```

16:9 video aspect ratio is

```css
.cssCarousel__viewport > ul > li > label{
	/* (9/16)*100 = 56.25 */
	padding-bottom: 56.25%;
}
```

## Hideable content
Anything inside of the li element with a class of "cssCarousel--showOnFocus" will be hidden by default and shown when that item is in focus

## non-image content
Anything can be placed in the li or label elements, but will be constrained to the item's aspect ratio