---
layout: page
title: "Go Setup Instructions"
permalink: /hw1/setup/
---

> This page is incomplete and poorly written. For 2 bonus participation points, [create a pull request](https://github.com/gwDistSys20/gwDistSys20.github.io) to improve it!

## Install Go

Follow the instructions at https://golang.org/doc/install

Follow the instructions to install Go based on your Operating System: -

<h4> 1. Download Go to your device</h4>

Click the links shown below based on your OS to download the Go installer.

<div class="container-fluid">
  <div class="row justify-content-center" style="margin-top: 12px;">
    
  <div class="col-md-3">
   <a href="https://golang.org/dl/go1.15.1.linux-amd64.tar.gz" id="start" class="download js-download">
        1. <span id="download-button" class="big js-downloadButton">Download Go for Linux</span>
        <span id="download-description" class="desc js-downloadDescription">( go1.15.1.linux-amd64.tar.gz (116 MB))</span>
      </a>
   </div>  <br>      
  <div class="col-md-3">
  <a href="https://golang.org/dl/go1.15.1.windows-amd64.msi" id="start" class="download js-download">
    2. <span id="download-button" class="big js-downloadButton">Download Go for Windows</span>
    <span id="download-description" class="desc js-downloadDescription">( go1.15.1.windows-amd64.msi (115 MB))</span>
  </a>
  </div>
  <div class = "col-md-3"><br>
  <a href="https://golang.org/dl/go1.15.1.darwin-amd64.pkg" id="start" class="download js-download">
          3. <span id="download-button" class="big js-downloadButton">Download Go for Mac</span>
          <span id="download-description" class="desc js-downloadDescription">( go1.15.1.darwin-amd64.pkg (117 MB))</span>
        </a>
  </div>
</div>
</div>

<h4> 2. Install Go in your device</h4>

Once Go installer has been downloaded, follow these steps to install Go to your device based on the Operating System used by the device: -

<details><summary><strong>Linux Installation</strong></summary>
<p>

```html
Remove all the previous versions of Go before installing a new version on the device. To do so, follow these steps:- 

1. Delete the go directory (usually /usr/local/go)
2. Remove GO bin directory from PATH environment variable of the device (edit /etc/profile or $HOME/.profile)

Once it is confirmed that all previous versions have been deleted, follow these steps to install Go:-

1. Create a Go tree in /usr/local/go, by extracting the downloaded archive into /usr/local. Run following command 
   as root or through sudo

   tar -C /usr/local -xzf go1.14.3.linux-amd64.tar.gz

2. Add the following line to the $HOME/.profile or /etc/profile

   export PATH=$PATH:/usr/local/go/bin

Note: Changes made to profile file are applied only after the user logs into computer the next time, if you want 
immediate results execute shell commands directlty or execute them via profile such as source $HOME/.profile

3. Verify the installation by confirming the version of go installed, by running following command on cmd: -

   $ go version
```
</p>
</details>

<details><summary><strong>Mac Installation</strong></summary>
<p>

```html
Remove all the previous versions of Go before installing a new version on the device. To do so, follow these steps:- 

1. Delete the go directory (usually /usr/local/go)
2. Remove GO bin directory from PATH environment variable of the device (remove the /etc/paths.d/go file)

Once it is confirmed that all previous versions have been deleted, follow these steps to install Go:-

1. Open the GUI installer package downloaded and follow the prompts to install Go.
  
2. The package installer will install Go distribution in /usr/local/go and sets PATH variable to /usr/local/go/bin,
   restart any open Terminal sessions for the change to take effect.

3. Verify the installation by confirming the version of go installed, by running following command on cmd: -

   $ go version
```
</p>
</details>

<details><summary><strong>Windows Installation</strong></summary>
<p>

```html
Remove all the previous versions of Go before installing a new version on the device. To do so, follow these steps:- 

1. Double click Add/Remove programs in the Control Panel.
2. Select Go Programming Language in Add/Remove programs and follow prompts.

Once it is confirmed that all previous versions have been deleted, follow these steps to install Go:-

1. Open the MSI installer and follow prompts to download Go.

2. By default, Go is installed in C:\Go, location can be changed as needed.

3. Verify the installation by confirming the version of go installed, by running following command on cmd: -

   $ go version
```
</p>
</details>

<h4> 3. Go Code </h4>

With this final step, the go setup is complete, check out some nice go tutorials to expand your learning: -

1) https://golang.org/doc/tutorial/getting-started
2) https://gwadvnet20.github.io/wiki/go/
3) https://golangbot.com/goroutines/
4) https://chai2010.gitbooks.io/advanced-go-programming-book/content/
5) https://www.youtube.com/watch?v=YS4e4q9oBaU
6) https://www.geeksforgeeks.org/golang/
7) https://www.coursera.org/learn/golang-getting-started

## Install VS Code

 - Follow the instructions at https://code.visualstudio.com
 - Download VS Code based on the type of OS and hardware of your device from https://code.visualstudio.com. 
 
 1) #### Installation steps for MacOS 
    - Download Visual Studio Code for macOS as a zip file from above site.
    - Extract the contents of the zip file
    - Drag "Visual Studio Code.app" to the "Applications" folder in order to make it available in the "Launchpad"
    - Open "Visual Studio Code" application by double-clicking it.
    - Right click the VS Code icon, and select "Keep in Dock" to add the application to the Dock.
 
 2) #### Installation steps for Windows
    - Download Visual Studio Code for Windows and run the installer (VSCodeUserSetup-{version}.exe)
    - Accept the agreement and check the Create Desktop Icon checkbox
    - Finally click install and Finish once installation is complete
    - Double click VS Code icon and open the application.
    
3) #### Installation steps for Linux
   - Install using snap following these commands: -
     a) sudo apt install snapd
     b) sudo snap install code --classic
   - Install using the .deb/.rpm packages from https://code.visualstudio.com. 
   - Double click VS Code icon and open application.
   
 - Select `Open Folder` and navigate to your repository
 - Open a file that ends in `.go`
 - Install the goland extension from https://marketplace.visualstudio.com/items?itemName=golang.Go
 - A small window will open in the bottom right offering to install the Go extension. As you start to write code a lot of these will come up... you might as well let it install  all the helper packages.
