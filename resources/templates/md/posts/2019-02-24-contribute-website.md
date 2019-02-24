{:title "How To Contribute to ClojureTO Website"
 :author "Hildeberto Mendonca"
 :layout :post
 :tags  ["cryogen" "website" "blog"]
 :toc false}

You will need [Leiningen][1] 2.5.0 or above installed.

The web server can be started from the `my-blog` directory using the `lein-ring` plugin:

```
lein ring server
```

The server will watch for changes in the `resources/templates` folder and recompile the content automatically.

Cryogen uses [Selmer][2] templating engine for layouts. Please refer to its documentation to see the supported tags and filters for the layouts.

The layouts are contained in the `resources/templates/themes/{theme}/html` folder of the project. By default, the `base.html` layout is used to provide the general layout for the site. This is where you would add static resources such as CSS and JavaScript assets as well as define headers and footers for your site.

Each page layout should have a name that matches the `:layout` key in the page metadata and end with `.html`. Page layouts extend the base layout and should only contain the content relevant to the page inside the `content` block.
For example, the `tag` layout is located in `tag.html` and looks as follows:

```xml
{% extends "templates/html/layouts/base.html" %}
{% block content %}
<div id="posts-by-tag">
    <h2>Posts tagged {{name}}</h2>
    <ul>
    {% for post in posts %}
        <li>
            <a href="{{post.uri}}">{{post.title}}</a>
        </li>
    {% endfor %}
    </ul>
</div>
{% endblock %}
```

Cryogen uses [Highlight.js](https://highlightjs.org/) for code syntax highlighting. You can add more languages by replacing `templates/js/highlight.pack.js` with a customized package from [here](https://highlightjs.org/download/).

The `initHighlightingOnLoad` function is called in `{theme}/html/base.html`.

```xml
<script>hljs.initHighlightingOnLoad();</script>
```

The generated static content will be found under the `resources/public` folder. Simply copy the content to a static
folder for a server such as Nginx or Apache and your site is now ready for service.

[1]: https://github.com/technomancy/leiningen
[2]: https://github.com/yogthos/Selmer
