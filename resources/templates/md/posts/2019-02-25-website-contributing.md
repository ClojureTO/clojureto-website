{:title "How to Contribute to ClojureTO Website"
 :author "Hildeberto Mendonca"
 :layout :post
 :tags  ["cryogen" "website"]
 :toc true}

The wind is blowing at 85km/h outside, followed by rain and snow with low visibility. I couldn't find anything more interesting to do other than contributing to ClojureTO website. The goal today is to write a recursive article that explains how to contribute to this website by publishing itself.

### Pre-requisites

1. **Git**:

2. **GitHub Account**:

3. **Leiningen**:

4. **Cryogen**:

5. **Passion for Clojure**:

6. **Community Driven**:

### Forking The Repository

Not everybody is a good friend of a ClojureTO's co-organizer to claim push privileges. So, I need to start by forking [clojureto-website][1] to submit a pull request at the end.

    $ git clone https://github.com/ClojureTO/clojureto-website.git

### Loading the Submodule

For the moment, the folder `resources/public` is empty because the submodule was not initialized yet.

    $ cd clojureto-website
    $ git submodule init
    $ git submodule update
    $ git submodule foreach git pull origin master

Now, the folder `resources/public` is not empty anymore. It contains the most recent published content.

### Cryogen Basics

### Writing the Contribution

### Previewing the Content

As a diligent Clojure programmer, I have Leinigen installed and configured.

    $ lein ring server

### Commiting Changes

    $ cd resources/public
    $ git add .
    $ git commit -m "Published how to contribute to the website"
    $ cd ../..
    $ git add resources/templates/md/posts/2019-02-25-website-contributing.md
    $ git add resources/public
    $ git commit -m "Published how to contribute to the website"

### Creating a Pull Request

[1]: https://github.com/ClojureTO/clojureto-website
