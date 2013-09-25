# Folder Structure

---

Now that we will be working on large, long running projects with multiple
developers, it is essential that we organize our project in the same way
in order to:

* Facilitate efficient collaboration between developers
* Include new team members quickly

## Table of Contents

* [General Project Organization]()
* [Root Folder Files](#root-folder-files)
* [Assets Folder](#asset-folder)
	* [Fonts](#fonts)
	* [Images](#images)
	* [Scripts](#scripts)
	* [Styles](#styles)


---


## [Root Folder](#root-folder)
The structure of this folder very much depends on the programming language being used.
See [Programming Languages](https://github.com/thejamesdempsey/Code-Style-Guidelines/blob/master/Languages/) for more details.


## [Assets Folder](#assets-folder)
Regardless of the application being built, it is important to define a similar structure for the presentation
layer. All such folder and files will exist in an `asset` folder at the `root` level of the project.


## [Fonts](#fonts)
In order to be inline with out branding guidelines, we need to have a font system that allows us to use branding
fonts without violating copyright issues. [Typekit](https://typekit.com) has all our official fonts.

Is there another way to host and serve our fonts without making them downloadable by the end user -- font embedding?
Think [Typeface.js](http://typeface.neocracy.org) or [Cufón](https://github.com/sorccu/cufon/wiki/about).


## [Images](#images)
Any images used in the project should go into this folder -- all web consumed images served from this root and not
any of the sub-folders. There are several sub-folders of importance.

The `originals` folder holds image source files like Photoshop and InDesign.

The `www-images` is optional,
it holds high fidelity web formatted images like PNGs, JPEGs and so forth.


## [Scripts](#scripts)
Javascript files and frameworks will be stored in this folder.


## [Styles](#styles)
The main stylesheet in any project should be `screen.css`. Other file(s) include `print.css`.
[Inuit](https://github.com/csswizardry/inuit.css) is a object oriented css framework that give you design
patterns, not design decisions.

`project-name folder` holds project specific css file(s). This file should be name `project-name.scss`. This includes
customizations that override [Cru Inuit](https://github.com/elikem/cru-inuit.css) as well.

Inuit is stored in the inuit folder. View their README file to learn more on how to use it.

`screen.scss` brings all the css files together. It imports inuit, project specific css files.