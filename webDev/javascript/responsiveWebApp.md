# responsive web app

A responsive web app is one that doesn't need (as much as possible) to refresh or redirect to update the webpage when operations occur such as getting, posting, updating, or deleting resources. 

One good example is **twitter**. When you tweet (post), your tweet is automatically added to the news feed without refreshing the page. When you scroll down till there are no more posts, more posts are added below the already loaded ones. It retrieves data from the server and adds those dynamically in the DOM tree.

Remember that HTML files are basically hypertext media that has a markdown for displaying information and links to other files. PHP files contain server-side code that runs on the server and renders the HTML that will be sent to the client browser. To make a webpage **feel like an app**, we need JavaScript; a *client-side* programming language.

### traditional webpage
```html
<form class="postingForm" method="post" action="/home/actionpost.php">
    <textarea name="postContent" required="true">
    </textarea>

    <button type="submit" name="submit">
        POST</button>
</form>
```

This is non-responsive. When we press the `<button>`, the client sends an http `POST` request to `server/home/actionpost.php` with the `$_POST` superglobal containing `postContent` key with the value of whatever is inside the `<textarea>`.

### responsive webpage
Here is a responsive version of the above:
```html
<div id="postingForm">
        <textarea id="postingForm_content" required="true">
        </textarea>
    <button id="postButton">POST</button>
</div>
```

```javascript

setInterval( () => {
    /* Some code to send an API GET request */
    /* Some code to process the request response*/
},1000);

document.getElementById("postButton").onclick = () => {

    let textarea = document.getElementById("postingForm_content");

    /* Some code to send an API POST request with body */
    textarea.value = "";
}
```

Check my example [@DanesZalor/php-blog](https://github.com/DanesZalor/php-blog).

It's a long process but what you need is:
- API endpoints in your server to send/retrieve json data
    ```php
    function respond($data, int $responseCode){
        header('Content-Type: application/json', true, $responseCode);
        echo json_encode($data);
    }
    ```
- a function for sending http requests
    - You can use `XMLHttpRequest`
    ```javascript
    let request = new XMLHttpRequest();
    request.open(method, url);
    request.send(JSON.stringify(objectBody));

    request.onload = functionToHandleOnLoad;
    ```
    - or [`fetch()`](https://javascript.info/fetch)
    - or make your own with *Promises* 