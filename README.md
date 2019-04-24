# [Natours-Startup](https://jayli3.github.io/natours-startup/ "Natours-Startup")
`Live:` https://jayli3.github.io/natours-startup/

A mockup landing page for a travel agency startup. Completed with HTML & CSS.

## Goals
- Be up to speed with the most modern and advanced CSS properties and techniques;
- Be ready to build responsive layouts for all kind of devices and situations;
- Truly understand how CSS works behind the scenes;
- Be able to architect large CSS codebases for reusability and maintainability using Sass.

## Features & Code Snippets
The key features of this landing page are extracted and summarized below for future reference.

Project utilizes the **7-1 sass pattern** as well as the **BEM** (Block Element Modifier) to create scalable and maintainable code.

***Note that the code snippets are only the core codes that make the feature work, other styling (padding, margin, color etc) have been omitted in the snippet to save space.**

### `@keyframes` animations
----
By defining these reusable `@keyframes` blocks, I was able to animate the hero title, text and button.

[![Hero animations](https://github.com/jayli3/natours-startup/blob/master/readme_resources/gif01.gif?raw=true "Hero animations")](https://github.com/jayli3/natours-startup/blob/master/readme_resources/gif01.gif?raw=true "Hero animations")
```scss
@keyframes moveInLeft{
	0%{
		opacity: 0;
		transform: translateX(-10rem);
	}
	80%{
		transform: translateX(1rem);
	}
	100%{
		opacity: 1;
		transform: translateX(0);
	}
}

@keyframes moveInRight{
	0%{
		opacity: 0;
		transform: translateX(10rem);
	}
	80%{
		transform: translateX(-1rem);
	}
	100%{
		opacity: 1;
		transform: translateX(0);
	}
}

@keyframes moveInUp{
	0%{
		opacity: 0;
		transform: translateY(3rem);
	}
	80%{
		transform: translateY(-0.5rem);
	}
	100%{
		opacity: 1;
		transform: translateY(0);
	}
}
```


### Card Animations
----
Definitely the most difficult and fun to implement. It is achieved by creating 2 slides on top of eachother. 
First I define`backface-visibility: hidden;` so that the backside of any slide will not be visible when turned.
Then allow the backside to be initially turned 180 degrees. Then magic happens after applying `:hover` transitions!

[![ Cards Effects](https://github.com/jayli3/natours-startup/blob/master/readme_resources/gif07.gif?raw=true " Cards Effects")](https://github.com/jayli3/natours-startup/blob/master/readme_resources/gif07.gif?raw=true " Cards Effects")

```scss
.card{
	perspective: 150rem;
	-moz-perspective: 150rem;
	position: relative;
	height: 50rem;

	&__side{
		height: 50rem;
		width: 100%;
		backface-visibility: hidden;
		transition: all 0.8s ease;
		position: absolute;
		top: 0;
		left: 0;
		border-radius: 0.3rem;
		box-shadow: 0 1.5rem 4rem rgba($color-black, 0.15);
		overflow: hidden;

		&--front{
			background-color: $color-white;
		}

		&--back{
			transform: rotateY(180deg);
		}
	}
 
	&:hover &__side--front{
		transform: rotateY(-180deg);
	}

	&:hover &__side--back{
		transform: rotateY(0);
	}
}
```

### Image Hover Transitions
----
Hovering causes the target image to grow and increase its shadow while the rest of the images shrink and decrease its shadows to create a 3D effect.

[![Image Effects](https://github.com/jayli3/natours-startup/blob/master/readme_resources/gif06.gif?raw=true "Image Effects")](https://github.com/jayli3/natours-startup/blob/master/readme_resources/gif06.gif?raw=true "Image Effects")

```scss
.composition{
	position: relative;

	&__photo{
		width: 60%;
		box-shadow: 0 1.5rem 4rem rgba($color-black, 0.4);
		border-radius: 0.3rem;
		position: absolute;
		z-index: 10;
		transition: all 0.2s;

		&:hover{
			transform: scale(1.05) translateY(-0.5rem);
			box-shadow: 0 3.5rem 4.5rem rgba($color-black, 0.5);
			z-index: 20;
		}
	}

	&:hover &__photo:not(:hover){
		transform: scale(0.95);
		box-shadow: 0 0.5rem 2.5rem rgba($color-black, 0.3);
	}
}
```


### Story Section: hover effect & background video
----
The story section features other peoples experiences with the company. The interesting part of this section is the skewed effect of each review container as well as the hovering effect which displays their name and blurs their icon.

The parallelogram shape of background of the container is achieved by skewing it by x degrees (in this case -9 degrees as seen below), and making sure that the rest of the contents inside of the container itself is skewed 9 degrees (opposite of its parent container).

Now the wrapping around of the text to the shape of the image is achieved by using CSS propert called, shape-outside and giving its specified values. Note however, that this will only work if the element has defined dimensions (width and height as seen on the code below).

```scss
.story{
	width: 75%;
	margin: 0 auto;
	box-shadow: 0 3rem 6rem rgba($color-black, 0.1);
	background-color: rgba($color-white, 0.6);
	border-radius: 0.3rem;
	padding: 6rem 6rem 6rem 9rem;
	font-size: $default-font-size;

	transform: skewX(-9deg);

	& > *{
		transform: skewX(9deg);
	}

	&__shape{
		width: 15rem;
		height: 15rem;
		float: left;
		position: relative;

		transform: translateX(-3rem) skewX(9deg);

		-webkit-shape-outside: circle(50% at 50% 50%);
		shape-outside: circle(50% at 50% 50%);

		-webkit-clip-path: circle(50% at 50% 50%);
		clip-path: circle(50% at 50% 50%);
	}

	&__caption{
		position: absolute;
		top: 50%;
		left: 50%;
		opacity: 0;
		transform: translate(-50%, 20%);
		color: $color-white;
		text-transform: uppercase;
		font-size: 1.7rem;
		transition: all 0.3s;
		backface-visibility: hidden;
	}

	&:hover &__caption{
		opacity: 1;
		transform: translate(-50%, -50%);
	}

	&:hover &__image{
		transform: translateX(-3rem) scale(1);
		filter: blur(5px) brightness(80%);
	}
}
```

[![Hover Effects](https://github.com/jayli3/natours-startup/blob/master/readme_resources/gif02.gif?raw=true "Hover Effects")](https://github.com/jayli3/natours-startup/blob/master/readme_resources/gif02.gif?raw=true "Hover Effects")
----
The **background video** is defined in the html: `autoplay`, `muted` and `loop`.
The `source` taggives the browser a backup video of a different file extension to fall back to.
##### HTML
```html
<div class="bg-video">
    <video class="bg-video__content" autoplay muted loop>
        <source src='img/video.mp4' type='video/mp4'>
        <source src='img/video.webm' type='video/webm'>
        Video is not supported in your browser.
    </video>
</div>
```
Styles below, key to make it `position: absolute` with a low `z-index`.

##### SCSS
```css
.bg-video{
	position: absolute;
	top: 0;
	left: 0;
	height: 100%;
	width: 100%;
	z-index: -1;
	opacity: 0.15;
	overflow: hidden;

	&__content{
		height: 100%;
		width: 100%;
		object-fit: cover;

	}
}
```

[![Hover Effects 2](https://github.com/jayli3/natours-startup/blob/master/readme_resources/gif03.gif?raw=true "Hover Effects 2")](https://github.com/jayli3/natours-startup/blob/master/readme_resources/gif03.gif?raw=true "Hover Effects 2")


### Custom Radio Buttons
----
The radio buttons are custom styled using `::after` css pseudo element behind the label.

[![Custom Radio Buttons](https://github.com/jayli3/natours-startup/blob/master/readme_resources/gif04.gif?raw=true "Custom Radio Buttons")](https://github.com/jayli3/natours-startup/blob/master/readme_resources/gif04.gif?raw=true "Custom Radio Buttons")

##### Core Code:
```scss
.form{
	
	&__radio-group{
		width: 49%;
		display: inline-block;

		@include respond(tab-p){
			width: 100%;
			margin-bottom: 2rem;
		}
	}

	&__radio-input{
		display: none;
	}

	&__radio-label{
		font-size: $default-font-size;
		cursor: pointer;
		position: relative;
		padding-left: 4rem;
	}

	&__radio-btn{
		height: 3rem;
		width: 3rem;
		border: 5px solid $color-primary;
		border-radius: 50%;
		display: inline-block;
		position: absolute;
		left: 0;
		top: -0.45rem;

		&::after{
			content: "";
			display: block;
			border-radius: 50%;
			position: absolute;
			height: 1.3rem;
			width: 1.3rem;
			top: 50%;
			left: 50%;
			transform: translate(-50%, -50%);
			background-color: $color-primary;
			opacity: 0;
			transition: all 0.2s;
		}
	}

	&__radio-input:checked + &__radio-label &__radio-btn::after{
		opacity: 1;
	}
}
```

### Navbar Button
----
Main highlight I want to point out is the button. The button contains a couple hover effects, but the most interesting effect is when it's clicked; the 3 lines spins into a cross symbol.
This is done by creating pseudo elements using `::before` and `::after` in place of a checkbox, when checked, the animations will play.

[![Navbar Effects](https://github.com/jayli3/natours-startup/blob/master/readme_resources/gif05.gif?raw=true "Navbar Effects")](https://github.com/jayli3/natours-startup/blob/master/readme_resources/gif05.gif?raw=true "Navbar Effects")

```SCSS
.navigation{

	&__label{
		background-color: $color-grey-light-1;
		height: 7rem;
		width: 7rem;
		border-radius: 50%;
		position: fixed;
		top: 6rem;
		right: 6rem;
		z-index: 2000;
		box-shadow: 0 1rem 3rem rgba($color-black, 0.1);
		text-align: center;
		transition: all 0.1s;

		&:hover{
			cursor: pointer;
			transform: scale(1.05);
		}
	}

	&__checkbox{
		display: none;
	}text-align: center;

	//FUNCTIONALITY
	&__checkbox:checked ~ &__nav{
		opacity: 1;
		width: 100%;
	}

	&__checkbox:checked ~ &__background{
		transform: scale(100);
	}

	//ICON
	&__icon{
		position: relative;
		margin-top: 3.5rem;

		&,
		&::before,
		&::after{
			width: 3rem;
			height: 2px;
			background-color: $color-grey-dark-3;
			display: inline-block;
			transition: all 0.2s;
		}

		&::before,
		&::after{
			content: "";
			position: absolute;
			left: 0;
		}

		&::before{
			top: -0.8rem;
		}
		
		&::after{
			top: 0.8rem;
		}
	}

	&__label:hover &__icon:before {
		top: -1rem;
	}

	&__label:hover &__icon:after {
		top: 1rem;
	}

	&__checkbox:checked + &__label &__icon{
		background-color: transparent;
	}

	&__checkbox:checked + &__label &__icon:before{
		transform: rotate(135deg);
		top: 0;
	}

	&__checkbox:checked + &__label &__icon:after{
		transform: rotate(-135deg);
		top: 0;
	}
}
```


## Responsiveness
The most important aspect of front-end web dev is to design a responsive website that works seamlessly across all devices. This is achieved by utilizing a `@mixin` that accepts an argument to apply the correct `@media` queries when used. The page was built desktop-first and uses `max-width` to set the break points.
Code of the `@mixin`:
```scss
@mixin respond($breakpoint){
	@if($breakpoint == phone){
		@media only screen and (max-width: 37.5em){ @content }			//0 - 600px
	}
	@if($breakpoint == tab-p){
		@media only screen and (max-width: 56.25em){ @content }			//600 - 900px
	}
	@if($breakpoint == tab-l){
		@media only screen and (max-width: 75em){ @content }			//900 - 1200px
	}
	@if($breakpoint == big-desktop){
		@media only screen and (min-width: 112.5em){ @content }			//1800px +
	}
}
```

A general rule to follow when applying `@media` queries is to do it in this  order:
1. Base
2. Layouts
3. Components
4. The rest

#### Cards:
----
No hover feature on touch devices, so everything is in one card.
[![Responsive Design](https://github.com/jayli3/natours-startup/blob/master/readme_resources/jpg01.jpg?raw=true "Responsive Design")](https://github.com/jayli3/natours-startup/blob/master/readme_resources/jpg01.jpg?raw=true "Responsive Design")

#### Form:
----
Compact and minimal.
[![Responsive Design](https://github.com/jayli3/natours-startup/blob/master/readme_resources/jpg02.jpg?raw=true "aaa")](https://github.com/jayli3/natours-startup/blob/master/readme_resources/jpg02.jpg?raw=true "aaa")

#### Story:
----
Not skewed, but a rectangle.
[![Responsive Design](https://github.com/jayli3/natours-startup/blob/master/readme_resources/jpg03.jpg?raw=true "aaa")](https://github.com/jayli3/natours-startup/blob/master/readme_resources/jpg03.jpg?raw=true "aaa")

#### Images:
----
Clean.
[![Responsive Design](https://github.com/jayli3/natours-startup/blob/master/readme_resources/jpg04.jpg?raw=true "aaa")](https://github.com/jayli3/natours-startup/blob/master/readme_resources/jpg04.jpg?raw=true "aaa")



## NPM Dev Packages:
```json
"devDependencies": {
    "autoprefixer": "^9.5.1",
    "concat": "^1.0.3",
    "node-sass": "^4.11.0",
    "npm-run-all": "^4.1.5",
    "postcss-cli": "^6.1.2"
  }
```

## Handy NPM Scripts:
```json
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "watch-sass": "node-sass ./sass/main.scss ./css/style.css -w",
    "live-server": "live-server",
    "start": "npm-run-all --parallel watch-sass live-server",
    "compile-sass": "node-sass ./sass/main.scss ./css/style.comp.css",
    "concat-css": "concat -o ./css/style.concat.css ./css/style.comp.css ./css/icon-fonts.css",
    "prefix-css": "postcss --use autoprefixer -b 'last 10 versions' ./css/style.concat.css -o ./css/style.prefix.css",
    "compress-css": "node-sass ./css/style.prefix.css ./css/style.min.css --output-style compressed",
    "build-css": "npm-run-all compile-sass concat-css prefix-css compress-css"
  }
```
