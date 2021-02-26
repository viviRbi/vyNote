# HTML

### Definition
- HTML stands for HyperText Markup Language. It is used to structure content on a webpage.
- CSS stands for Cascading Style Sheets. It is a style sheet language used for describing the presentation of a document written in a markup language such as HTML
### DOCTYPE html
- Doctype is not a tag. It is an instruction (directive) to the browser about what version of HTML the page is written in.
- It must be the very first non-comment line declared within our Html documents.

### Body
Contains info/content that will be displayed to the user when rendered by the browser

### HTML tags/ elements
- Used to indicate how content should be displayed
- Usually they required an opening and closing tag. Those that do not require a closing tag are called self-closing tags
- Some of the html tags: h1->h6, div, img, a hr, br, input

### White space in HTML
HTML does not care about white space, we use ```<br/>``` to make a line break and escape character ```\&nbsp;``` for space

### Escape characters
Escape characters are Microsoft specific, and are reserved for control characters. In HTML, they are undefined and in XHTML, they are invalid. To use them, we need to use their escape character equivalents.
| Escape character | Their eqivalents | Their meaning |
| :------------ |:--------------- | :--------------- | 
| < | \&lt; | less than |
| > | \&gt; | more than |
| & | \&amp; | ampersand |
| " | \&quot; | quote |
|   | \&nbsp;| Space |

### Structural vs Sematic markup
- **Structural Markup** are used to present the content itself with no extra information. Ex: div, p, ul li, br, sub, i, strong (subscribtion)
- **Semantic Markup** provide extra information, which means the name of the tag indicate where to use the content. Ex: h1, blockquote, q, abbr (abbreviations), s (strike-through text), section, main, code, em, dfn (use for definition of a word)
- Ex of abbr: ``` <abbr title="Cascading Style Sheet">CSS</abbr> ```

### Lists 
There are 3 diferent type of lists:
- **Order list ol** : lists where each item numbered. Ex: 1 2 3, A B C, I II III, i ii iii.
- **Unordered lists ul**: Lists where each item had some bullet points.
- **Defination lists**: Lists made up of terms <dt> and defination <dd>. Ex:
``` html
<dl>
	<dt>Ordered List</dt>
	<dd>A list where each item is numbered</dd>

	<dt> Unorder list </dt>
	<dd>A list where each item has a bullet point</dd>

	<!-- And so on with defination lists -->
</dl>
```
### img
- Use to add an image to a web page. It is a self-closing tag. - 
- It is an inline element
- Its attribute: 
	- src : path to the image file (local or external) ex: ```<img src="../img-folder/abc.png" alt="An image" /> ```
	- alt : provide text description if the image do not load
	- title : Use to provide info when hover over the image
	- width, height, align (desprecate, hurts SEO) 
- <img> cross site scripting: ```<img src="fakelink-sdhgjksdhfjk.com" onerror="console.log('You have been hacked.  Please pay me 1 BTC');">```

### iframe
- iFrame is short for inline frame
- An iFrame is like a little window places on webpage. The term is short for inline frame
- Ex of google map: ```<iframe src="https://www.google.com/maps/embed?pb=!1m18!!5m2!1sen!2sus" width="600" height="450" style="border: 6px;" allowfullscreen="" loading="lazy"></iframe>```
- Ex of youtube clip: ```<iframe width="800" height="315" src="https://www.youtube.com/embed/t2ByLmLnYJ8" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>```

### Table
```html
<table>
<thead>
	<tr>
		<th>Table header 1: First name</th>
		<th>Table header 2: Last name</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>Vy</td>
		<td>Le</td>
	</tr>
	<tr>
		<td>Thanh</td>
		<td>Le</td>
	</tr>
</tbody>
</table>
```
### Form
- The form will take input from visitors then post it to the backend application
- Action attribute: Make a request to this website. Ex: ``` <form action="http:///www.example.com">```
- Method: type of the request (Get, Post). Ex: 
``` html
<form action="http:///www.example.com" method="GET">
	<input placeholder='search for keyword'/> 
	<input type='submit'/>
</form>
```
- Elements that used in form: form, fieldset, legend, label, input (type=radio, type=checkbox, type=hidden, type=submit), select - option, textarea 
