# Puzzler 007: Paging List with Load More

**Description:**

This exercise challenges you to implement a screen that displays a paginated list of items. Users can load additional pages by clicking a "Load More" button.

**Problem Specification:**

* Create a screen that displays a list of items.
* Initially, only the first page of items is loaded.
* Implement a "Load More" button at the bottom of the list.
* Clicking the "Load More" button fetches the next page of items from the ViewModel using a Flow.
* Update the list to display all loaded items from all pages.
* Handle potential errors during data fetching and display appropriate messages.

**Focus:**

* Understanding how to use Flows for paginated data loading.
* Managing state for multiple pages of data in the ViewModel.
* Updating the UI incrementally as new pages are loaded.

**Implementation:**

1. **ViewModel:**
    * Define a Flow that fetches a page of items based on a page number.
    * Maintain a state variable to store the currently loaded pages and their data.
    * Update the state and emit new data from the Flow upon successful page loading.
    * Handle errors appropriately and update the state accordingly.
2. **Screen:**
    * Observe the Flow emitted by the ViewModel using `viewModel.dataState.collectAsState()`.
    * Based on the observed state:
        * Display the loaded items in a list.
        * If more pages are available, show the "Load More" button.
        * Display an error message if any errors occur during loading.
    * Clicking the "Load More" button triggers fetching the next page through the ViewModel.

**Additional Notes:**

* Consider using libraries like Paging3 or Coil for efficient paging and image loading.
* Implement proper error handling and retry mechanisms for failed requests.
* You can display loading indicators or progress bars while fetching new pages.

**Challenge:**

* Implement infinite scrolling functionality where new pages are loaded automatically as the user scrolls down the list.
* Display loading indicators for each individual page being fetched.

