# Use NPM to automatically reload any project
This is a brief step-by-step guide outlining how you can use npm and a package called "lite-server" to automatically reload static content sites for your local development.

## what does all of this mean?
It means, if you are working on simple sites using only CSS, HTML, and ordinary JavaScript, you won't have to manually hit F5 to update your site after every change you make. The browser will refresh automatically as you work.

## Requirements
The approach is quite simple and is like using any other software, except we run it from the command line, instead of through a normal user interface

## steps
1. Install [Node](https://nodejs.org/en/) - If you don't know which version to get pick whichever version is marked "LTS" for your operating system. (LTS stands for Long Term Support) which generally means this version will be patched and maintained by the people working on Node for a longer time than the other verisons on offer.
2. Open up your command line tool

* On Windows press and hold `[WIN] + [R]` then type `cmd` and hit enter.
* On a Mac press and hold `[Cmd] + [Space]` and type `terminal` then hit enter.

3. Change the [Working Directory](https://www.computerhope.com/jargon/c/currentd.htm) to the root of your project. That is the folder containing your index.html, javascript files, and css files.
4. Once your working directory is in your root directory type the following command: `npm init`. The tool will prompt you for some information. It is safe to ignore these for now and simply hit enter until it stops bothering you.
5. If you've followed the previous steps correctly, you will note a new file has been created alongside your other work files named `package.json`

* If you do not see package.json in the same folder as your other work files it is likely that you did not set your current working directory correctly before running the command.

6. If you see the `package.json` file, you can type the next command `npm i lite-server`

* **NOTICE** this operation will download files on your computer, and put them in a folder names node_modules in your current working directory).

7. Open up your package.json file and add the following code to its structure

```
"scripts": {
  "dev": "lite-server"
}
```

If you've added the section correctly your package.json file should look something like the below example (version numbers notwithstanding).
```
{
  "name": "",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "dependencies": {
    "lite-server": "^2.5.4"
  },
  "devDependencies": {},
  "scripts": {
    "dev": "lite-server"
  },
  "author": "",
  "license": "ISC"
}
```
*note* if you already have a scripts section you can replace it with the statement from step 7.

Additionally, take note that none of the other sections technically matter to you yet as you are only using NPM to download a package for your local development. The other fields only become important if you intend to publish a package.


8. After the download is complete, and your `package.json` file has been edited type the following command in your terminal: `npm run dev`

And that is it. If you successfully followed this guide your terminal should be hosting your project files in a small web server for local development on the following url: `localhost:3000`

Note 1: You will only have to perform the setup steps once pr. project. The next time you want to work you will only have to perform step 3 and 8.

Note 2: By convention, the first page the lite-server package looks for is named `index.html`, so you should rename your frontpage to `index` if it is not already named so.