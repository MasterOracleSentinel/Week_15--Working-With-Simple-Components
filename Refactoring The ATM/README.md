# Refactoring The ATM
## 1. ATM Improvements Task 1 - Select Refactor
-------------------------------------------------

Adding Features to ATM
Through this week’s videos, you have seen the steps required to implement a basic ATM. Now, it’s your turn to implement 
a few improvements to the same ATM shown in the browser window on the right.

Looking at this implementation, the following are a few short comings:

No input validation: This means that you can make your account balance go negative by withdrawing more money than is 
actually available in the account.

Confusing UI: The Deposit and Cash Back options are right next to each other and there is no difference in the UI other 
than a label above the number input box, it is easy for a user to do the opposite of what they intended.
For the user to toggle between a Deposit UI and a Cash Back UI, you need to change this UI, providing a more clearly 
defined difference between them

Your task in this activity will be to implement two additions to the shown ATM application:

* To provide a multi-choice selection, add a <select> input element below Account Balance which will allow the 
user to switch between Deposit, Cash Back, and a null option. The content below the <select> input will only be shown 
if the atmMode is set to Deposit or Cash Back, but not the third option (i.e., null). The atmMode should be initialized to the 
null option in React.useState().

* Validate the number input such that the Submit button is disabled when you attempt to take out more money than is available in the account.

You can complete these tasks by executing the following steps:

Note: This task will be graded on the functionality of the application. You will have more flexibility on 
implementation and variable names as long as the expected behavior described is present in the application.

1. Add another variable to React state to track the atmMode. This should:
* Be a string variable rather than a Boolean like isDeposit
* Be initialized to "" (empty string)
* Hold either "" (empty string), "Deposit", or "Cash Back" as the three possible transaction modes

2. In the return() function, below the \<"h2"\> element where the value is the status variable, add the following JSX code snippet.

![menu002](https://user-images.githubusercontent.com/105542222/216724008-2e739b02-2e2e-49d2-a796-9888c5ce2671.png)
  
This must be copied exactly for this activity to be evaluated correctly. Note the following characteristics about this code block:
  
* The values for each option are "", "Deposit", and "Cash Back"
* The ids on the \<select\> and \<option\> elements should not be changed in this example
* onChange sends the event to a function called handleModeSelect; you will need to create this function in a later step
 
3. Create a function after handleSubmit called handleModeSelect, which takes the change event as an input. It will then:

* Set the React state variable you created to be the event.target.value, where event would be the name of the function parameter passed in by the onChange in the \<select\> element added in Step 2
* write logic which takes that same event.target.value, which should be either "", "Deposit", or "Cash Back", and sets the isDeposit state value using the existing setIsDeposit() setter function. No change is needed in the isDeposit value if the event.target.value is an empty string. For the other two possible values, you should be able to figure out which value it should be set to.

4. Remove the Deposit and Cash Back buttons from your JSX template. You no longer need them , because you set the isDeposit value in the handleModeSelect function.

5. Create conditional rendering for the number input and submit fields. This means that they will not even show on the page before the user has selected an action (Deposit or Cash Back). To conditionally render a \<div\>\</div\>, you would simply have a variable that is either truthy or falsy and use it in your JSX like the following example:

![menu001](https://user-images.githubusercontent.com/105542222/216723700-a3764801-38e2-40c5-b379-d9cf33284cfa.png)
  
You will do the same except with your newly created atmMode variable and the remaining \<ATMDeposit\>\</ATMDeposit\> element. After this step, there should be nothing showing below the \<select\> element if there is no mode selected.

After this step, you can test out the ATM after your refactor to ensure it is working as expected. If something is not working, check your work by adding console logs in the various handler functions. Simple tests you could do would be ensuring when you’ve selected the Deposit mode, inputted the number 5, and pressed Submit. Following this, the account balance will increase by $5. Same with the Cash Back mode but the account balance will decrease by $5.


## 2. ATM Improvements Task 2 - Input Validation 
-------------------------------------------------

Now that you have refactored the ATM to use a \<select\> field rather than the Deposit and Cash Back buttons, you can now implement the functional improvement mentioned above, i.e., input validation.

1. Add a variable to React state to track whether the transaction is valid. For the scope of this activity, the only transactions considered 
invalid will be a Cash Back transaction, where the inputted number exceeds the current account balance.
Add the following line underneath the other React.useState() function calls:

![menu003](https://user-images.githubusercontent.com/105542222/216740474-37973973-2b2c-4607-94b4-df7d7c2a7b0a.png)

2. Note that initially, validTransaction will be set to false
Send the value of validTransaction to the \<ATMDeposit\> component as a parameter

3. Prevent an invalid value from being submitted to \<ATMDeposit\>

* On the declaration of the \<ATMDeposit\> component, use object destructuring to add a prop called isValid
* In the \<ATMDeposit\> component JSX, add a disabled HTML attribute on the submit input element
* Use isValid to set the disabled attribute
* In the implementation of the \<ATMDeposit\> component, use the return value of setValidTransaction to set the value of the isValid prop

Hint: You can use a logical NOT (!) to turn a true value into a false value.

4. Add logic to the handleChange() function to check the validity of the form.

* Execute setValidTransaction(false) and return if the event.target.value is less than or equal to 0
* If the atmMode is Cash Back and the event.target.value is greater than totalState, execute setValidTransaction(false), otherwise execute setValidTransaction(true) to allow form submission

Your ATM improvements are now complete. To test the functionality of your code, go to the next page.
-----------------------------------------------

## 3. Testing the Work
The following test cases should have the specified results. You can run through these before submitting to ensure you’ve covered everything.

Test 1: Refresh browser -> Select Deposit -> Enter 10 -> Select Submit
Result 1: Submit button should be enabled and Account Balance should show $10.

Test 2: Refresh browser -> Select Cash Back -> Enter 10
Result 2: Submit button should be disabled.

Test 3: Refresh browser -> Select nothing
Result 3: The following should be all that is showing with the conditional rendering:

![image](https://user-images.githubusercontent.com/105542222/216740668-64685a9b-a66c-4950-965a-0d82218ce5bd.png)

Test 4: Refresh browser -> Select Deposit -> Enter 100 -> Press Submit -> Press Submit again -> Change mode to Cash Back -> Change input value to 50 -> Press Submit
Result 4: Account Balance should now show $150.
In the same way, this activity looks at the existing ATM app, identifies improvements, and implements them. What would your own improvements to this version be?

Hints:

* Your variable names don’t need to exactly match the examples. Feel free to name them any way you like as long as you correctly access them to create the functionality described.

* If you get stuck and something isn’t working, be sure to put in console.logs to check what values are actually stored in the variables.

* To check whether the inputted number field is greater than totalState, remember to change it to number type by doing Number(event.target.value). This will allow you to use math operators such as > or < on it.

![task_menu001](https://user-images.githubusercontent.com/105542222/216740865-a6132a3f-2a93-4010-bc9f-ebe29a8b272a.png)


![task_menu002](https://user-images.githubusercontent.com/105542222/216740812-6ab55172-6ad1-49fe-adad-9d61bdec3b29.png)


