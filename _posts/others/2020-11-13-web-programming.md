---
layout: post
mathjax: true
title: "Web programming- Foundations!"
read: 20
secondary: others
date: 2020-11-12
---

*This post is written from what I studied in [Web Programming Foundation](https://www.linkedin.com/learning/web-programming-foundations/welcome?u=2127121)*

## 1. Deconstruct the Web

Website loads the browser, you can read, view or listen to the content. What really happens?

**Step 5:** We keep spliting data into smaller until:
+ Reach min number of samples in a node

+ Gini impurity does not improve

+ Reach maximum depth allowed for tree

a. **Address bar**:
* Filled with a URL
 A locator following a universal standard that points a specific resource on the web and that resource is the document you are trying to access. Besides, that resource is a server connected to the internet and its IP address is mapped to the domain you used in a DNS 
  
b. Process

Enter URL in the address bar -> User hit Return 

-> The browser sends a get request to this URL and asks the server to send back all the data it has to the browser. 

// (parallel)

-> The URL is sent to DNS and DNS figures out which IP address domain points at and passes the request to the server on that IP address

c. Resources
+ Resource received by the browser is in HTML (HTML is document for the worldwide web).
+ In HTML, it contains all content of pages, references to media, image, audio.
+ It also contain links to CSS (contain instructions on how the content is displayed on the browser) and JavaScript (small programs that run in the browsers)

Finally, the browser puts HTML, CSS and JavaScript together

## 2. Parts that make up the Web
- HTML: for content
- CSS: for style
- JavaScript: for interactivity

a. HTML
- Core markup language 
- Be the documents in the browser
- Traditionally, web document was built on static web: meaning if we build a site with 100 pages, and want to update, we have to update independently all of pages. 
- Nowadays, move from static web development to dynamic web applications. Developer creates templates outlining HTML structure -> server/browser combines these templates with data from a database to create the final document -> No longer a unique document for each page -> A change in a single file or in database can apply to all or any subset of documents.
- In HTML, each piece of element is wrapped in a beginning and an end tag, creating an HTML element
- Each of these elements is a DOM's node and the browser handles each of them as independent object -> CSS applies style property to each item independently. 

![](/sources/Others-web-programming3.png){:height="60%" width="60%"}

b. CSS
- Provide instructions on how elements in a document should be styled
- We can supply CSS either in line HTML or as an external reference style sheet -> new CSS rules override what the browser provides.
- Rules are applied from the top of style sheet down

c. JavaScript
- JavaScript: add interactivity on the top of CSS ad HTML. It interacts with DOM by manipulating DOM nodes.  

d. Process of HTML, CSS, JavaScript
User enter URL -> Browser pulls down the HTML document -> download CSS and JavaScript references: first run JavaScript to see if any of the HTML markup has changed, then applies CSS, finally leave JavaScript run

e. DOM tree behind website

Here is an example of boxes on the website

![](/sources/Others-web-programming.png){:height="60%" width="60%"}

Behind these boxes are elements that are organized into DOM (document object model) as this below photo.

![](/sources/Others-web-programming2.png){:height="60%" width="60%"}

- DOM is the browser's model for the document displayed
- Each element of HTML document is a leaf or node, and connections are branches. 
- When you add a new element to HTML document, you are adding a node to this DOM tree.
- When you target elements using CS or JavaScript, you ask the browser follow DOM tree from the root to the node ...
- In HTML, each piece of element is wrapped in a beginning and an end tag, creating an HTML element
- Each of these elements is a DOM's node and the browser handles each of them as independent object -> CSS applies style property to each item independently. 

**Example**: When document is loaded into the browser, the browser creates a node tree, modeling the relationships between different HTML elements or nodes. In a standard HTML, you will have an HTML object containing 2 objects (head and body)

![](/sources/Others-web-programming4.png){:height="60%" width="60%"}

These nodes are in turn in a strict hierarchical relationships, depend on how they are nested in the HTML. For example, a link in menue is a node nested in *li*, *li* is nested in *ul*, *ul* is nested in *nav* and so on.

![](/sources/Others-web-programming5.png){:height="60%" width="60%"}

f. Events
- Anything happens in a browser, an event is triggered. Example, click the link, open the browser, hit an enter, move the mouse...
- Use JavaScript to respond these events
- Event handling:
  -  First, identify the DOM node the interactive behavior is attached to
  -  Second, identify the event you want to detect and bind that event to the DOM node. 
  -  Third, create a function to run when the event is triggered

## 3. Put all together

![](/sources/Others-web-programming6.png){:height="60%" width="60%"}

HTML markup describes the document and identify each object using tag -> These tags are turned into nodes on DOM tree -> JavaScript targets these nodes to change them and apply interactivity to them -> CSS rules target these nodes to apply style to them -> Events are triggered when user performs some sort of behavior at which point the HTML, CSS and DOM tree may get changed. 

## 4. Tools
- Code editor like Visual studio code
- Browser developer tools (interact with live site on the browser)
- Browser like Google Chrome (edit or manipulate code directly in the browser develop tools)
- Run from your computer, directly in your browser is not as the same as running an HTML document on web server because many features will not work => Need a local web server 
- Set up local web server: by setting up a virtual machine or full-web server using tools like Vagrant or WampServer...For a small project, we can use some extensions (eg. Live Server) of visual studio code to spin up a small and local server environment that sync code editor and the browser. "Live Server" extension performs exactly as a live server somewhere on the web. This extension is good because when you change in code editor, the server updates and forces the browser to immediately reload. 
  