# Shared Footer
A Vue footer component to be used across all nonprofit and umbrella sites. 

# Prerequisites
To be able to use the Vue footer component, you need to have these installed:
1. Bulma - the component uses Bulma for it's styling. To be able to get a good view on what the footer looks like, you need to have Bulma installed. https://bulma.io/
2. Any SCSS processor - The vue component's styles are made using SCSS. To customize the component, you should use SCSS so you need a processor or compiler to be able to customize the styles.
3. Vue - Of course, you need Vue to use this component.

# Example
The most updated site footer can be found on this site: http://fortheearth2.surge.sh/

# How to Use
Below is the .vue file(sfc component) of the footer and a .scss file with SCSS variables used for the footer. To be able to use the component: 
1. A gist with the Vue SFC and the .scss containing variables that the component uses. https://gist.github.com/johnveeuminga/488919d938cd6f7ca649ee53833294f4 
2. Make a new .vue file, copy and paste the `AppFooter.vue` on the gist.
3. Import the SCSS variables in the `_footer-variables.scss` to your app.
4. Download a copy of the `maximum-good.png` that is provided above. Add the `maximum-good.png` on your project.
5. You can now instansiate the footer like below:


## Example instance:
```
<shared-footer 
  :nav-options='{prependLinks: false, useDefaultNavLinks: true}'
  :nav-links='navLinks'
  :img-url='require('../assets/maximum-good.png)'
/>
```
# Options

## imgUrl
Type: String,
Default: `require('../assets/maximum-good.png')`
To render the logo, you need to define a URL for the image. If this is not defined, the 'center' section of the footer would not render 

Example:
```
<shared-footer 
  :img-url='require('../assets/logo.png)'
/>
```

## Nav Links
Type: Array
Required: No
An array that contains all our links that we want to add/place to the the footer. 
To define a link we must declare an object with the keys `link`, `label`, `openInNewTab`(optional)  attribute

Example:
```
navLinks: [
 {
    link: '#',
    label: 'Sample',
    openInNewTab: false, // Optional. Defaults to false. This defines the behavior of the link on click.
  }
]
```

And just add it to our footer

```
`
<shared-footer 
  :nav-links='navLinks'
/>
```

## Navigation Options
All options should be included in the :nav-options attribute. 
### useDefaultNavLinks
Type: Boolean
Required: No
Default: true
The footer has default navigation links in the component itself. When set to true, we use the default links and prepend/append all the links that we define ourselves.
### prependLinks
Type: Boolean
Required: No
Default: true
If set to true and use *defaultNavLinks* is set to `true`, we add the custom links before the default links. If set to false, we append it to the custom links.

Example nav options object
```
{
  prependLinks: false, 
  useDefaultNavLinks: true,
}
```

## learnMoreLink
Type: String 
Default: #
The `Learn More` button link.

Example: 
```
<shared-footer 
  :learn-more-link='#'
/>
```


# Slots
## footer__motto
The motto part of the footer. 

Example:
```
<shared-footer>
  <slot name='footer__motto'>
    Sample motto here
    <router-link to='#' class='button is-primary'>Button</router-link>
  </slot>
</shared-footer>
```

## footer__copyright
The copyright or the bottom part of the footer

Example:
```
<shared-footer>
  <slot name='footer__copyright'>
    <p> <small>Copyright (c) 2006-2019 DailySource.  All rights reserved.  Terms of Service.</small> </p>
  </slot>
</shared-footer>
```
