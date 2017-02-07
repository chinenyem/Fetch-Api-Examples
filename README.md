# Fetch-Api-Examples

MDN (Mozzila Developers Network) Technical defintion:

The Fetch API provides a JavaScript interface for accessing and manipulating parts of the HTTP pipeline, such as requests and responses. It also provides a global fetch() method that provides an easy, logical way to fetch resources asynchronously across the network.

When calling the  Fetch API and passing it the URL we defined as a constant above and since no more parameters are set this is a simple GET request. Then we get a response but the response we get is not JSON but an object with a series of methods we can use depending on what we want to do with the information, these methods include:

- clone() - As the method implies this method creates a clone of the response.
- redirect() - This method creates a new response but with a different URL.
- arrayBuffer() - In here we return a promise that resolves with an ArrayBuffer.
- formData() - Also returns a promise but one that resolves with FormData object.
- blob() - This is one resolves with a Blob.
- text() - In this case it resolves with a string.
- json() - Lastly we have the method to that resolves the promise with JSON.

json() example

 const ul = document.getElementById('authors');
    const url = 'https://randomuser.me/api/?results=10';
    let li, img, span;

    function createNode(element){
        return document.createElement(element);
    }

    function append(parent, el){
        return parent.appendChild(el);
    }


    //json() - Lastly we have the method to that resolves the promise with JSON.
    fetch(url)
        .then((resp) => resp.json())
        .then(function(data){
            let authors = data.results // Get the results
            console.log(authors)
            return authors.map(function(author){ // Map through the results and for each run the code below
                    li = createNode('li'),
                   img = createNode('img'),
                   span = createNode('span');
                   
               img.src = author.picture.medium; // Add the source of the image to be the src of the img element
               span.innerHTML = `${author.name.first} ${author.name.last}`; //Make the HTML of our span to be the first and last name
               console.log(span.innerHTML)
               console.log(img)
               
                append(li, img); // Append all our elements
                append(li, span) ;
               //if (ul != null ) { append(ul, li);}
                $('ul#authors').append(li)
              
            })
        })
        .catch(function(error){
            console.log(error)
        });



