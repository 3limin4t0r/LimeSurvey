# Question templates for LimeSurvey

Coming with the 3.X Verson of LimeSurvey you will be able to create your 
own set of questiontypes and alternative views for questions.

All you need to know is a little html and xml.
(And for the more advanced stuff also js and css would help.)

## The config.xml

Config files are very common, a.e. joomla. The config file for the question-template 
should contain a few basic things.

### Metadata - Or, what is this about and who has written it?

Your question view or type should have your name and your email on it, so people can ask questions and congrat you to 
your awesome question type

Also you should give some informatione about the used licence (remember LimeSurvey is GPL) and a short description.

It makes a lot of sense to write wich version of the view it is, to let people know If they would have to update

The `metadatas` part should therefor look something like this:

```xml
    <metadatas>
        <name>MyAwesomeQuestionView</name> 
        <creationDate>23/12/2016</creationDate>
        <author>LimeSurvey Programmer</author>
        <authorEmail>info@limesurvey.org</authorEmail>
        <authorUrl>http://www.limesurvey.org</authorUrl>
        <copyright>Copyright (C) 2005 - 2016 LimeSurvey Gmbh, Inc. All rights reserved.</copyright>
        <license>GNU General Public License version 2 or later</license>
        <version>1.0</version>
        <apiVersion>1</apiVersion>
        <description>Everything will be better with this questiontype</description>
    </metadatas>
```

### Files - Or, do we need some other stuff?

You can add peripheral files to the question view. 

Please make sure, that you put your own files in an `asset` folder in the base folder of your question view.

The `files` part should look somnething like this:
```xml
<files>
    <css>
        <filename>css/mycss.css</filename>
    </css>
    <js>
        <filename>scripts/myscript.js</filename>
    </js>
</files>
```

### Custom Attributes - Or, I want it my way.

You can add your own attributes.

These will be visible and editable in the question edit view in the backend.

So if you would like to add some more power to your question view, like a unified greeting message over every question of this type.
Or fixed width and height of images in the question. Anything you can think of.

You can have as many extra attributes as you want. But be careful not to flood the question edit view with a million new attributes.

For a full list of possible inputtypes please have a look at the questionHelper in application/helpers

A full list is coming someday.

The `custom attributes` part should look something like this:
```xml
<custom_attributes>
    <attribute>
        <name>myCustomAttribute</name>
        <category>Display</category>
        <sortorder>90</sortorder>
        <inputtype>text</inputtype>
        <default>defaulttext</default>
        <help>Describing what this custom attribute will do.</help>
        <caption>My custom Attribute: </caption>
    </attribute>
</custom_attributes>
```

### Engine - Or, Somehow the system has to know about this.

Last but not least you have to tell LimeSurvey where to put and what to do with your question view/type.
And if your extra css/js should be loaded.

You can choose to make it visible as well as a question template as a new question type.

This is rather important, because you won't be able to use your question template if you do not make it visible.

The `engine` part should look like this:
```xml
    <engine>
        <load_core_css>true</load_core_css>
        <load_core_js>true</load_core_js>
        <show_as_template>true</show_as_template>
        <show_as_question_type>true</show_as_question_type>
    </engine>
```

### A working example - Or, just that.

Here is a complete example of a config.xml file for your own question view.

Just take this as a basis and build on top of it.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<config>

    <metadatas>
        <name>YourAwesomeQuestionView</name> 
        <creationDate>23/12/2016</creationDate>
        <author>LimeSurvey Programmer</author>
        <authorEmail>info@limesurvey.org</authorEmail>
        <authorUrl>http://www.limesurvey.org</authorUrl>
        <copyright>Copyright (C) 2005 - 2016 LimeSurvey Gmbh, Inc. All rights reserved.</copyright>
        <license>GNU General Public License version 2 or later</license>
        <version>1.0</version>
        <apiVersion>1</apiVersion>
        <description>Everything will be better with this questiontype</description>
    </metadatas>

    <files>
        <css>
            <filename>css/mycss.css</filename>
        </css>
        <js>
            <filename>scripts/myscript.js</filename>
        </js>
    </files>

    <custom_attributes>
        <attribute>
            <name>myCustomAttribute</name>
            <category>Display</category>
            <sortorder>90</sortorder>
            <inputtype>text</inputtype>
            <default>defaulttext</default>
            <help>Describing what this custom attribute will do.</help>
            <caption>My custom Attribute: </caption>
        </attribute>
    </custom_attributes>

    <engine>
        <load_core_css>true</load_core_css>
        <load_core_js>true</load_core_js>
        <show_as_template>true</show_as_template>
        <show_as_question_type>true</show_as_question_type>
    </engine>
</config>
```

## The folder structure

To be able to work the question template needs a dedicated structure.

It is rather important, because otherwise the framework would not be able to get the files from 
the correct location. This would lead to massive errors and we already have enough of that.

So here is an example structure for working on top of a multiplechoice question:

```tree
upload/
└── question_templates/
    └── my_awesome_template
        └── survey
            └── questions
                └── answer
                    └── multiplechoice
                        ├── answer.php
                        ├── assets
                        │   ├── css
                        │   │   └── my_awesome_template.css
                        │   └── scripts
                        │       └── my_awesome_template.js
                        ├── columns
                        │   ├── column_footer.php
                        │   └── column_header.php
                        ├── rows
                        │   ├── answer_row_other.php
                        │   └── answer_row.twig
                        └── config.xml

``` 