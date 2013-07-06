Git Manual
==========
Here is a small Git guide, created because we usually use prepared software for working with repositories, but after we should be able to know command line git instructions. It's much better than any other UI client! :-) 

Repository initialization
---------------------------
```
touch README.md
git init
git add README.md
```
or, if you've already all your project initialized
```
git add . //Check all files to next commit
git commit -m COMMIT //It creates a new commit
git remote add origin URL //We add a remote, as https://github.com/m3n0R/GitManual.git
```
There is another way to initialize a repository
```
git clone /path/to/repo //We create a local copy of the repository
git clone username@host:/path/to/repo //We create a remote copy of the repository
```

Work flow
---------
Your local repository is composed by three "trees", managed by git. The first one is your "Working folder" that contains all files. The second one is the "Index" which plays a middle area rol, and finally "HEAD" wich points to last commit released

<img src="https://github.com/m3n0R/GitManual/blob/master/resources/flow.png">





===================================================== 



Ramas
-----
Para crear ramas hay varias formas de hacerlo:
* Mediante la instrucción ```git checkout -b``` --> Crea una nueva branch y apunta a ésta.
* Mediante la instrucción ```git branch``` --> Crea una nueva branch pero te deja apuntando a la que estabas.
```java
git branch // muestra todas las ramas
git branch BRANCH //crea una nueva branch
git branch -b BRANCH //crea una nueva branch y la hace la branch activa. Aunque también se puede hacer git branch y después git checkout <BRANCH>
git branch <BRANCH> <COMMIT> // crea la rama a partir del commit dado.
git branch -b <BRANCH> <COMMIT> //crea la rama a partir del commit dado y hacerle checkout
git branch -m <actual> <nuevo> //renombra la rama
```


Repositorios remotos
--------------------
```java
git push origin <BRANCH> // Hacemos un push al remote origin, BRANCH suele ser master
``

























<a href="http://img27.imageshack.us/img27/1590/screen1es.png" alt="Screen 1">
  <img src="http://img27.imageshack.us/img27/1590/screen1es.png">
</a>


Try out the sample application

<a href="https://play.google.com/store/apps/details?id=com.manuelpeinado.multichoiceadapter.demo">
  <img alt="Android app on Google Play"
       src="https://developer.android.com/images/brand/en_app_rgb_wo_45.png" />
</a>

Or browse the [source code of the sample application][1] for a complete example of use.





Alternatively, you can, of course, use the ID of an existing app.

In either case, you will also need to associate your Android key hash with the app. Click 'Edit App' and open up the 'Native Android App' section at the bottom of the dashboard. Add the key hash that you obtained at the end of the previous step with the keytool app.

<a>
  <img src="https://fbcdn-dragon-a.akamaihd.net/cfs-ak-ash3/676658/827/440884335967686-/Screen%20Shot%202012-10-17%20at%2010.45.03%20PM.png" />
</a>

Save this change.

You will also need to return to this dashboard and add your app's package name and main activity class once you have created a new Android project itself.

2 - In your App

* Register the package and activity with Facebook

At this point, you should return to the App Dashboard on the Facebook Developers site and add your Android app's package and activity names to the Android settings. Also enable 'Facebook Login':






License
-------

Copyright 2013 m3n0R

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.


[1]: https://github.com/m3n0R/EasyFacebookConnect/tree/master/EasyFacebookConnect-Samples





