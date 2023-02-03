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

2. In the return() function, below the "<h2>" element where the value is the status variable, add the following JSX code snippet.

![menu001](https://user-images.githubusercontent.com/105542222/216723700-a3764801-38e2-40c5-b379-d9cf33284cfa.png)

  
This must be copied exactly for this activity to be evaluated correctly. Note the following characteristics about this code block:
  
* The values for each option are "", "Deposit", and "Cash Back"
* The ids on the <select> and <option> elements should not be changed in this example
* onChange sends the event to a function called handleModeSelect; you will need to create this function in a later step
 
3. Create a function after handleSubmit called handleModeSelect, which takes the change event as an input. It will then:

* Set the React state variable you created to be the event.target.value, where event would be the name of the function parameter passed in by the onChange in the <select> element added in Step 2
* write logic which takes that same event.target.value, which should be either "", "Deposit", or "Cash Back", and sets the isDeposit state value using the existing setIsDeposit() setter function. No change is needed in the isDeposit value if the event.target.value is an empty string. For the other two possible values, you should be able to figure out which value it should be set to.

4. Remove the Deposit and Cash Back buttons from your JSX template. You no longer need them , because you set the isDeposit value in the handleModeSelect function.

5. Create conditional rendering for the number input and submit fields. This means that they will not even show on the page before the user has selected an action (Deposit or Cash Back). To conditionally render a <div></div>, you would simply have a variable that is either truthy or falsy and use it in your JSX like the following example:

![image](https://user-images.githubusercontent.com/105542222/216723386-aa59a0a5-e96e-4929-9679-68e600a82b63.png)
  
You will do the same except with your newly created atmMode variable and the remaining <ATMDeposit></ATMDeposit> element. After this step, there should be nothing showing below the <select> element if there is no mode selected.

After this step, you can test out the ATM after your refactor to ensure it is working as expected. If something is not working, check your work by adding console logs in the various handler functions. Simple tests you could do would be ensuring when you’ve selected the Deposit mode, inputted the number 5, and pressed Submit. Following this, the account balance will increase by $5. Same with the Cash Back mode but the account balance will decrease by $5.
