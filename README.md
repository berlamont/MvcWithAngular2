# MvcWithAngular2
<h1>This is web project configured for working with angular 2.0 -rc 4 and Microsoft Visual Studio 2015</h1>

Short instruction how to run angular 2 with MS Visual Studio

<ol>
<li>Install NPM Task Runner and Package Installer.</li>
<li>Create new empty web project.</li>
<li>Add package.json file to the solution root with next content
<pre>
{
    "name": "myproject",
    "version": "1.0.0",
    "devDependencies": {
        },
    "scripts": {
        "updateNpm": "npm install npm@latest"
    }
} 
</pre>
</li>
<li>Run "updateNpm" command from your taskrunner. <b>Even if you have last npm - do this. It is important.</b>
If you have already installed Node.js before skip this step. If not - go the Node.js and install latest version of node.js.
Inside Visual studio, go the Tools -> Options -> Projects and Solutions -> External web tools and set a path to the propper node.js version. Do not forget to move your new path up the hill.</li>
<li>Update your package json with dependencies, angular 2 needed. (With little overhead for the old browswers)
<pre>
{
  "name": "myproject",
  "version": "1.0.0",
  "devDependencies": {
    "gulp": "^3.9.1",
    "typescript": "1.8.10",
    "typings": "^1.0.4"
  },

  "dependencies": {
    "@angular/common": "2.0.0-rc.4",
    "@angular/compiler": "2.0.0-rc.4",
    "@angular/core": "2.0.0-rc.4",
    "@angular/forms": "0.2.0",
    "@angular/http": "2.0.0-rc.4",
    "@angular/platform-browser": "2.0.0-rc.4",
    "@angular/platform-browser-dynamic": "2.0.0-rc.4",
    "@angular/router": "3.0.0-beta.1",
    "@angular/router-deprecated": "2.0.0-rc.2",
    "@angular/upgrade": "2.0.0-rc.4",

    "systemjs": "0.19.27",
    "core-js": "^2.4.0",
    "reflect-metadata": "^0.1.3",
    "rxjs": "5.0.0-beta.6",
    "zone.js": "^0.6.12",

    "angular2-in-memory-web-api": "0.0.14"

  },
  "scripts": {
    "postinstall": "typings install",
    "typings": "typings",
    }
}</pre></li>

<li>Run install command from the Task runner.</li>
<li>Create app folder in the root of your solution. Add app.components.ts to the app folder.</li>
<li>Configure typescript for Visual studio. Close your project and open .csproj file in the text editor. Find PropertyGroup section and add two additional options: 
<TypeScriptExperimentalDecorators>true</TypeScriptExperimentalDecorators> <TypeScriptEmitDecoratorMetadata>true</TypeScriptEmitDecoratorMetadata> </li>
<li>Save changes and open solution.</li>
<li>Open your project properties and go to the TypeScript setting. Pick CommonJS as module system.</li>
<li>Update app.component.ts with this code.
<pre>
import { Component } from '@angular/core';
@Component({
    selector: 'my-app',
    template: 'My First Angular 2 App'
})
export class AppComponent { } </pre></li>

<li>Add main.ts to the app folder.
<pre>import { bootstrap }    from '@angular/platform-browser-dynamic';
import { AppComponent } from './app.component';
bootstrap(AppComponent);</pre></li>

<li>Add index.html to the root of your project</li>

<li>Add systemjs.config.js to the root with next code.
<pre>(function (global) {
    var map = {
        'app': 'app', // 'dist',
        '@angular': 'node_modules/@angular',
        'angular2-in-memory-web-api': 'node_modules/angular2-in-memory-web-api',
        'rxjs': 'node_modules/rxjs'
    };
    var packages = {
        'app': { main: 'main.js', defaultExtension: 'js' },
        'rxjs': { defaultExtension: 'js' },
        'angular2-in-memory-web-api': { main: 'index.js', defaultExtension: 'js' },
    };
    var ngPackageNames = [
      'common',
      'compiler',
      'core',
      'forms',
      'http',
      'platform-browser',
      'platform-browser-dynamic',
      'router',
      'router-deprecated',
      'upgrade',
    ];
    function packIndex(pkgName) {
        packages['@angular/' + pkgName] = { main: 'index.js', defaultExtension: 'js' };
    }
    function packUmd(pkgName) {
        packages['@angular/' + pkgName] = { main: '/bundles/' + pkgName + '.umd.js', defaultExtension: 'js' };
    }
    var setPackageConfig = System.packageWithIndex ? packIndex : packUmd;
    ngPackageNames.forEach(setPackageConfig);
    var config = {
        map: map,
        packages: packages
    };
    System.config(config);
})(this);
</pre></li>
<li>Press F5 to run your app. If you see My First Angular 2 App on your screen - all is ok. You can proceed developing.</li>
</ol>
