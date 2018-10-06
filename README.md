ResponsiFlex
============================

 ResponsiFlex is a CSS framework that takes advantage of modern browsers and the Flexbox model to create truly responsive layouts, without hacks. No floats, no `inline-block`s - just intuitive, responsive, fluid layouts.

The commented & tabbed ResponsiFlex stylesheet is just 10.2kb, or 6.54kb minified. It is released under the GNU General Public License. 

### Prerequisites

ResponsiFlex has no dependencies - just plug it into your page and have at it.

### How it works

**ResponsiFlex** is based on the standard 12-column grid, with some extra flavour thrown in. Each `boxcontainer` is 100% of its parent's width, and each of its child `box` elements can be set to a desired width with a simple named class: `.box.six` makes the box half the width of its `.boxcontainer` as it takes up six columns; `.box.one` is 1/12th the width, because it's one column. There are also special `.box.tenths` class for 10%-width &amp; `.box.fifths` for 20% (as they don't fit neatly into a 12-column grid, but you may find you want them more often than you realise).

The boxes have a `1.250rem` gutter (or 20px, assuming a root 16px); alternatively you can use the `.nogutter` class to make them butt up to each other perfectly. If you want a different gutter value, just use search &amp; replace to change `1.250rem` to whatever you want. Could you convert it to SASS or LESS? Sure! Am I gonna? Nope!

## Usage

Take a look at [ResponsiFlex's GitHub page](https://indextwo.github.io/responsiflex/) for a full set of demos and code examples. 

Basic usage goes like this:

```html
<!-- With standard gutter: -->
<div class="boxcontainer">
	<div class="box six">
		I'm one half.
	</div>
	
	<div class="box six">
		I'm the other half.
	</div>
</div>

<!-- With no gutter: -->
<div class="boxcontainer nogutter">
	<div class="box six">
		I'm one half.
	</div>
	
	<div class="box six">
		I'm the other half.
	</div>
</div>

<!-- Centred: -->
<div class="boxcontainer aligncenter">
	<div class="box four">
		I'm a third of the size and centred.
	</div>
</div>
```

## Classes

### The Container

 * `.boxcontainer`: The Flexbox column wrapper. All columns should go within here.
 * `.boxcontainer.columns`: By default, boxcontainer will order its children left-to-right. Adding .columns will stack it's children top-to-bottom instead.
 * `.boxcontainer.align[center/right]`: By default child boxes will be left-aligned. Adding `.align[center/right]` will change that. Note the difference between `.aligncenter` and `.alignmiddle` (below).
 * `.boxcontainer.justify`: This will attempt to evenly distribute your child boxes across their container. Note that this only takes effect for any rows where there is space between the boxes to justify them.
 * `.boxcontainer.align[top/middle/bottom]`: By default child boxes will be top-aligned. Adding `.align[top/middle/bottom]` will change that. Note the difference between `.alignmiddle` and `.aligncenter` (above).
 * `.boxcontainer.stretchheight`: This will attempt to force all of its children to be the same height, regardless if whether any are shorter than the others. Works best for single rows of items.
 * `.flex-nowrap`: By default, the boxcontainer is set to wrap its child items. Using this in combination with `.flex-noshrink` (see **Child Boxes** section) can force flexbox items to break out of their containers. Handy for things like slideshows & carousels.
 * `.boxcontainer.nogutter`: By default there is a set gutter between each box (and the boxcontainer has a negative margin to account for that). `.nogutter` Removes any margins so all direct child items butt up to each other.
 * `.boxcontainer.mobileretainwidths`: ResponsiFlex has a media query to set all child boxes to 100% width when the viewport is less than `48em` (assumed 768px) wide. Using `.mobileretainwidths` will mean that child boxes will retain their responsive percentage widths even on narrow viewports (Note that you can change this media query condition yourself within the CSS if you want to change it).
 * `.mobile-boxcontainer`: This is for a boxcontainer that will ONLY do its thing when the viewport is less than 48em wide (see above). Sometimes you might want your display elements to behave as normal in desktop view, but get some funky alignment going on in mobile - that's what this is for.

### The Child Boxes

 * `.box`: A child of .boxcontainer. A `.box` can be a set width (`.one, .two, .three` etc. up to `.twelve`) or given no defined width, in which case it will adjust according to its content.
 * `.box.[tenths/fifths]`: A twelve-grid layout is neat and pretty much standard, but every so often you might want something that's exactly a fifth of the width, or even a tenth; In that case, `.box.fifths` or `.box.tenths` will give you perfect 20% or 10%-width boxes.
 * `.flex-grow`: If you don't know exactly how much space there's going to be left in your container, but you want to take up whatever's left, then this is the class for you.
 * `.flex-stretch`: Pretty much as above; the main difference is that `.flex-glow` specifically sets the `flex-grow` CSS property, `.flex-stretch` sets the flex shorthand `flex: 1`. Read more about it [here](https://css-tricks.com/snippets/css/a-guide-to-flexbox/).
 * `.flex-noshrink`: Flexbox will try to be as accomodating as possible with your boxes. Using this will force boxes to never shrink below their defined width. Handy when used in conjunction with `.flex-nowrap` (see above in **The Container**).
 * `.flex-self-[top/middle/bottom]`: You can align any child item to the top, middle or bottom of its container independent of the alignment of the other items or the parent.
 * `.box.mobile-width.mobile-[*]`: You can define how a box spans its container specifically on narrow viewports using the `.mobile-width` class. For example, if you have four `.box.three` elements in a row, but instead of them all expanding to 100% on a narrow viewport, you want them to switch to 50% width (so you get a 2x2 grid), you can define them as `<div class="box three mobile-width mobile-box-six">`.

## Notes &amp; Assumptions

 As with all things in life, there are some caveats and things to note with ResponsiFlex:

 *  The gutters are hard-coded in the CSS at `1.250rem` (or 20px, assuming a root EM of 16px). If you want a different gutter, just search &amp; replace `1.250rem` in the CSS - it won't affect anything else. Could you convert it to SASS or LESS? Sure! Am I gonna? Nope!
 *  To account for the gutter spacing, the default `.boxcontainer` class has a negative margin. This shouldn't have any impact on any of your layout, and the negative margin is not in place when a boxcontainer is justified or has no gutter.
 *  To make sure everything works as expected (with the above point especially), boxcontainers and their children all have `box-sizing: border-box;` set.
 *  The 'mobile' media queries kick in at a width of `48em` (768px assuming a room EM of 16px). If you want to change this, you can go right ahead and modify the CSS to suit your needs.
 *  The classes have been written to try and keep their CSS specificity as low as possible so that they can be easily overwritten, but obviously the more complex the rule (e.g. `.mobile-boxcontainer > .mobile-box.nine, .boxcontainer > .box.mobile-width.mobile-nine`), the more specific you might need to be to override it.

You can view working demos on [ResponsiFlex's GitHub page](https://indextwo.github.io/responsiflex/)
 
 ## Authors

* [Lawrie Malen](https://github.com/indextwo) at [Very New Media&trade;](http://www.verynewmedia.com)

## License

This project is licensed under the GNU General Public License - see the [LICENSE](LICENSE) file for details
