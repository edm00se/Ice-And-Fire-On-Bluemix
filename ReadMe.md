# App of Ice and Fire on Bluemix

Rather, a Bluemix capable version, which runs perfectly fine in a traditional Domino server environment.

## The App

The application itself is a modified version of the origial [App of Ice and Fire](https://github.com/edm00se/AnAppOfIceAndFire), which was a culmination of efforts on segregated application design, Java HTTPServlets which extend DesignerFacesServlet, which includes FacesContext access (granting us access to the user's Session), other excellent goodies.

This application, while not using much in the way of XPages design elements, relies on the XPages runtime and demonstrates the flexibility, power, and capability of development with the XPages runtime.

## Setup

This version includes the relevant JARs that are required, in the Code/Jars path (Code/JARs, in Domino Designer). The only things required to get this application running in your own environment are:

* `.../jvm/lib/security/java.pol` needs to be updated with
 
	```
		grant {
        	permission java.security.AllPermission;
		}
	```
	Note: This is not as scary as it sounds, it just means that we're allowing our Java codethat happens to be inside an NSF to be able to run priveleged operations, the same as you would get from code deployed in an OSGi plugin, in a JAR in .../jvm/lib/ext/, or inside a _doPriveleged_ block; it's just easier this way.
* in `notes.ini` (or Internet Site document), set `HTTPEnableMethods=PUT,DELETE`
* ensure the `lwpd.domino.adapter.jar` is a part of the build path for your generated NSF (from the application's ODP)
	Note: Probably only if you notice an error in your Problems tab, you may need to inspect your Build Path (found under the Project menu) and ensure that the `lwpd.domino.adapter.jar` JAR is added as an "External JAR". If you're looking for a step-by-step on this, [Sven Hasselbach did a decent write up on this](http://hasselba.ch/blog/?p=746).

## Back-End Mock

To mock the back-end and run the client/UI app without a Domino server (with no back-end logic by the *HTTPServet*s), you can use `json-server`. To do this, you can either install the dependencies specified in the _package.json_ file by running `npm install` or you can install `json-server` globally yourself, via `npm install -g json-server`. [Create a symlink](http://www.howtogeek.com/howto/16226/complete-guide-to-symbolic-links-symlinks-on-windows-or-linux/) to the App ODP/WebContent path called 'public'; this is how `json-server` will identify the directory with the static assets. To start, from the project path, either run `json-server --id unid --watch housesDB.json --routes routes.json` or just use `npm start`. The _package.json_ file defines the same for the _start_ command that _npm_ will use.

## History

This application been the subject of of numerous blog posts of mine, as I've progressed through building it out. It has also been featured in a couple Notes in 9 episodes and in my 2015 MWLUG session.

* My blog series, [A Saga of Servlets](https://edm00se.io/servlet-series/)
* [Ni9 173: Getting Started With HTTPServlets](http://www.notesin9.com/2015/04/09/notesin9-173-getting-started-with-servlets/)
* [Ni9 180: Alternative Front-End Development](http://www.notesin9.com/2015/09/01/notesin9-180-alternative-frontend-development-for-xpages/)
* [MWLUG 2015's AD113: Speed Up Your Applications w/ Nginx and PageSpeed](https://github.com/edm00se/AD113-Speed-Up-Your-Apps-with-Nginx-and-PageSpeed)

## License

As with the original App of Ice and Fire and is my norm for my blog and my GitHub repositories, the work contained herein is licensed under a <a href="http://choosealicense.com/licenses/mit">the MIT License (MIT)</a>. You may use, alter, and redistribute the code herein (with citation), while expecting no warranty for its use.
