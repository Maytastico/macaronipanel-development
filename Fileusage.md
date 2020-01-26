- [**Files**](#files)
  - [File specification](#file-specification)
  - [The File class](#the-file-class)
- [**Userspace**](#userspace)
- [**Modules**](#modules)
  - [Module Structure](#module-structure)


# **Files**
This application contains a simple file administration tool and it is devided in an userspace and modulespace.
A security issue with files in MacaroniPanel is that everyone who knows where the files are located can access and crawl them. That's a problem for files that can be observed like images, .pdf, .html or .txt files but it is easy to display or link to a files inside a webpage. The main use-case for files in Macaroni is for adding modules to the system and manipulate picture of a website.  

## File specification
A file inside MacaroniPanel is represented inside the database and is stored inside the Panel. There are some options that can be set inside the database.
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
- Folderpath
  - An absolute path to the file. It does not contain the foldername of were the MacaroniPanel is saved

![Files Entity Relationship Model](https://github.com/MacaroniDamage/macaronipanel-development/blob/master/fileER/fileER.png)

## The File class
The file class is able to add, remove and edit the information of a file.

![file](https://github.com/MacaroniDamage/macaronipanel-development/blob/master/file/file.png)

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


