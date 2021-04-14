## Team 5
- Work on iterator functionalities, iterator filter, styling the app, create login page, login/logout function

- Iterator functionalites:
	- Warn: there will be some confusions because we use a mockup batch template and iteration template, and we linked their relationship using batch id. All of the select box of the iterator component use batch template. The iterator only use to send to the database, and loop through to not allow duplication of the same project to the same batch 
	- The select box had its own component. It uses @Output decorator with Event Emitter to pass value to its parent
	- The batches in Filter and select component was get from a batch mock database. 
	- When click send iterator, the batch id, start date and end date was stored into an Interator object together with the selected project from mat form material element and send to the backend
	- The iterator array was get using a httpget request at OnInit life cycle hook. If there is no iterator from the backend, it will immiadiately send. If there is any Iteration in the array. 
	- If the selected project id not equal to the selected Iterator project Id, and the selected batchId from batch object equal to iteration object batchId, the new Iterator will be sent
	- If the batchId from the batch template is not in the Iterator array, we can also send a new iterator to the backend.
	- Everytime we success, it'll show a success message. If not, it'll send an error message to notify the user.

- Iterator filter:
	- The view page used Mat Form, it was actually not a material we familiar of, we add a function in the iterator filter mat form field in the view page template and in its component.ts, we pass the batchValue Id as a MatSelectChange event and get it using eventName.value. 
	- We then loop through all Iteration, get the iteration with the batch id that match the selected batch Id, get their project field and cast its type to project, then put put them to a MatTableDataSource object and the related project was displayed

- Styling the app:
	- Our group did a lot of styling for the application too
	- Not only we use Bootstrap, we add a lot of re-useable css code following Bootstrap like btn-orange, float-left, pointer, bg-orange
	- We also use root element to to create global variable like the orange color and the font. We used it in our pre-define css class, as well as across the template. All of the font + orange color we used in all the app can be changed with just a simple update in style.css :root --orange value or --rev-font value

- Create login page:
	- We update the styling for the login page, do the functionality and add a template driven form there
	- If the user haven't touch the input, the submit btn disabled and the error will appeared when user hover it
	- If the user not meet the requirement, the error will appeared there pernamently, until the user give the correct input
	- When successfully login, the login btn will change from login to logout, and the user got redirect to the main page. If not, there will be an error mesage showing up

- Login Logout function:
	- When the user succesfully login, we pass their data to the Session Storage
	- The key was used using the environment.ts so it easy to manage when there's a lot of function use that key to interact with the session.
	- Then we create a login service that use that environment variable to check if user account was in the session or not. 
	- We inject that service as public to use it in the navbar template and use *ngIf to toggle between Login/Logout button
	- For the logout, we use that environment variable to remove the user account in the session