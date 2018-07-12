# Sierra Webpac BiblioCommons-like Skin

This is a BiblioCommons-like skin<a href="#1"><sup>1</sup></a> for Sierra Webpac<a href="#2"><sup>2</sup></a>, developed by Dan Lou at Palo alto City Library. The skin mimics the library's BiblioCommons website style and it is mobile friendly.

Many BiblioCommons libraries want to keep the Sierra Webpac as a backup catalog for  the following reasons:

* To meet the needs of library customers who just want to have a basic catalog to search and borrow items.
* Some functions are only available in Webpac for now, and make the Webpac pages look and feel like BiblioCommons will enhance user experience.
	* The self registration web page where customer first request a library card online.
	* The personal information modification web page where customers can opt in or out of SMS services.
* BiblioCommons uses APIs to talk to ILS. It is rare, but Webpac could serve as a backup in case the API services get interrupted.

This project attempts to keep the consistent look and feel of multiple library catalog websites, and to provide a more modern and user-friendly Webpac. 

This repository contains the Webpac files that got most heavily customized for the purpose, where I try to push the limits of Webpac and apply BiblioCommons style to it.

## Install

1. I recommend to install this first on your staging port or on your training server. Upload the Siera Webpac example set from Innovative Interfaces via Sierra Webmaster module if you have not already had a Webpac running on the specific port/server.
2. Clone or download this repository. Upload all files in `webpac` folder via Sierra Webmaster module. This will update existing files in Webpac and add new ones required by this new skin. 
3. Rename wwwoptions.txt to wwwoptions and restart Webpac.
4. Customize image files, CSS files and html files to match your library's specific style as needed. For example, use your library's own logo images. 
5. When you are ready to make the above changes to your live port, remember to back up all files on your live port first, as Innovative Interfaces recommended. Also, if you have the free enhancement product Airpac for Smartphones, please request Innnovative Interfaces to disable that. The new design is mobile responsive, so let's say good bye to Airpac and keep all user interface consistent across devices.


## Screenshots

### Main page/ Opac page view

 Desktop | Mobile 
----------|-----------
<img src="screenshots/webpac_main.png" width=300 alt="desktop view"> | <img src="screenshots/webpac_main_mobile.png" width=200 alt="mobile view"> 

### Browse page view

 Desktop | Mobile 
----------|-----------
<img alt="desktop view" src="screenshots/webpac_keywordsearch.png" width=300> | <img alt="mobile view" src="screenshots/webpac_keywordsearch_mobile.png" width=200> 

### Record view

 Desktop | Mobile 
----------|-----------
<img alt="desktop view" src="screenshots/webpac_bib.png" width=300> | <img alt="mobile view" src="screenshots/webpac_bib_mobile.png" width=200> 

### Patron account view
 Desktop | Mobile 
----------|-----------
<img alt="desktop view" src="screenshots/webpac_patronaccount.png" width=300> | <img alt="mobile view" src="screenshots/webpac_patronaccount_mobile.png" width=200> 

## Documentation

### CSS

Most of the customizations are for combining BiblioCommons style with Webpac code, and at the same time, make it mobile responsive:

* external_library_branding.css
* header_all.css
* style.css
* styles.css

If you are a BiblioCommons website, you can also download the first three stylesheets from your BiblioCommons site. A note here is that I did make some changes to these files, like fonts, colors or anything in conflict with my Webpac style.

### WWWOPTIONS

This is a speical beast in Webpac and it is very powerful.

* wwwoptions

Almost all buttons are customized here in order to get rid of or replace those classic but poor-quality icons that appear everywhere in Webpac.

To keep the interface cleaner and make localization easier, it is best not to specify text for material type icons. But in our case, we want to have it, but the label will automatically disappear if you are on a mobile view. As an option, you can easily delete the label from the we boptions. For example, the book material type `a` web option can be changed to

```
IMAGE_MATTYPEa="class="hidden" alt="Book"/><span class="icon icon-book-series" aria-hidden="true"></span><a style="hidden>
```

Web Options also provide a way to control many other system generated code in Webpac, such as which HTML file to use for header and footer, what meta tags and scripts should get linked to in head in almost every HTML page, etc.. It also works with webpub.def file to control many crucial search/display functions and behaviors in Webpac. We did not touch any crucial functions in this repository.


### HTML

To make the CSS take effect in webpac, we need to heavily rewrite html code in webpac. 

#### Header and Footer

* toplogo.html
* toplogo_loggedin.html
* botlogo.html

Create brandnew header and footer in Webpac. You can bring in the exact same header and footer from BiblioCommons, including the sub menus in top navigation bar. Make sure you call out to BootStrap jquery and javascript files. 

	<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
	<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>

In our case, we decided to simplify things a bit. The header and footer in Webpac do not contain many links to BiblioCommons. To further differentiate the two catalog interfaces, Webpac is in a different color.

#### Search Pages

Customize the main page, the main search page and the advanced search page:

* mainmenu.html
* opacmenu.html
* srchhelp_X.html

We decided to make the main search page (web path /search) and main page(web path /) the same. It contains a simple search box.

#### Account Pages

* modpinfo.html
* selfreg.html
* patronview_web.html

Most of the work is done to make these mobile responsive. These pages are very unfriendly for customization since the tables or divs in side often do not have a unique id or class.

I also customized the selfreg.html to contain a birthdate field that integrates a smart JQuery calendar. The code in the repository automatically generate the following view:

| Desktop view with birthdate calendar overlay open            | Mobile view with birthdate calendar overlay open             |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| <img alt="desktop view" src="screenshots/selfreg.png" width=300> | <img alt="desktop view" src="screenshots/selfreg_mobile.png" width=200> |


#### Localization and Translation

I did some light localization in Chinese, Russian and Spanish:

* toplogo_chx.html
* toplogo_loggedin_chx.html
* mainmenu_chx.html
* opacmenu_chx.html
* srchhelp_X_chx.html
* bib_display_chx.html
* acquire_web_chx.html
* toplogo_rus.html
* toplogo_loggedin_rus.html
* mainmenu_rus.html
* opacmenu_rus.html
* srchhelp_X_rus.html
* bib_display_rus.html
* acquire_web_rus.html
* toplogo_spi.html
* toplogo_loggedin_spi.html
* mainmenu_spi.html
* opacmenu_spi.html
* srchhelp_X_spi.html
* bib_display_spi.html
* acquire_web_spi.html

Please refer to Sierra Dcumentation if you want to have the website fully localized in a foreign language.

### Logo Images

* favicon.ico
* logo.png
* mobile_logo.png
* PAC_Library_Logo_leaf-150x150.png

---

1. <a name="1"></a>BiblioCommons is a modern layer of online catalog. The CSS is mainly based on Bootstrap. It coexistes with library's Integrated library systems (ILSs) and creates a complete OPAC replacement.

2. <a name="2"></a>Webpac is the online catalog interface for libraries that use the Sierra/Millennium ILS from Innovative Interfaces.


