## Puzzler 009: Chat Application with Live Updates

**Description:**

This exercise challenges you to develop a simple chat application that simulates real-time message updates using Flows.

**Problem Specification:**

* Create two screens:
    * **Chat Screen:** Displays a list of received messages and a text field for sending new messages.
    * **Send Message Screen:** Allows users to compose and send a new message.
* Implement a Flow in the ViewModel that simulates receiving messages at regular intervals (e.g., every 2 seconds).
* The Chat Screen should observe the Flow and update the message list dynamically as new messages arrive.
* Clicking the "Send" button on the Send Message Screen should trigger a new message emission in the Flow, simulating sending a message.
* Consider implementing basic user identification for each message (e.g., sender name).

**Focus:**

* Understanding how to use Flows for real-time data updates.
* Implementing asynchronous communication channels between screens using a shared Flow.
* Updating UI components dynamically based on Flow emissions.

**Implementation:**

1. **ViewModel:**
    * Define a Flow that emits new messages at regular intervals using `delay` and `emit`.
    * Include message content and sender information in each emitted message object.
    * Implement a function to handle sending a new message, adding it to the Flow.
2. **Chat Screen:**
    * Observe the Flow emitted by the ViewModel using `viewModel.messages.collectAsState()`.
    * Maintain a list of received messages in the composable state.
    * Update the message list whenever a new message is emitted from the Flow.
    * Display the message content and sender information for each message.
3. **Send Message Screen:**
    * Allow users to compose a new message in a text field.
    * Upon clicking "Send", trigger the send message function in the ViewModel, passing the composed message.

**Additional Notes:**

* You can use libraries like Coroutines or RxJava for managing asynchronous operations.
* Consider implementing user interface elements for refreshing the chat list or handling potential errors.
* Explore advanced techniques like debouncing user input for sending messages.

**Challenge:**

* Implement user authentication and differentiate messages based on the sender.
* Allow users to see typing indicators when another user is composing a message.

By completing this exercise, you'll gain practical experience with using Flows for real-time communication and updating UI elements dynamically in response to asynchronous data streams.
