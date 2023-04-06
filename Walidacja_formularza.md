# Walidacja formularza


HTML5 adds some attributes that allow form validation. For example, the required attribute can be added to an input field to make it mandatory to fill in.

More complex form validation can be done using JavaScript.

The form element has an onsubmit event that can be handled to perform validation.

For example, let's create a form with two inputs and one button. The text in both fields should be the same and not blank to pass the validation.

<form onsubmit="return validate()" method="post">
  Number: <input type="text" name="num1" id="num1" />
  <br />
  Repeat: <input type="text" name="num2" id="num2" />
  <br />
  <input type="submit" value="Submit" />
</form>
