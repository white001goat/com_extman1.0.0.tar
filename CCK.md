# CCK

## Introduction

Moyo wrote its own multilingual Content Construction Kit. For some background information, please read [this blog post]
(http://moyoweb.nl/en/blog/2014-01-17/content-management-on-steroids.html). From this post:

> In our opinion, the distinction between articles and other types of content (say: events) is artificial.
> After all, they are all content items that have to be presented to the user in different ways. This idea prompted us
> to abolish all different content types and use a generic content item instead. Each content type is to be filled in
> by a content manager, thus generating custom content editing screens for each content type.

Currently, our CCK is in its third or so iteration. The main package is `com_cck`. This is where all the content types
are defined and this is where all our components come together.

The CCK was developed by [Moyo Web Architects](http://moyoweb.nl).

## Requirements

   * Joomla 2.5 or 3.X .
   * Koowa 0.9 or 1.0 (as yet, Koowa 2 is not supported)
   * PHP 5.3.3 or better
   * Moyo Components
       * com_moyo
       * com_taxonomy
       * com_articles

## Installation

Installation is done through composer. In your `composer.json` file, you should add the following lines to the repositories
section:

```json
{
    "name": "moyo/cck",
    "type": "vcs",
    "url": "https://github.com/cta-int/cck.git"
}
```

The require section should contain the following lines:

```json
    "moyo/cck": "1.0.*",
```

Afterward, just run `composer update` from the root of your Joomla project.

### jsymlinker

Another option, currently only available for Moyo developers, is by using the jsymlink script from the [Moyo Git
Tools](https://github.com/derjoachim/moyo-git-tools).

## Usage

### Fieldsets

Fieldsets simply contain names and elements. The edit screen can be accessed by Choosing `Components >> CCK >> Fieldsets`
in the menu.

(@todo: wait for new GUI for further explanation)

### Elements

Fieldsets are populated by elements. Although many common elements have been predefined, the content manager can always
define new ones, e.g. when a new component is added to the CMS.

The following fields are defined for each element:

* **Title** Defines the title of the element
* **Slug** Unique identifier. Automatically generated, unless manually filled in. Use with care
* **Published** Defines whether an element is actually usable in fieldsets.
* **Type** Defines the content type of the element. More in this in the next section
* **Fieldsets** Enables the content manager to define the fieldsets in which to add the element.
* **Placeholder** Placeholder text as per HTML standard.
* **Default** Default value
* **Required** Defines whether an element is required as per HTML standard.

Please note that elements are sharable among fieldsets.

#### Types

The following content types can be assigned to an element:

* **Article** A CCK article as per Moyo's com_articles.
* **Booleanlist** Generates a true/false radio item.
* **Calendar** Generates a calendar.
* **Checklist** Generates a list of checkboxes based on the values given.
* **Colorpicker** Generates a color picker. Its output is hexadecimal, e.g. #ff0000 for red.
* **Date** Generates a date picker. Its output is a date in the YYYY-MM-DD format.
* **File** Generates a single file uploader / picker. Uses FileMan
* **Files** Generates a multiple file uploader / picker along with descriptions.
* **Image** Generates an image uploader / picker. Used for banners, thumbnails and other graphical elements.
* **Listbox** Generates a listbox based on the values given.
* **Radiolist** Generates a list of radio items.
* **Textarea** Generates a text area as per the HTML standard.
* **Textfield** Generates a text input field as per the HTML standard.
* **URLs** Generates a list of hyperlinks. Each links has an address, a description and a target.

#### API for content types

As long as `com_cck` is part of a Joomla! or Nooku application, the types above can be called manually in forms. Most, if not all
of the types need a single parameter, which is a array of configurable parameters:

* **model** (string) Name of the called model.
* **value** (mixed) the value or values of the element
* **name** (string) the name of the element in the form. Commonly a slug.
* **text** (string) title text.
* **required** (boolean) Is an element required?
* **selected** (mixed) Sets the default value when multiple options are selectable.  => $config->row->value,
* **attribs** (array) HTML attributes with their values
* **filter** (mixed) Optional filters
* **translate** (boolean) makes an element optionally translatable

Please note that the exact number of parameters differs as per context. After all when an element has a single value, the
'selected' attribute will be irrelevant, so it will not be a required or optional parameter.

### Connections

***Note*** This function is invisible to the content editor. Any misconfiguration will thoroughly break stuff. Therefore,
this functionality is only accessible to the developer!

A connection is the actual link between a package and a fieldset. Whenever a package has items that need a fieldset,
a connection needs to be configured. When an item is edited, the proper fieldsets are retrieved and the proper forms
are generated. Each connection consists of the following elements:

* **cck_fieldset_id** Name of the fieldset
* **title** Sets the title of the fieldset that needs displaying.
* **slug** automatically generated
* **package** The name of the package that uses the fieldset
* **name** The name of the element within the package that needs displaying. The developer will recognize that this
 refers to the view within the package.
