# Source for Falster lab website

The website is developed using the [Hugo](https://hugodocs.info) static site generator and deployed on [netifly](netlify.com).

The site layout was adapted from [Carl Boettiger's lab notebook](https://github.com/cboettig/labnotebook), the theme of which he's also made available as [hugo-material theme](https://github.com/cboettig/hugo-material). As noted there, this theme is an adaptation for Hugo of the Bootstrap-based [Material Design](https://github.com/creativetimofficial/material-kit) by [Creativetim](https://www.creative-tim.com), which itself builds off [Bootstrap v4](https://getbootstrap.com) and [Google's Material Design kit](https://material.io). Thanks to Carl, Creativetim, Bootstrap and Google for contributing the open source materials that made this site possible.

## Building site

Following are my notes on site upkeep.

Download & install Hugo from https://github.com/gohugoio/hugo/releases. NB, you don't need `Go` to run `Hugo.`

To build site run

```
hugo
```

To view, run following, which will open a viewer on localhost:1313/

```
hugo server -D
```

## Short codes

Hugo uses short codes to easily embed content. See https://gohugo.io/content-management/shortcodes/

```
{{< tweet 306854385076543488 >}}
```

```
{{< figure src="https://danielfalster.com/images/2016.06.27-useR/useR-600x300.png" height="100" width="100" >}}
```

I wrote the following additional shortcodes for use in the site:


```
{{< iframe "https:...." "960" "540" >}}
```

```
{{< nicequote "quote" "author" "source" >}}
```
