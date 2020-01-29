- [**Files**](#files)
  - [How is a file stored on the database](#how-is-a-file-stored-on-the-database)
  - [The file class](#the-file-class)
    - [Examples](#examples)
      - [Adding a file](#adding-a-file)
- [**Userspace**](#userspace)
- [**Modules**](#modules)
  - [Module Structure](#module-structure)


# **Files**
This application contains a simple file administration tool and it is devided in an userspace and modulespace.
A security issue with files in MacaroniPanel is that everyone who knows where the files are located can access and crawl them. That's a problem for files that can be observed like images, .pdf, .html or .txt files but it is easy to display or link to a files inside a webpage. The main use-case for files in Macaroni is for adding modules to the system and manipulate picture of a website.  

## How is a file stored on the database
A file inside MacaroniPanel is represented inside the database and is stored inside the Panel, on the harddisk. There are some options that can be set inside the database.
For examples:
- Tags 
  - Contains information that can be searched by a user
- Description 
  - A text that describes a picture
    - Can be used for a picture galery
    - A news feed that contains pictures
- Filename
  - To find the file
  - To search for a file
- user_id
  - Contains the id of a user
    - To show the file on the filemanage of the user
- Folderpath
  - An absolute path to the file. It does not contain the foldername of were the MacaroniPanel is saved

![Files Entity Relationship Model](https://github.com/MacaroniDamage/macaronipanel-development/blob/master/fileER/fileER.png)

## The file class
The file class combiens the content of a file. It stores advanced information from the database and contains futher information from the actual file, that is stored on the hard disk. You can describe the file class as an interface between the file on the harddisk and the database. This class has the ability to add a file to the database, to remove a file form the database and harddisk, rename a file. A thing that was important for me was validating the type and content of a file. For example validating a that the file is an image or that a file  is a video or that a file contains text.

![file](https://github.com/MacaroniDamage/macaronipanel-development/blob/master/file/file.png)

### Examples

#### Adding a file

We assume that we want to add a file that is located in `/files`. Its name is `manuel.png`.

At first we have to contruct the object. The first parameter contains the path to the file. The Folder were the Panel is stored will be concatenated inside class.

`$file = new File("/files", "manuel.png");`

Adding additional information to the file isn't nessesary but I will add a description and some tags to the file in this example.

`$file->setDescription("This is manuel when he traveled to New York");`

Adding tags to this picture can be a bit tricky because this method requiers an array as a parameter and there are two methods or more for forward an array to a method.

First method:

`$tags = array("Manuel", "Traveling", "Fun");`

`$file->setTags($tags);`

Second method:

`$file->setTags(array("Manuel", "Traveling", "Fun"));`

Futhermore the class gives you the possibility to add the file to a user, so the user is able to see the file inside its file manager. It is nessesary to put in an number as a parameter.
If you don't know the id of a user, you can user the method `User:fetchIDfromUsername()`

When you know the user id

`$file->setUser(1);`

When the user id is unknown

`$file->setUser(User:fetchIDfromUsername("Manuel"))`

If you are ready to add the file, you can add the file to the database. 

`$file->addFile();`

# **Userspace**
The userspace contains files that were uploaded by the user. A use-case would be the upload of profile pictures.

File structure:
- /userfiles
  - /{userID}

# **Modules**
The modulespace contains the folders of modules, that were added by an administrator. Inside these folders are scripts and files for a module. 

## Module Structure
A module has to contain:
  - A UI that can be accessed by the dashboard, these are inside the [/backend] folder
  - A module.json file which contains basic information of a module like:
    - author
    - version
    - name
    - The structur how on how .php or .html files should be displayed and how they are linked together inside the navigation.
    - The permissions that are essential for the module


A module may contain:
  - A folder that contains the essential [/scripts] to work. A use case can be a .php script that takes data form a website or a file inside the backend folder, that was put in by an user.
  - A folder which is called [/assets] that contains for example
    - JavaScript files
    - HTML files
    - PHP classes
    - Images
    - Videos


Structur inside the filesystem can be:
- /modules
  - /{moduleName} 
    - /scripts 
    - /assets
    - /backend
    - /module.json


