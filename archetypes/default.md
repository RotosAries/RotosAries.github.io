---
title: "{{ replace .Name "-" " " | title }}"
date: {{ now.Format "2006-01-02" }}

# format for string: "xxxx-xx-xx"
# lastmod: "2022-10-01"

# set false when you want the post publish
draft: true
# one category: ["category-1"] 
# more categories: ["category-1", "category-2", ...]
categories: []
# refer to categories
tags: []
# seires
# series: []
# Top image for the post
image: ""
# Hide from home page
hideFromHomePage: false
---
