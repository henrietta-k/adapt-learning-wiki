**First** - Make sure you have followed the documentation on [Setting up your development environment](https://github.com/adaptlearning/adapt_framework/wiki/Setting-up-your-development-environment).

### Locating the course files
Navigate to ```src/course/``` here you will find the following files/folders:

####Config.js
--to-do--

####en
The folder ```/en/``` folder contains all of the language specific data of your course. "en" is used in this instance to hold all English data and assets.

Inside this folder are a number of .json files which all follow contain [core model attributes](https://github.com/adaptlearning/adapt_framework/wiki/Core-model-attributes) as well as a directory used to store and language specific images.

Here it's key to work with the files in the following order to better understand how the framework is constructed. In the following documentation we will be looking at the example files provided.

Further reading on the [articles, blocks and components](https://community.adaptlearning.org/mod/page/view.php?id=20) can be viewed on the community site in the 'Layout and Navigation' section.

### Modifying the existing demo course
For this exercise you will need to have:
* 1x terminal window which is running ``$ grunt server`` from the root of your project folder [see previous documentation on running the server](https://github.com/adaptlearning/adapt_framework/wiki/Setting-up-your-development-environment). Once running we wont need to refer back to this terminal window.
* 1x browser tab open displaying the working build, on the main menu screen
* 1x terminal window which is pointing to the root of your project folder, this we will use shortly.

####course.json
Begin by opening the course.json file, Here we can edit the title and short description of your course.
Modify both of these values and save your code.

Now you will need to re-build your course to see your modifications. To do this you will need to open your terminal window (not the terminal running the server), and run the following command.

``$ grunt build''

After a short period of time, the build process will complete. Switch over to your browser and refresh the course. You will now see at the top of the course the name and description have been updated.


####contentObjects.json
Now lets look at adding a new item to the menu. You will see there are already a number of items in this file.

Here we have 2 options, we can create:
* a 'page' item
* or a 'menu' item

A page item will direct the user to an article, a menu will direct a user to a sub-menu screen.

Go ahead and copy the first example:

````
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
````

Scroll to the bottom of your document and locate the last instance of ````}````

Update this to include a comma, ````},````
On a new line directly after paste the code you copied earlier, so the end of your file should now look like the following:

````},

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
````



####articles.json
--to-do--

####blocks.json
--to-do--

####components.json
--to-do--

####images/
Here you can store any images used in your course.


**Next** - [Developing plugins](https://github.com/adaptlearning/adapt_framework/wiki/Developing-plugins)