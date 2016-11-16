# Add Page By Form Plugin

The **Add Page By Form** Plugin is for [Grav CMS](http://github.com/getgrav/grav). It allows (anonymous) users to add a page by filling in a form.

## Security

This plugin is being developed for a specific use case where an anonymous user is allowed to add a page to a Grav website. The page is not visible in the menu by default but gets moderated by the Admin user. Upon approval the Admin sets 'published: true' so the page will be included in the menu.

The above use case does not require any security and so, this plugin does not provide any security measures.
Please take this in consideration before using this plugin.

## Installation

Installing the Add Page By Form plugin can be done in one of two ways. The GPM (Grav Package Manager) installation method enables you to quickly and easily install the plugin with a simple terminal command, while the manual method enables you to do so via a zip file.

### GPM Installation (Preferred) (not implemented yet)

The simplest way to install this plugin is via the [Grav Package Manager (GPM)](http://learn.getgrav.org/advanced/grav-gpm) through your system's terminal (also called the command line).  From the root of your Grav install type:

    bin/gpm install add-page-by-form

This will install the Page Creator plugin into your `/user/plugins` directory within Grav. Its files can be found under `/your/site/grav/user/plugins/add-page-by-form`.

### Manual Installation

To install this plugin, just download the zip version of this repository and unzip it under `/your/site/grav/user/plugins`. Then, rename the folder to `add-page-by-form`. You can find these files on [GitHub](https://github.com/bleutzinn/grav-plugin-add-page-by-form) or via [GetGrav.org](http://getgrav.org/downloads/plugins#extras).

You should now have all the plugin files under

    /your/site/grav/user/plugins/add-page-by-form
	
> NOTE: This plugin is a modular component for Grav which requires [Grav](http://github.com/getgrav/grav) and the [Error](https://github.com/getgrav/grav-plugin-error) and [Problems](https://github.com/getgrav/grav-plugin-problems) to operate.

## Configuration

Before configuring this plugin, you should copy the `user/plugins/add-page-by-form/add-page-by-form.yaml` to `user/config/plugins/add-page-by-form.yaml` and only edit that copy.

Here is the default configuration and an explanation of available options:

```yaml
enabled: true
dateformat: 'd-m-Y g:ia'
```
- 'enabled' determines whether the plugin is active
- 'dateformat' sets how the date time should be displayed

## Usage

Create a page with a form. Make sure the 'form.md' file looks like:
```
---
title: 'Create New Page'
route: '01.home/blog'
pagefrontmatter:
    title: 'Fallback title'
    content: 'Fallback content'
    template: item
    published: true
    instructor:
        name: 'John Doe'
        title: 'dr.'
form:
    name: new-page-form
    fields:
        -
            name: author
            label: 'Author'
            placeholder: Identify yourself as requested by your Instructor
            autocomplete: true
            type: text
            validate:
                required: true
        -
            name: title
            label: 'Page Title'
            placeholder: null
            autocomplete: true
            type: text
            validate:
                required: true
        -
            name: content
            label: 'Page Content'
            size: long
            placeholder: null
            type: textarea
            validate:
                required: true
        -
            type: spacer
            text: This text is displayed between the Content field and the Submit button
    buttons:
        -
            type: submit
            value: Submit
            classes: null
    process:
        -
            addpage: null
        -
            display: thankyou
---

You can create a new page by filling in the form below.

Please enter the Page Title and write some content to appear on the new page.
```


route sets the file location for the new page.
template specifies the Twig template to be used by the new page. This line will be added to the new page header (YAML Frontmatter).

Everything inside the pagefrontmatter block, except for 'content', will be inserted in the new page's frontmatter.
This makes it easy to use any value in a Twig template e.g. {{ page.header.author }}.

Finally, create the required Twig template file in the 'templates' folder of your theme. The template file name must match the name as set in the configuration file. So when in your configuration you have: 'template: page' then the template file name must be: 'page.html.twig'.
To create a blog post type page, simply set 'template: item' (and possibly 'published: true').

## Credits

[Slug generator by Alex Garret](http://codereview.stackexchange.com/questions/44335/slug-url-generator) and of course to everyone who contibutes to Grav.

## To Do

- Improve feedback when an error occurs during page creation.
- Explain the usage better.

