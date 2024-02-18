# Puzzler 003: Network Request with Loading State

## Description

This exercise challenges you to implement a screen that fetches data from an API using a Flow in the ViewModel. While fetching data, display a loading indicator. Upon successful retrieval, show the fetched data. If an error occurs, display an appropriate error message.

## Problem Specification:

* Create a screen with a button labeled "Fetch Data".
* Clicking the button triggers a network request using a Flow in the ViewModel.
* While fetching data, display a progress indicator or loading animation.
* If the data is fetched successfully, update the UI to display the retrieved information.
* If an error occurs during the network request, display an error message to the user.
* Use appropriate error handling mechanisms to catch potential exceptions.

## Focus:

* Understanding how to use Flows for asynchronous operations like network requests.
* Managing different emission states (loading, success, error) in the UI based on Flow values.
* Implementing error handling for network requests.

## Implementation:

1. **ViewModel:**
    * Define a Flow that fetches data from the API upon receiving a trigger (e.g., button click).
    * Use appropriate libraries or methods for making the network request.
    * Emit different states from the Flow based on the request outcome:
        * Loading state while fetching data.
        * Success state containing the fetched data.
        * Error state with an exception object.
2. **Screen:**
    * Observe the Flow emitted by the ViewModel using `viewModel.dataState.collectAsState()`.
    * Based on the observed state:
        * If loading, display a progress indicator.
        * If success, update the UI to display the fetched data.
        * If error, display an error message to the user.

**Additional Notes:**

* You can use libraries like [Retrofit](https://square.github.io/retrofit/) or [Volley](https://google.github.io/volley/) for making network requests.
* Consider using sealed classes or data classes to represent different emission states in the Flow.
* Implement proper error handling and display user-friendly error messages.

**Challenge:**

* Implement a retry mechanism for failed network requests.
* Display additional information like loading progress percentage or remaining time.
