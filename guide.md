# Guide for editing the Edge Computing Group Website UPRM

## Author: Jacob M. Delgado López

Hello! This is a guide on how to edit the Website for future students. (Hopefully I didn't do too bad of a job and the website is still being used). 

I will explain the folders and their purpose. I will also mention when I folder was NOT edited during the creation of the website. If they were not edited then it's safe to assume you won't hve to either, unless you want to get creative and risk the website exploding :P 

### Folders:

_data = Contains yml files which are used to store stuctured data. For example, members.yml stores information about the lab members like names, roles, images, etc.

_includes = Contains html files for various aspects of the website. For example, the footer was edited to include the UPRM logo.

_layouts = Contains html files for establishing common layouts. This was not edited

_posts = used for blog posts. Can be leverage to add a News sections to the website. This was not edited.

assets - CSS = Contains css files. beautifuljekyll is the global css and was edited for styling of the website
         img = Contains images from original fork. This was not edited
         js = Contains js for jekyll. This was not edited

images - lab_photos = Contains group photos of the lab
       - members = Contains images of the members from the lab. 

pages = Contains markdown files that have the structure of the pages in the navbar

### Important files you will probably edit:

index.html = This the home page for the website. Here you can edit the photo that is displayed, text or the PI's email

_config.yml = This file connects the whole website and makes it run. Here you configure the navbar to connect to other pages. Additonally, can also chnage the color Scheme of the website.

members.yml = This file contains all the informaiton regarding the members of the lab. To add a new member, go to the apropriate section (Postdoc, PhD, Master's, etc.), copy paste an existing entry, and fill in the appropriate information.

publications.yml = This file contains the publications made by the lab. To add a new publications, copy paste an existing entry and fill in the appropriate information.

lab_photos.md = This file displays photos of the lab throughout the years (maybe you can spot me)

You can assume that all the other files should be left as is. If you do want to edit them, be careful!

I hope this guide was helpful! If it was, say hello to Dr. Wilfredo and the rest of the lab for me. 

Wish you the best on your reseach!