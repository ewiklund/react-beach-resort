react-router-dom netlify -- you need a redirect (search on the web)
react-icons https://react-icons.github.io/icons?name=fa
https://reactjs.org/docs/context.html#reactcreatecontext
rfc 
rcc

if you comment out an image in your data.js file; you will not see the picture but instead a "link" to the picture. What we did was:

1) imported a defaultImg in the Room.js: 
import defaultImg from "../images/room-1.jpeg";

2)  declared it in the <img src:
<img src={images[0] || defaultImg} alt="single room"

This way a default picture is going to be displayed !!

https://styled-components.com/

Space ID: t6jo52dhzwr6
Content Delivery API - access token: DXStx9VPgHnDcnftR7Y-k8J0KhPLbGYZ0QwIQ6SK0H4


When you use Contentful; you will need to create an API from Settings -> API keys. Take a note of the Space ID and Content Delivery API - access token. You will need that for your project!

1) run 'npm i contentful' from the terminal of Code
2) create Contentful.js with the following:

import { createClient } from "contentful";

export default createClient({
 space: "t6jo52dhzwr6",
 accessToken: "DXStx9VPgHnDcnftR7Y-k8J0KhPLbGYZ0QwIQ6SK0H4"
});

When you access your website; you'll notice that your code is retrieving data from all content types in Contentful; not just the one we created!! To fix that we did:

3) update context.js with the following to change how we get the data; ie from contentful:

import Client from "./Contentful";
Client.getEntries({
 content_type: "beachResort"
}).then((response) => console.log(response.items));

Note that the content-type is the Content type ID, ie:

the ID to retrieve everything related to this content type via the API.

4) Once you comment out // import items from "./data";

Notice that the ordering of the hotels are not going to be the same. To fix that; do the following:

Add the following line below content_type: "beachResort",
order: 'sys.createdAt'


Then save and you will find the appearance in the correct order.

You can also uncomment the above and instead use:
Order: "fields.price". Or reverse order: "-fields.price"

When you use Contently in your script; you should create an .env file in the project directory (same level as package.json) because of the space and accessToken.

Like so:

REACT_APP_API_SPACE=t6jo52dhzwr6
REACT_APP_ACCESS_TOKEN=DXStx9VPgHnDcnftR7Y-k8J0KhPLbGYZ0QwIQ6SK0H4

Then in the Contentful.js:

export default createClient({
 space: process.env.REACT_APP_API_SPACE,
 accessToken: process.env.REACT_APP_ACCESS_TOKEN
});

Then in the .gitignore file; add .env under # testing

Create a new repository in Github.

Then from the Terminal in Code; run:
git add .
git commit -m "react beach app"
git remote add origin https://github.com/ewiklund/react-beach-resort.git 


Then go to Netlify and click on Create new site from Github
Select Github from next page and select your repository. Then you need to Authorise and at the Create a new site, click on Show Advanced button and enter the same keys and values from the .env file. Then hit Deploy.
 