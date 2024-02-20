# Puzzler 004: User Input Validation with Real-time Feedback

## Description

This exercise challenges you to implement a screen with a text field where users enter their name. As the user types, validate the name length in real-time using a Flow in the ViewModel. Provide instant feedback to the user based on the validation status.

## Problem Specification

* Create a screen with a text field for entering a name.
* Implement a Flow in the ViewModel that observes the text field input changes.
* Validate the name length in the Flow based on a minimum requirement (e.g., 3 characters).
* Based on the validation result, emit different states from the Flow:
    * Valid: If the name meets the length requirement.
    * Invalid: If the name is too short.
* The screen should observe the Flow and update the UI in real-time:
    * Display the entered name.
    * Change the text field background color or display an error message based on the validation state.

## Focus:

* Understanding how to combine Flow with composable state (e.g., TextField value) for validation.
* Providing real-time feedback to the user based on input changes.

## Implementation Notes

1. **ViewModel:**
    * Define a Flow that transforms the text field value updates.
    * Use a debounce operator to avoid excessive emissions for every character change.
    * Validate the name length within the Flow and emit either `Valid` or `Invalid` state.
2. **Screen:**
    * Observe the Flow emitted by the ViewModel using `viewModel.nameState.collectAsState()`.
    * Bind the text field value to a composable state variable.
    * Update the UI based on the observed state:
        * Display the entered name.
        * Change the text field background color (e.g., green for valid, red for invalid).
        * Optionally, display an error message for invalid names.

## Additional Notes

* You can use libraries like DebounceFlow from kotlinx-coroutines-core for debouncing emissions.
* Consider using different UI elements like error text or icons for visual feedback.

## Challenge

* Implement additional validation rules like checking for special characters or spaces.
* Provide more informative error messages based on the specific validation failure.

