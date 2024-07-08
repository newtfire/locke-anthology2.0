<h1>Documentation</h1>

<h2> How to Run </h2>
This site requires the use of Node and Eleventy

### [Instaling Node](https://nodejs.org/en/learn/getting-started/how-to-install-nodejs):

- To run the site you first need to download node, which can be done at this link: https://nodejs.org/en/download

### [Instaling Eleventy](https://www.11ty.dev/docs/):
 
 - Once node is installed you must run these node commands: 

`npm init -y `

- This installs the package.json that Eleventy requires

`npm install @11ty/eleventy --save-dev`

- This installs Eleventy itself on the project

`npx @11ty/eleventy`

- This is used to run Eleventy

- If everything was successful you should see this after running eleventy

`
npx @11ty/eleventy
[11ty] Wrote 0 files in 0.03 seconds (v2.0.1)
`
### Generating Poem HTML Files:

- The poems are generating by running the poemHtml.xsl file in an XML editor such as Oxygen
- This file can be ran over any of the poem TEI files, and it will run over the entire collection
- The poem HTML files will be generated in the Poems folder in the Source folder

### Populating Poem Attributes:

- Running poemData.js will create the poemAttributes.json file inside the data folder
- This file contains the title, author, file path, and potential art for each poem file
- variables from this file or any other file in the data folder can be simply be retrieved by using the variable name, 
  with no need to call the file itself 


<h2> Changes between version 1 and version 2 </h2>

- The main difference between the two versions of the sites is
 that it is now being made with Eleventy/11ty.
- Another major change to the site is way the poems are displayed.
 Poems can now be filtered based on the author, and can be viewed beside
 the original book.

### Eleventy:

- One of the main advantages of Eleventy is its flexibility. 
It doesn't impose any specific structure or conventions on your project, 
allowing you to organize your files however you want. 
This makes it great for both simple and complex projects.

- Eleventy also supports various templating languages, including Nunjucks. 
Nunjucks is a powerful templating language that allows you to create reusable 
templates and include dynamic content in your HTML files. With Nunjucks, you can 
create layouts, which are like templates for your entire site or specific sections of it. 
Layouts help maintain consistency across your site by allowing you to define common elements 
like headers, footers, and navigation menus in one place and reuse them across multiple pages.

<h2>Poems Page:</h2>

### HTML Structure:

- **Author Buttons Section (`#authorButtons`):**
    - This section dynamically generates buttons for each author listed in the authors variable. Each button is labeled with the author's name.
    - The onclick attribute of each button is set to call the filterPoems(authorName) JavaScript function with the corresponding author's name as an argument.


- **Archive Iframe Container (`#archiveIframeContainer`):**
    - This container holds an iframe element (#archiveIframe) that displays content from the Internet Archive.
    - Initially, the iframe's source is set to a default URL. However, it gets updated dynamically based on the author selected by the user.

- **Poem Collection (`#poemCollection`):**
    - This section dynamically displays individual poems on the webpage. Each poem is represented by a div element with the class poem.
    - The data-author and data-page attributes of each poem div store the author's name and the page number where the poem can be found, respectively.

### JavaScript Functions:

1. **`iframeUrl(authorName)` Function:**
    - This function updates the source URL of the iframe based on the selected author's name.
    - It iterates through all the poems (div elements with the class poem) displayed on the page.
    - For each poem associated with the selected author, it extracts the page number and compares it to find the lowest page number.
    - If a valid page number is found, it constructs a URL for the Internet Archive containing the corresponding page number and updates the iframe's source to display that page.

2. **`filterPoems(authorName)` Function:**
    - This function filters poems based on the selected author's name.
    - It iterates through all the poems displayed on the page.
    - If a poem's author matches the selected author, it sets the poem's display style to 'block', making it visible. Otherwise, it sets the display style to 'none', hiding the poem.
    -  After filtering the poems, it calls the iframeUrl(authorName) function to update the iframe content based on the selected author.

### Interaction with JSON Data:

- The JavaScript code interacts with JSON data containing poem attributes such as title, author, page, and file path.
- Each poem object in the JSON data contributes to dynamically populating the webpage with poem information.

### Author Button sorting using Author.js

- This code creates a set of unique author names (authorsSet) by mapping over the poemAttributes array and extracting the author attribute.
- It then converts the set into an array (authors) and maps over it to transform author names with underscores into names with spaces.
- Authors are sorted alphabetically based on their last names using the sort() method and the localeCompare() function.
- The sorted authors array is returned, which is then used to generate buttons for each author in the HTML.

### Display the Poem HTML files using poemDisplay.js

- This code iterates over each poem in the poemAttributes array and reads the content of its corresponding HTML file.
- It constructs the file path to each HTML file using the filePath attribute of each poem.
- The fs.readFileSync() function is used to synchronously read the content of each HTML file.
- The content of each HTML file is added to the poem object using the spread operator (...poem) along with the content key.
- The modified poem objects, now containing the content of their respective HTML files, are returned as an array.
