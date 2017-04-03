**First** - Make sure you have followed the documentation on [[setting up your development environment]].

### Locating the course files
Navigate to ```src/course/``` here you will find the following files/folders:

#### config.json
The [config file](Configure-your-project-with-config.json) is used to store any settings for your course. For example which folder to use as the default language or any LMS tracking settings.

#### en
The folder ```/en/``` folder contains all of the language specific data of your course. "en" is used in this instance to hold all English data and assets.

Inside this folder are a number of .json files which all follow contain [[core model attributes]] as well as a directory used to store and language specific images.

Here it's key to work with the files in the following order to better understand how the framework is constructed. In the following documentation we will be looking at the example files provided.

Further reading on the [articles, blocks and components](https://community.adaptlearning.org/mod/page/view.php?id=20) can be viewed on the community site in the 'Layout and Navigation' section.

### Modifying the existing demo course
For this exercise you will need to have:
* 1x terminal window which is running ``$ grunt server`` from the root of your project folder [[see previous documentation on running the server|Setting-up-your-development-environment]]. Once running we wont need to refer back to this terminal window.
* 1x browser tab open displaying the working build, on the main menu screen
* 1x terminal window which is pointing to the root of your project folder, this we will use shortly.

#### course.json
Begin by opening the [course.json](Content-starts-with-course.json) file. Here we can edit the title and short description of your course.
Modify both of these values and save your code.

Now you will need to re-build your course to see your modifications. To do this you will need to open your terminal window (not the terminal running the server), and run the following command.

``$ grunt build``

After a short period of time, the build process will complete. Switch over to your browser and refresh the course. You will now see at the top of the course the name and description have been updated.


#### contentObjects.json
Now lets look at adding a new item to the menu. You will see there are already a number of items in this file.

Here we have 2 options, we can create:
* a 'page' item
* or a 'menu' item

A page item will direct the user to an article, a menu will direct a user to a sub-menu screen.

Go ahead and copy the first example:

```js
...
    {
        "_id":"co-05",
        "_parentId":"course",
        "_type":"page",
        "_classes":"",
        "title":"Demo page",
        "body":"This page should contain a working Adapt page will all core bundled components and plugins working.",
        "graphic": {
            "alt": "alt text",
            "src": "course/en/images/origami-menu-one.jpg"
        },
        "linkText":"View"
    }
...
```

Scroll to the bottom of your document and locate the last instance of ````}````
Update this to include a comma, ````},````

_When inserting any new json objects, always make sure you include this comma between any objects, otherwise your course will fail to build._

On a new line directly after paste the code you copied earlier, so the end of your file should now look like the following:

```js
...
    },
    {
        "_id":"co-05",
        "_parentId":"course",
        "_type":"page",
        "_classes":"",
        "title":"Demo page",
        "body":"This page should contain a working Adapt page will all core bundled components and plugins working.",
        "graphic": {
            "alt": "alt text",
            "src": "course/en/images/origami-menu-one.jpg"
        },
        "linkText":"View"
    }
]
```

* Change the "_id" to an unused reference, for this example we want the item to be displayed last in the menu, so modify it to ```"_id":"co-25",```
* Change the title and the body, just as you did in the previous example.
* Save your code

Adapt content requires a structure of articles, blocks, and components. The number of each will vary from course to course, but the hierarchical relationship is fundamental to each page.

#### articles.json
Now that you have created your item in the menu you will want to create an 'Article'. Open the articles.json file, just as we did in the last example, copy the first json object and paste this at the bottom of your document.

Again we need to modify the '_id' attribute of this article, so change the id to 'a-50'.

The next important attribute to edit is the '_parentId' item, this is what links the article to the course object. The id here should be the '_id' which we assigned to our course object earlier. So update the value to 'co-25' to match.

You should now have something which looks like this..

```js
...
    },
    {
        "_id":"a-50",
        "_parentId":"co-25",
        "_type":"article",
        "_classes":"",
        "title":"Article first title",
        "body":"Body text for article"
    }
]
```

Modify the title and body and save your code.

#### blocks.json
Now that we've setup your first article, we can now include a new block element, this will be used later to add components.

Open the blocks.json file, again copy the first json object and paste this at the bottom of your document.

Again we need to modify the '_id' attribute of this block, so change the id to 'b-150'.

The next important attribute to edit is the '_parentId' item, this is what links the block to the article. The id here should be the '_id' which we assigned to our article earlier. So update the value to 'a-50' to match.

You should have something that looks like this:

```js
...
    },
    {
        "_id":"b-150",
        "_parentId":"a-50",
        "_type":"block",
        "_classes":"",
        "title":"Title of first block",
        "body":"Body text for block"
    }
]
```

Modify the title and body and save your code.

#### components.json
Its time to add a component to your course. Again copy the first json object and paste this at the bottom of your document.

Again we need to modify the '_id' attribute of this component, so change the id to 'c-200'.

The next important attribute to edit is the '_parentId' item, this is what links the component to the block. The id here should be the '_id' which we assigned to our block earlier. So update the value to 'b-150' to match.

You should have something that looks like this:

```js
...
    },
    {
        "_id":"c-200",
        "_parentId":"b-150",
        "_type":"component",
        "_component":"text",
        "_classes":"",
        "_layout":"left",
        "title":"Title of our very first component",
        "body":"Whoo - if we get this rendering we've made the big time"
    }
```

Modify the title and body and save your code. Now you will need to re-build your course and refresh your browser. From the main menu you will be able to click your new menu item. You should now see your article, block and component displaying on screen :)


#### images/
Here you can store any images used in your course. This folder will be exported in the build process and can be referenced where required using the following path value ```course/en/images/origami-menu-two.jpg```. Examples of its use can be viewed in the components.json file.

**Important:** if your course targets IE8, it is recommended to limit the number of components on a single page to 20. This is recommended to help avoid the popup warning "A script on this page is causing Internet Explorer to run slowly". See https://support.microsoft.com/en-gb/kb/175500 for more information.

**Next** - [[Styling your course]]