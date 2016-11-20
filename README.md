# Blog en Jekyll

* synchroniser votre site avec git sur *GitHub*
* générer le site à la volée et le servir avec *GitHub Pages*
* rédiger directement ses articles en ligne grâce à [*Prose*](prose.io)
* tester la compilation, le HTML et les liens avec [*Travis*](https://travis-ci.org/)
* incorporer des commentaires en JS avec [*Disqus*](https://disqus.com/)

## Doc Jekyll (Github)
* [Doc Jekyll in Github](https://github.com/jekyll/jekyll/blob/master/docs/_docs/continuous-integration.md)

## Jekyll website
* [Jekyllrb](http://jekyllrb.com)

## Help about Jekyll (stackoverflow-like)
* [Talk Jekyllrb](https://talk.jekyllrb.com)

## Liquid
* [Liquid basics](https://help.shopify.com/themes/liquid/basics)
* [Liquid for Designers](https://github.com/Shopify/liquid/wiki/Liquid-for-Designers)
* [Shopify Liquid Github](https://github.com/Shopify/liquid/wiki)

## Tuto about Jekyll
* [Make a Static Website with Jekyll](https://www.taniarascia.com/make-a-static-website-with-jekyll/)
* [Site statique avec Jekyll](https://www.sylvaindurand.fr/site-statique-avec-jekyll/)
* [Servir son site avec cloudfront](https://www.sylvaindurand.fr/servir-son-site-avec-cloudfront/)
* [Utiliser Github pour servir Jekyll](https://www.sylvaindurand.fr/utiliser-github-pour-servir-jekyll/)
* [Guide de démarrage : créer un blog statique avec jekyll](http://www.toam.fr/20-05-2013-guide-demarrage-jekyll/)
* [Getting Started with Jekyll](https://scotch.io/tutorials/getting-started-with-jekyll-plus-a-free-bootstrap-3-starter-theme)
* [Créer un blog statique Jekyll](https://www.grafikart.fr/tutoriels/html-css/jekyll-505)

## Color Hexa
* [color-hex](http://www.color-hex.com/color/008b8b)

----


# Space Jekyll

LA COULEUR BACKGROUND assets/css/main.css LIGNE CONTENANT .page-header{background:#5d4d7a;height:100%;}

A simple and elegant Jekyll theme based on Spacemacs. The theme works well on mobile devices as well.

See a live demo [here](https://victorvoid.github.io/space-jekyll-template/).

![](https://github.com/victorvoid/space-jekyll-template/blob/master/screenshot.png?raw=true)

# Site/User Settings

customize your site in ``_config.yml``

```ruby

# Site settings
description: A blog about lorem ipsum
baseurl: "" # the subpath
url: "" # the base hostname &/|| protocol for your site 

# User settings
username: Lorem Ipsum
user_description: Lorem Developer
user_title: Lorem Ipsum
email: lorem@ipsum.com
twitter_username: loremipsum
github_username:  loremipsum
gplus_username:  loremipsum
disqus_username: loremipsum

```

## How to create a post ? 

_posts create a file .md with structure:

```md
---
layout: post
title: "Lorem ipsum speak.."
date: 2016-09-13 01:00:00
image: '/assets/img/post-image.png'
description: 'about tech'
tags:
- lorem
- tech 
categories:
- Lorem ipsum
twitter_text: 'How to speak with Lorem'
---
```

## License
The MIT License (MIT)

Copyright (c) 2016 Victor Igor

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
