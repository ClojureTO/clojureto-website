{:title "How to Contribute to ClojureTO Website"
 :author "Hildeberto Mendonca"
 :layout :post
 :tags ["Cryogen" "Website" "Github" "Markdown" "Git"]
 :toc true}

The wind is blowing at 85km/h outside, followed by rain and snow with low visibility. I couldn't find anything more interesting to do other than contributing to ClojureTO website. The goal today is to write a recursive article that explains how to contribute to this website by publishing itself.

### Pre-requisites

That's what I need to be able to contribute:

1. **Git**: as a technical person, I have the habit of versioning the work I do. Git is the tool I use for that. This is also the tool needed to manage and publish the website.

2. **GitHub**: ClojureTO uses GitHub Pages as a hosting service. In short, when we push content to a repository it gets published on the website. To synchronize content with GitHub I need a GitHub account and Git.

3. **Leiningen**: this is the portal to enter in the Clojure World. A Swiss knife to manage Clojure projects. I use it to tests the changes I make in the website. I was also used it to create the website in the first place.

4. **Cryogen**: this tool, in combination with Leiningen, built this entire website. We explained how we did it in a [previews article][2]. Now, I need it to produce the content, define the layout, the style, and the navigation.

5. **Passion for Clojure**: to write such long and rich content, a good deal of time and knowledge is required. My passion for Clojure motivates me to do it.

6. **Community Driven**: a genuine intention to share knowledge and help others is also required.

### Forking The Repository

Not everybody is a good friend of a ClojureTO's co-organizer to claim push privileges. So, I need to start by forking [clojureto-website][1]. I click on the **Fork** button and get a new repository in my account. My contributions will remain there until it's time for a pull request.

![Forking clojureto-website repository](/img/fork-clojureto-website.png)

I clone the repository locally so I can start contributing:

    $ git clone https://github.com/htmfilho/clojureto-website.git

### Cryogen Basics

Understanding Cryogen is discovering ways of contributing. Its [website][3] covers all details. In summary, those with design skills could jump into `resources/templates/themes` and redefine how the content is presented, improve navigation, readability, harmonize colors, shapes. I personally have no talent there, so I care more about content, which is located at `resources/templates/md`. The one place that should not be touched at all is the folder `resources/public`. Those files are replaced whenever the files in the previously mentioned folders are modified and saved.

### Writing the Contribution

I wish I could write the content in Clojure, but that's not practical. So, I stick to [Markdown][4], a format supported by Cryogen. Markdown eliminates the pain of writing content in HTML by offering a minimalist markup language for web authoring. All the content in Markdown, including this article, is located at `resources/templates/md`. I can write **pages**, which are more institutional, and **posts**, which represent facts, perspectives, experiences, and discoveries.

Apart from Markdown, there is a caveat. At the top of a page or post, there is a Clojure-like map where we define values expected by the theme. For a page, there is something like this:

    {:title "About"
     :layout :page
     :page-index 0
     :navbar? true}

I would emphasize `:page-index`, which defines the order the page appears in the navigation, and `:navbar?` to include the page in the top menu. For this post in particular, I used this:

    {:title "How to Contribute to ClojureTO Website"
     :author "Hildeberto Mendonca"
     :layout :post
     :tags  ["Cryogen" "Website" "Github" "Markdown"]
     :toc true}

A special attention to `:tags`, which helps to organize the content, and `:toc` to show a table of content to help navigating in a long post.

### Previewing the Content

To preview the content exactly as it will appear on the website, I go to the root of the repository and run the following command:

    $ lein ring server

After a few seconds, the default browser opens and shows the website. Since this article is the most recent one, it appears in the front page, as shown in the image below:

![Forking clojureto-website repository](/img/preview-content-website.png)

Every time I save the file that I'm working on, the website is regenerated and the last changes are ready to see.

### Committing and Pushing Changes

At this point in time, the article is finished and ready to submit. I commit all my changes, including text and images, and push to my own fork:

    $ git add resources/templates/md/posts/2019-03-05-website-contributing.md
    $ git add resources/templates/img/fork-clojureto-website.png
    $ git add resources/templates/img/preview-content-website.png
    $ git commit -m "Article 'How to Contribute to ClojureTO Website'"
    $ git push origin master

Notice that I add each artifact one by one, instead of running a practical command like `git add .`. The reason is because I don't want to accidentally mess up with the submodule located at `resources/public`. More details latter on.

### Creating a Pull Request

The pull request happens on GitHub. Now that the changes are pushed, my fork is different from the original, and this difference is exactly the content of the pull request I'm creating. I click on the button "New pull request" and it shows me the differences.

![Pull request from my fork to clojureto-website repository](/img/pullrequest-content-website.png)

When I click the green button "Create pull request" I'm actually submitting my changes for review by one of the website's editors. My work is probably not done yet because they may ask me to fix some typos, rephrase some sentences and clarify others. I do extra changes and I just keep pushing to my master branch to have my pull request updated.

When the pull request is accepted and the merge is done, it doesn't mean the content is immediately published on the website. The editor has some work to do as well.

### Updating the Website with the Contribution

The editor is the person responsible for accepting the pull request and publishing the contributions in the sequence. This person has special push privileges to the repositories [clojureto-website][1] and [clojureto-github.io][5]. The pull request is merged and now the editor needs to generate the static content. In the event she never did it before, she starts by cloning the clojureto-website repository:

    $ git clone https://github.com/ClojureTO/clojureto-website.git
    $ cd clojureto-website

The editor has all recent changes locally and needs to setup the submodule `clojureto.github.io` in the folder `resources/public`:

    $ git submodule init
    $ git submodule update
    $ git submodule foreach git pull origin master

Now, the folder `resources/public` contains the most recent published content, but it needs to be updated with the most recent one. To do that, the editor needs to launch Cryogen once, so it can regenerate the static website in the folder `resource/public`:

    $ lein ring server

To stop the server she presses `Ctrl+C` and then she notices the content of the folder `resource/public` has changed:

    $ cd resources/public
    $ git status

She needs to move to the master branch, commit all the changes and push to the repository `clojureto.github.io`:

    $ git checkout master
    $ git add .
    $ git commit -m "Published article 'How to Contribute to ClojureTO Website'"
    $ git push origin master

When the push is completed the latest contributions to the website are published! But the work is not done. There is still a final step, which is updating the submodule of the the repository `clojureto-website`:

    $ cd ../..
    $ git add resources/public
    $ git commit -m "Updated submodule reference."
    $ git push origin master

That's enough with this website and Git. Starting next post, everything will be about the Community and Clojure!

[1]: https://github.com/ClojureTO/clojureto-website
[2]: https://clojureto.github.io/posts-output/2019-02-23-website-behind
[3]: http://cryogenweb.org
[4]: https://daringfireball.net/projects/markdown/
[5]: https://github.com/ClojureTO/clojureto.github.io
