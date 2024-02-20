# Puzzler 005: Debounced Search

## Description:

This exercise challenges you to implement a search bar that provides suggestions based on user input. However, you want to avoid overwhelming the server with frequent requests for every keystroke. Therefore, you'll implement a debouncing mechanism using Flows.

## Problem Specification

* Create a screen with a search bar for entering text.
* As the user types, capture the input using TextField composable.
* Implement a debouncing mechanism using Flow:
    * After each keystroke, emit the current input to a Flow.
    * Introduce a delay (e.g., 500 milliseconds) before considering the latest input for making a search suggestion request.
    * If a new keystroke arrives before the delay finishes, cancel the previous emission and wait for the new input to complete the delay.
* Upon receiving a debounced input, trigger a network request to fetch search suggestions.
* Display the retrieved suggestions as a list below the search bar.

## Focus:

* Understanding the concept of debouncing in asynchronous operations.
* Implementing debouncing logic using Flow operators like `debounce` and `conflate`.
* Handling user input and triggering network requests based on debounced values.

## Implementation

1. **ViewModel:**
    * Define a Flow that captures user input from the TextField.
    * Use the `debounce` operator with a specified delay to emit only the latest input after the delay finishes.
    * Use the `conflateLatest` operator to ensure only the most recent debounced value is emitted if multiple keystrokes occur within the delay window.
    * Trigger a network request based on the debounced input to fetch suggestions.
2. **Screen:**
    * Observe the Flow of suggestions emitted by the ViewModel.
    * Update the UI to display the received suggestions as a list.

## Additional Notes

* You can use libraries like Retrofit or Volley for making network requests.
* Consider using a data class to represent search suggestions.
* Implement proper error handling and display user-friendly messages in case of network issues.

## Challenge

* Implement a mechanism to clear the suggestions list when the search bar is empty.
* Enhance the UI to display loading indicators while fetching suggestions.

