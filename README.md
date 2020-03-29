

<a  href="https://marcelkolarcik.github.io/simple-jQuery-translator/index.html" target="_blank">
# simple-jQuery-translator - Demo
</a>

# simple-jQuery-translator 
 Simple jQuery translator, that will translate text, title of element, placeholder of input fields, alt attribute of image.
 
 If you need to include variables, simple-jQuery-translator can handle it as well.
 
 # Table of content 
- [Instalation](#Instalation)
- [HTML examples](#HTML-examples)
- [Variables](#Variables)
- [Usage](#Usage)
- [Browser support](#Browser-support)
 
 
 # Instalation 
 
  #### Download <code>assets/js/translator</code> folder from <a href = "https://github.com/marcelkolarcik/simple-jQuery-translator">simple Jquery translator repository</a >
  and place it in the root directory of your project.
                                     
 >  If developing locally, you will need to run HTTP server. One of them can be found at
                                    <a href = "https://github.com/lwsjs/local-web-server">local web server</a >.      
                                    
 >  If you are using any of the online translators, feel free to download <code>index.html, helper.html, usage.html, variables.html</code>
   and <code>assets/js/translator_helper</code> folder with it's files
   and follow the instruction in <a href = "https://marcelkolarcik.github.io/simple-jQuery-translator/helper.html">helper.html</a >
   to help you create translation JSON files faster.   
   
   > After creating translation JSON files using assets/js/translator_helper files and <code>index.html, helper.html, usage.html, variables.html</code> files, delete them from your 
   project directories, because they won't be needed anymore.
   
  #### Create translation JSON files and place them in  assets/js/languages 
  ```json
{
  "hello"                                                                                   : "Hola" ,
  "Examples"                                                                                : "HTML Ejemplos" ,
  "this is link"                                                                            : "este es el enlace" ,
  "label"                                                                                   : "etiqueta" ,
  "Your idea"                                                                               : "Tu idea" ,
  "Create something amazing..."                                                             : "Crea algo increíble ..." ,
  "image alt description"                                                                   : "descripción alternativa de la imagen" ,
  "helper"                                                                                  : "Ayudante" ,
  "link"                                                                                    : "enlace" ,
  "logo image"                                                                              : "Logotipo" ,
  "translate"                                                                               : "traducir" ,
  "switch to english"                                                                       : "Cambiar a inglés" ,
  "switch to slovak"                                                                        : "cambiar a eslovaco" ,
  "switch to spanish"                                                                       : "cambiar a español" ,
  "switch to polish"                                                                        : "cambiar a polaco" ,
  "english flag image"                                                                      : "imagen de la bandera inglesa" ,
  "slovak flag image"                                                                       : "imagen de la bandera eslovaca" ,
  "spanish flag image"                                                                      : "imagen de la bandera española" ,
  "polish flag image"                                                                       : "imagen de la bandera polaca" ,
  "Home"                                                                                    : "Hogar" ,
  "Link"                                                                                    : "Enlace" ,
  "Disabled"                                                                                : "Discapacitado" ,
  "Search"                                                                                  : "Buscar" ,
  "Title of element : data-title attribute"                                                 : "Título del elemento: atributo de data-title" ,
  "Placeholder for input fields : data-placeholder attribute"                               : "Marcador de posición para campos de entrada: atributo de data-placeholder" ,
  "alt attribute for images : data-alt attribute"                                           : "atributo alt para imágenes: atributo data-alt" ,
  "No translation for text"                                                                 : "Sin traducción de texto" ,
  "Examples of usage"                                                                       : "Ejemplos de uso" ,
  "Single data-text attribute"                                                              : "Atributo de data-text único" ,
  "Multiple data-text attribute"                                                            : "Atributo de data-text datos múltiples" ,
  "If there is no translation for the text, we will display text from data-text attribute." : "Si no hay traducción para el texto, mostraremos el texto del atributo de data-text" ,
  "Every element that need translating must have class"                                     : "Cada elemento que necesita traducción debe tener la clase" ,
  "and any combination of"                                                                  : "y cualquier combinación de" ,
  "with values written in default language"                                                 : "con valores escritos en idioma predeterminado" ,
  "___ ( three underscores )"                                                               : "___ (tres guiones bajos)" ,
  "Usage"                                                                                   : "Uso"
}
```
   
  #### Update <code>settings.js</code> 
   
   > Open settings.js in assets/js/translator/settings.js and update variables to match your site.
   
   ```javascript
   /*SITE'S DEFAULT LANGUAGE*/
   var default_language = 'en'; // Demo example : "en"
   
   /*PATH TO LANGUAGE FILES, UPDATE TO YOUR PROJECT'S FOLDER STRUCTURE*/
   var path_to_language_files = 'assets/js/languages'; // Demo example : "assets/js/languages"
   
   /*WHAT LANGUAGE FILES YOU ARE USING , FOR EXAMPLE: <br >
    DEMO SITE IS USING en.json, sk.json, es.json, pl.json => site_languages = ["en","pl","sk","pl"].*/
   var site_languages = ["en","pl","sk","pl"]; // Demo example : ["en","pl","sk","pl"]
   
   /*FOR DEVELOPMENT ONLY IF YOU WANT TO HIGHLIGHT TEXT THAT
     IS NOT TRANSLATED TO ANY PARTICULAR LANGUAGE YET
     SET highlight_class THAT WILL BE APPLIED TO ELEMENT THAT IS NOT TRANSLATED YET TO HIGHLIGHT IT
     TO NOTIFY YOU!
    SWITCH OFF IN PRODUCTION 
    var highlight_class =  ''  ; */
   var highlight_class = 'bg-warning text-danger p-1'; // Demo example : 'bg-warning text-danger p-1'
   ```      
   #### Include jQuery and translator.js in your HTML files, that need translating at the bottom of the the body.
   
   ```html
   
   <!--jQUERY JS -->
   	<script
   			crossorigin = "anonymous"
   			integrity = "sha256-WpOohJOqMqqyKL9FccASB9O0KwACQJpFTUBLTYOVvVU="
   			src = "https://code.jquery.com/jquery-3.4.1.js"	></script>
   
   	
   	<!--translator.js -->
   <script
   			src = "assets/js/translator/translator.js"
   			type = "module"></script>
   	
   ```     
   
   > If you want to use bootstrap's dropdown for changing languages as in demo example you will need to include bootstrap's css
    in document's head and change_language.js at the bottom of document's body.
   
   #### change_language.js 
   
   ```javascript
   /*USER CHANGING LANGUAGE*/
   $ ( document ).on ( 'click', '.language', function ()
   {
   	
   	var current_language =  $ ( this ).data ( 'language' );
   		
   	localStorage.setItem ( 'language', current_language );
   	
   	/*TRANSLATING ACCORDING TO USER CHOSEN LANGUAGE*/
   	translate ();
   	
   	/*CHANGING CHOSEN LANGUAGE FLAG IN NAVIGATION BAR , OPTIONAL*/
   	change_flag ( current_language )
   	
   } );
   ```
   
   ```html
   <!--BOOTSTRAP CSS FILES IN DOCUMENT'S HEAD-->
   	<link
   			crossorigin = "anonymous"
   			href = "https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css"
   			integrity = "sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh"
   			rel = "stylesheet"
   	>
   ```
   
   ```html
    <!--change_language.js AT THE BOTTOM OF THE BODY-->
   <script
   			src = "assets/js/translator_helper/change_language.js"
   			type = "module"
   	></script>
   	
``` 
	
>  If you want to use change_flag( current_language ) function to display flag next to the language name, 
	as in demo example, you will need to get country flags images and place them in 
	<code>assets/images/flags</code>and update paths with correct image name and path in dropdown navigation.
	 
> Country flags can be found <a href = "https://github.com/hjnilsson/country-flags">at country-flags</a > repository 
	
	 
#### Part of demo example dropdown navigation

```html 
<li class = "nav-item dropdown">
			  <a
					  aria-expanded = "false"
					  aria-haspopup = "true"
					  class = "nav-link dropdown-toggle ___"
					  data-toggle = "dropdown"
					  href = "#"
					  id = "language_flag"
			  >
				<img
						alt = ""
						class = "___"
						data-alt = "english flag image"
						src = "assets/images/flags/en_sm.png"
				></a>
			  <div
					  aria-labelledby = "language_flag"
					  class = "dropdown-menu"
			  >
				<a
						class = "dropdown-item language ___"
						data-language = "en"
						data-title = "switch to english"
						href = "#"
				>
				  <img
						  alt = ""
						  data-alt = "english flag image"
						  src = "assets/images/flags/en_sm.png"
				  >
				  &nbsp;english</a>
				<a
						class = "dropdown-item language ___"
						data-language = "sk"
						data-title = "switch to slovak"
						href = "#"
				>
				  <img
						  alt = ""
						  data-alt = "slovak flag image"
						  src = "assets/images/flags/sk_sm.png"
				  >
				  &nbsp;slovak</a>
				<a
						class = "dropdown-item language ___"
						data-language = "es"
						data-title = "switch to spanish"
						href = "#"
				>
				  <img
						  alt = ""
						  data-alt = "spanish flag image"
						  src = "assets/images/flags/es_sm.png"
				  >
				  &nbsp;espanyol</a>
				<a
						class = "dropdown-item language ___"
						data-language = "pl"
						data-title = "switch to polish"
						href = "#"
				>
				  <img
						  alt = ""
						  data-alt = "polish flag image"
						  src = "assets/images/flags/pl_sm.png"
				  >
				  &nbsp;polish</a>
			  </div>
			</li>
```
	
# HTML examples



### See examples live at <a  href="https://marcelkolarcik.github.io/simple-jQuery-translator/index.html" target="_blank"> simple-jQuery-translator - live Demo </a>
                                                                                                                                                  
                        

> Every element that need translating must have class
     ___ ( three underscores )
    
> and any combination of
    data-text, data-title, data-placeholder, data-alt
    
> with values written in default language

#### Single data-text attribute

```html
<span class = "___" data-text="hello" ></span>
```

#### Multiple data-text attribute

```html
<p>
<span class = "___" data-text = "This is" > </span >
<strong class = "___ " data-text = "bold text." > </strong >
<span class = "___  text-info bg-secondary p-3" data-text = "And this is green text on grey background" > </span >
</p>
```
   
  #### Title of element : data-title attribute
  
```html
  <a class = "___" data-title = "this is link" data-text = "link" href = "#" > </a >
```
  
  #### Placeholder for input fields : data-placeholder attribute
    
```html
    <label class = "___ " data-text = "Your idea" for = "placeholder" ></label >
    <textarea class = "___ form-control col-md-6" data-placeholder = "Create something amazing..." id = "placeholder" ></textarea>
```
 #### alt attribute for images : data-alt attribute
    
```html
   <img class="___" src = "/assets/images/non_existing_file.png" data-alt = "image alt description" alt=" " >
```

 #### If there is no translation for the text, we will display text from data-text attribute.
    
```html
   <p class="___" data-text="Not translated string" ></p>
```
# Variables

> If you need to include variable(s) in the text, following examples will help you achieve that.

### Variables live at <a  href="https://marcelkolarcik.github.io/simple-jQuery-translator/variables.html" target="_blank"> simple-jQuery-translator - variables </a>
                                                                                                                                                  
    
 # Usage 
 
 ### First load of the page
 
 > Translator will try and match any of site language(s) with browser language(s) by running translate(); function.
  
 > If there will be match, page will be translated to matched language.
  
 >  Otherwise page will get translated to default language as set in
   assets/js/translator/settings.js
   
 >  In any case we will store this language into localStorage .
 
 ### User changing language
 
 > When user changes language, we will run translate(); function again
  and page will be translated to that language. And newly selected language will be set in localStorage.
  
 > In the demo example, we are using bootstrap's dropdown, and 'click' event to trigger translate(); function.
 
 > You can of course apply different logic for triggering translate(); function.
     assets/js/translator_helper/change_language.js
     
 # Browser support
 
 Currently supporting
 
 - Firefox
 - Chrome
 - Opera 
 - Edge and UC Browser might behave strangely :  jQuery's $.getJSON() is not loading language files, sometimes...
    ( looking for fix )
 