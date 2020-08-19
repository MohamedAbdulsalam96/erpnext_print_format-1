# Creating beautiful print formats in ERPNext.

ERPNext is a beautiful software and many organizations use it. And print formats are really important to organizations as hardcopy of every document with their letterhead is a core requirement. Recreating their template in ERPNext is an art and not easy.

I’ll break down the process to make it easy for all the beginners.

ERPNext uses Jinja templating for this purpose. I’m not going to give you a deep explanatory course on Jinja, but the basics that you’ll need for a neat, aesthetic template.

When the client gives you their existing template, you should make a thorough observation of it.
First off, we split the template into 3 parts: Above, Middle and Below.
1. Above: The above part includes all the static items in the page including the letter head, the customer details and the head of the table(if any).

2. Middle: This part consists of recurring things in the template. Eg: the rows in the table.

3. Bottom: This part consists of static items in the bottom half of the template, including the footer of the table, other calculations and footer of the template.

Now that we have divided the template into three parts. It becomes fairly easier for us to do things and also makes the code look beautiful(you’ll understand how as you keep reading).
We will now use macros for the above and bottom sections/parts. Macros are pieces of code defined by a name. And hence, you can call them just by that name whenever you need them(like functions).
Here is how you define a macro:
```
{% macro name_of_macro() %}
	<p>Hi</p>
{% endmacro %}
```

Now, you can refer to that macro anywhere(below its declaration) with:
```{{ name_of_macro() }}```

Each time you call it, the code inside of it replaces it.
```
	<p>Test</p>			>		<p>Test</p> 
	{{ name_of_macro() }}		>		<p>Hi</p>
	<p>Again test</p>		>		<p>Again test</p>
	{{ name_of_macro() }}		>		<p>Hi</p>
	<p>Finish</p>			>		<p>Finish</p>
```

First off, we recreate the the whole template in html with the help of bootstrap.
Here is a basic example:
```
<div class="container-fluid">
	<div class="row d-flex align-items-end justify-content-between" style="padding-top: 10px; font-size: 13px">
        	<div class="col-xs-12">
            		Dear Sir/Madam,<br>
            		Thank you for placing the purchase order. We hearby confirm our acceptance as follows:
        	</div>
    	</div>
</div>
```
Using **col-xs** is necessary as anything else will cause wkhtmltopdf to break and the the generated PDF will loose its alignment, although the print version will look fine. Intendation is also very important as if increases the readablity of the code and when working as a team, it gives a great advantage.

Now that you have converted the basic template into html format, its time for us to use Jinja to fetch value into our format.
The format for it is ```{{ name of variable to print }}```
