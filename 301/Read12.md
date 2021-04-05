# Partials
We use partials when we want to have the same **HTML** page across multiple views, such as when dealing with *nav* and *footer*, we usually don't need to change them at every page of our website. To do so, we need to create an **EJS** file for *nav* and another one for the *footer*,for example with nav:
```
<div class="header">
    <nav>
        <ul>
            <li><a href="/">Home</a></li>
        </ul>
    </nav>
</div>    
```
footer:
```
<footer>
    <p> copyright ASAC 2021 </p>
</footer>   
```
and then we need to include them in our pages as the following example:
```
<%- include ('partials/footer') %>
```
inside the page we need to include in.
