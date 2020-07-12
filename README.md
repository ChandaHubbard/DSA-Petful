# DSA-Petful
For EI petful project - React, Node, DSA


https://courses.thinkful.com/ei-dsa-v1/checkpoint/11

Data Structure and Algorithms: Full Stack Project
You've been asked to create a site for an animal shelter which allows adoption of cats and dogs. These are the only 2 animals allowed in the shelter. The adoption process works strictly on a "First-In, First-Out" basis. The FIFO is based on the animals that came to the shelter first. People can adopt a cat, or a dog, or both, but they may only adopt the animal that came to the shelter first. In addition, people who want to adopt are also put in a Queue so they can adopt when it's their turn.

Note: In addition to implementing the following user stories, your application should follow the design best practices you have learned up to this point: mobile-first CSS with all content clear and readable on all screen sizes.

See http://uxarchive.com, http://mobile-patterns.com, and http://dribbble.com for layout inspiration.

User stories
USER STORY #1:
As a pet lover, I want to visit the FIFO pet adoption site 
so that I can get more information about the adoption process.

Acceptance criteria

When I go to the FIFO adoption agency site

* I see a description of the adoption process.
* I see a meaningful picture related to the description.
* I see a button for starting the adoption process.
USER STORY #2:
As a user interested in adopting pets, I want to get more information 
on each pet so that I can make an informed decision about who to adopt.

Acceptance criteria

When I visit the adoption page, I can see:

* An image of the pet;
* A physical description of the pet;
* The pet's name, gender, age, and breed.
* A story of the pet's journey to the shelter
USER STORY #3:
As a user interested in adopting pets, 
I want to see the pets that I can adopt.

Acceptance criteria

When I visit the adoption page, I can only see the 
pet that is next in line to be adopted.
USER STORY #4:
As a user interested in adopting pets, I want to get in line to adopt.

Acceptance criteria

When I visit the adoption page:

* I can see a list of other people currently in line.
* I can submit my name and be added to the end of the line.
* When I am not at the beginning of the line, I cannot see an option to adopt a pet.
* For demo purposes: Once I join the line, I can see other pets being adopted until I am at the front of the line.
    * Every five seconds, the user at the front of the line should be removed from the line and one of the pets up for adoption should disappear.
    * When I am at the front of the line, a new user should be added to the line behind me every five seconds until there are a total of five users in line.
USER STORY #5:
As a user interested in adopting pets, I want to adopt a pet.

Acceptance criteria

When I am at the front of the line:

* I can see an option to adopt a pet.
* When I choose to adopt a pet: 
    * I see a confirmation that I have adopted the pet.
    * I see my name removed from the line.
    * I see the pet I adopted is removed from view and replaced with another pet.
Helpful starting point
This app will use 2 distinct repositories: 1 for the client, and 1 for the server.

Create the parent directory for your app on your local machine: mkdir Petful.
Move into the directory: cd Petful.
Set up the client and the server
Clone the server template repository:

git clone https://github.com/tparveen/DSA-Petful.git
Push your changes up to GitHub

Create and test API endpoints
Your app should be able to show us the cat or dog that has been in the shelter the longest, and also be able to remove an animal from the shelter after it has been adopted. This will require GETing the pet information to show and and DELETEing, the pet from the shelter when it is adopted.

Other requirements
Use a Queue data structure that is implemented with either a singly linked list or doubly linked list.
Deploy your client using Vercel
Deploy your server using Heroku
Test the functionality of your code often! Make incremental changes and see that they're working in the browser before you move on.
Apply the same approach to accessibility. Resolve any accessibility warnings your linter generates, and run aXe when you write new markup and styles.
Getting an animal
Add a GET endpoint at api/cat which returns the following cat information as JSON:
{
  imageURL:'https://assets3.thrillist.com/v1/image/2622128/size/tmg-slideshow_l.jpg', 
  imageDescription: 'Orange bengal cat with black stripes lounging on concrete.',
  name: 'Fluffy',
  sex: 'Female',
  age: 2,
  breed: 'Bengal',
  story: 'Thrown on the street'
}
Run the server: npm start.
Go to http://localhost:8080/api/cat and look at your cat!
Now add another GET endpoint at api/dog which returns a dog as JSON. You can use the following information:
{
  imageURL: 'http://www.dogster.com/wp-content/uploads/2015/05/Cute%20dog%20listening%20to%20music%201_1.jpg',
  imageDescription: 'A smiling golden-brown golden retreiver listening to music.',
  name: 'Zeus',
  sex: 'Male',
  age: 3,
  breed: 'Golden Retriever',
  story: 'Owner Passed away'
}
Go to http://localhost:8080/api/dog and say "hi" to your dog!
Helpful hints on deploying your server
DO SOME SERVER-SIDE PREPARATION
Make sure you've added the following to server/index.js:

  app.use(cors({
    origin: CLIENT_ORIGIN
  });
In server/src/config.js, make sure you've exported the following:
module.exports = {
CLIENT_ORIGIN : process.env.CLIENT_ORIGIN || 'http://localhost:3000',
PORT : process.env.PORT || 8080
}
Double-check that your async actions still return your data.

Create the Heroku app: heroku create PROJECT_NAME.

connect your git repo to Heroku’s: heroku git:remote -a PROJECT_NAME

When server is finalized, push your code to Heroku: git push heroku master.

Helpful hints on deploying your client
GET YOUR CLIENT TO VERCEL
Create a vercel.json file in the root directory of your client, containing the following code:
 {
 "version": 2,
 "routes": [
   {
     "src": "^/static/(.*)",
     "dest": "/static/$1"
   },
   {
     "src": "^/favicon.ico$",
     "dest": "/favicon.ico"
   },
   {
     "src": "^/manifest.json$",
     "dest": "/manifest.json"
   },
   {
     "src": "^/site.webmanifest.json$",
     "dest": "/site.webmanifest.json"
   },
   {
     "src": ".*",
     "dest": "/index.html"
   },
 ]
}

Before we can deploy to Vercel, we need to build the client files. Make sure to have a .env file with any global variables needed, like the API url. These env vars must start with: REACT_APP_, or else, react-scripts will ignore them! For instance, in client’s .env file we might have:
REACT_APP_API_BASE=https://SERVER-PROJECT-NAME.herokuapp.com/api
and the config.js file (client) would then read something like:
export default {
REACT_APP_API_BASE: process.env.REACT_APP_API_BASE || “http://localhost:8080/api”
}
Afterwards we can use react-scripts to build our client files so we can then deploy them to Vercel:
npm run build
or
yarn run build
When the build process is done, we can deploy to Vercel:
vercel --prod
Note the URL that Vercel provides for your production build, as you will use it below to configure Heroku.

CONFIGURE THE SERVER ON HEROKU TO ACCEPT REQUESTS FROM THE CLIENT
Add a CLIENT_ORIGIN environment variable to your Heroku app pointing to your deployed client:
heroku config:set CLIENT_ORIGIN=https://CLIENT_PROJECT_NAME.now.sh
Make sure there is no trailing slash!
you can add env vars in Heroku from your account’s dashboard as well.
Run heroku restart (or: Restart All Dynos - from dashboard) to ensure that the app runs with knowledge of the new client origin.
For further details on client deployment go to this checkpoint: https://courses.thinkful.com/ei-react-v1/checkpoint/19

Document your app
Now that all the core features of your app are in place, you should have a pretty good idea of how you would explain the app to a user. Do that! Add some copy to your client's dashboard that gives your app a name and explains what its purpose is and how to use it. You could even put this introductory content into its own component on the dashboard to make it easier to show and hide later.

Both repos in this project should have README.md files.

Put all your team members names on the README.md for both client and server
The client's README should reflect the introduction present in your app, and link to the live app.
Include screenshots if you can!
The server's README should explain how other developers would consume (or use) your API, and provide example requests and responses.
Both READMEs should also explain the tech stacks used in the repo, for the benefit of developers who might want to work on your project.
All members of the team must submit the project for grading
Look beyond deployment
Now that your app is deployed, you have an opportunity to make some improvements.

Bonus Stories:
BONUS STORY #1
As a user interested in adopting pets, I want to see a list of pets that have already been adopted.

Acceptance criteria

When I visit the FIFO adoption agency site:

* I can see a link to view "Success Stories."
* When I click the link:
    * I can see the names and images of pets that have been adopted, along with the names of the people who adopted them.
    * If I have adopted a pet, I see my name in the list along with an name and image of the pet I have adopted.
BONUS STORY #2
As a Petful administrator, I want to see a list of all pets currently up for adoption.

Acceptance criteria

When I visit the FIFO adoption agency site:

* I can see a link to log in.
* When I log in with the correct credentials (which can be hardcoded), I see a Manage Pets page.
* I see a Dogs section and a Cats section which includes the names and pictures of all pets up for adoption.
* When a pet is adopted, I see that the pet is removed from this list.
BONUS STORY #3
As a Petful administrator, I want to put up a pet for adoption.

Acceptance criteria

When I log in to the Manage Pets page;

* I can see a button to add a pet.
* When I click the Add Pet button:
    * I can choose whether the new pet is a Cat or Dog.
    * I can add a name, gender, age, breed, physical description, story, and image for the new pet (all fields required).
* When I submit the information:
    * I can see the new pet added to the correct section (Cats or Dogs) of the Manage Pets page.
    * I can see the new pet come up for adoption on the adoption page.

BONUS STORY #4
As a Petful administrator, I want to remove a pet from the adoption queue.

Acceptance criteria

When I log in to the Manage Pets page;

* Near each pet's picture, I can see a button to remove the pet.
* When I click the Remove Pet button:
    * I can see the new pet removed from the Manage Pets page.
    * I can see the new pet is no longer available for adoption on the adoption page.