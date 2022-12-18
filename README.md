---
title: Documentation
---

Editing the WAND site
=====================
- - -

**I need to be:** 
- [Adding a person](#adding-a-person)
  - [Providing them a profile image](#providing-a-profile-image)
  - [Addding a custom tab name](#addding-a-custom-tab-name)
  - [Adding a new category of people](#adding-a-new-category-of-people)
- [Adding a project](#adding-a-project)
  - [With an internal link](#with-an-internal-link)
  - [With an external link](#with-an-external-link)
- [Adding a research topic](#adding-a-research-topic-listed-under-research-tab)
- [Adding a main page](#adding-a-main-page-eg-home)
  - [With a dropdown menu](#with-a-dropdown-menu)
- [Using the different layouts](#using-the-different-layouts)
- [Adding a new collection](#adding-a-new-collection)
- [Testing the site locally](#testing-the-site-locally)

Link to markdown parser documentation \[[Kramdown](https://kramdown.gettalong.org/quickref.html)\]

Link to jekyll templating language \[[liquid](https://shopify.github.io/liquid/basics/introduction/)\]

<!--split-->
## Adding a person
Create a new markdown file in `collect/_people/` . Add the following to the top of it, (including dashes) and fill out required values.

```yml
---
layout: person
name: [full name of person]
role: [category to be listed under, as per how it appears in _data/pCategory.yml]
projects: (optional) [project 1's set name], [project 2's set name]
link: (optional) [external link instead of internal profile page]
---
```
You can then follow this with any amount of markdown you'd like to describe the person.

Note the only required fields for a person are layout, name and role. Adding a link variable will replace the internal page link with an external one.

#### Providing a profile image
To set the image of a person, drop the image into `assets/images/` . Make sure to rename the image to the persons name value in lowercase, and spaces set to underscores.

eg. name: Jane Doe
Will request an image called jane_doe.[image extention]

#### Addding a custom tab name
Add the tab variable to the front matter with any value, then the title varaible with the tab name you want.

eg.

```yml
---
layout: person
name: [full name of person]
tab: yes
title: [sets the displayed tab name]
---
```

#### Adding a new category of people
Simply append your category to `_data/pCategory.yml` in the format

```yml
- name: [category's name]
```
<!--split-->
## Adding a project
#### With an internal link
Create a new markdown file in `collect/_projects/`  . Add the following to the top of it (including dashes) and fill out required values.

```yml
---
layout: project
name: [the name of your project]
topic: [name of topic to attach the project under]
description: [short project description]
title: [changes the displayed tab name]
---
```
You can then follow this with any amount of markdown you'd like to describe the project.


#### With an external link
Open the file `_data/externalProject.yml` and attach your projects details appropriately in the format.

```yml
- topic: [name of topic to attach the project under]
  name: [name of project being attached]
  description: [short project description]
  link: [the link address]
```

<!--split-->
## Adding a research topic (Listed under research tab)
Create a new markdown file in `collect/_research/`. Add the following to the top of it (including dashes) and fill out required values.

```yml
---
layout: topic
name: [put your topic name here]
title: [changes the displayed tab name]
---
```
You can then follow this with any amount of markdown you'd like to describe the topic.

<!--split-->
## Adding a main page (eg, Home)
To add a main page, simply add a markdown file to the site's main directory. To add a link to it in the nav bar, add its address to the `data/navigation.yml` file.

```yml
- name: [link name]
  link: [file name].html
```

#### With a dropdown menu
If the nav items name already has an existing collection with the same name, simply add the drop variable.
For example:

```yml
- name: People
  link: people.html
  drop: yes
```
As long as there is a collection existing with the name value lowercase (eg. people). A drop down menu will be generated with links to the items in the collection. Note that dropdown menus are not displayed on mobile.

<!--split-->
## Using the different layouts

**default** - Will simply output the content unformatted and center aligned. This layout is designed as a gateway for other layouts, therefore this layout is not reccommended for using with content directly.

**maps** - Outputs the content in a div 40% of the page width, leaving space on the right for a google maps embed.

**people** - Any content will be output normally. Then a list of the people in the peoples collection will be output and formatted in a tidy manner.

**person** - Name and role values will be displayed next to an image that's src is derived from the image name. Any input content will then be attached below this, followed by a table of projects that have been listed in the person's front matter.

**plain** - Outputs the content as plain text aligned to the left.

**project** - Output content as plain text, then attach a link back to the topic the project is related to.

**research** - List all the items in the research collection each with a link to their respective topics. Every second research item has an off-white background colour.

**sections** - Split the content based on input `<!--split-->` tags. Every second section has it's background colour set to off white.

**topic** - Display input content and then list all projects associated with the topic in a table.

**twitter** - Similar to maps, output the content to fill 60% of the display width and then attach a twitter scroll to the right side of the content.

<!--split-->

## Adding a new collection
Modify `_config.yml` by adding the collections name under the `collections:` variable. Adding the `output:` variable allows you to output individual pages for each collection entry if you set it to true.

eg.
```yml
collections:
     people:
        output: true
     research:
        output: true
```

Note sometimes using tab characters can break this, use spaces instead.

Then create a new directory in `collect/` for your collection with the same name as your collection, with an underscore in front of it.

eg. `collect/_people` and `collect/_research`

<!--split-->

## Testing the site locally

The website can be run locally from docker:

```
$ docker run --rm \
  -e "JEKYLL_ENV=docker" \
  --volume="$PWD:/srv/jekyll:Z" \
  --publish [::1]:4000:4000 \
  jekyll/jekyll \
  jekyll serve \
    --config _config.yml,_config.docker.yml
```

Your site should now be hosted at http://localhost:4000/

[Back to top](#editing-the-wand-site)
