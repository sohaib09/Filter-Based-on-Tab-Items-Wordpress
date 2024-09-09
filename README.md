**Dropdown Item Storage and Redirect**
This project involves storing the name of a selected dropdown item in localStorage and then redirecting to a specific page. Upon reaching the redirected page, the script retrieves the stored item name and uses it to trigger a click on a corresponding tab element. The following sections describe the implementation details and usage of the project.

**Overview**
Store Dropdown Item: When a user clicks on an item in a dropdown menu, the item's text content is stored in localStorage, and the user is redirected to the education page.
Retrieve and Act on Stored Item: On the redirected page, the script retrieves the stored item name and triggers a click on a tab element that matches the stored name.
Implementation


**1. Storing Dropdown Item**
This script listens for clicks on dropdown items within a specific menu and performs the following actions:

Prevents the default link behavior.
Stores the clicked item's text content in localStorage.
Redirects the user to the specified education page.
document.addEventListener('DOMContentLoaded', function () {
    // Add click event listener to dropdown items
    document.querySelectorAll('.wordpress_menu_css #menu-1-303dcee .elementor-nav-menu--dropdown li a').forEach(function (item) {
        item.addEventListener('click', function (e) {
            e.preventDefault(); // Prevent default link behavior

            // Store the clicked item value in localStorage
            let dropdownItemName = e.target.textContent.trim();
            localStorage.setItem('dropdown_item_name', dropdownItemName);

            // Debugging: check if the localStorage is being set
            console.log('Dropdown item name stored:', dropdownItemName);

            // Redirect to the education page
            window.location.href = 'https://ifarmag.ca/education/';
        });
    });
});


**2. Retrieving and Acting on Stored Item**
Upon loading the education page, this script:

Retrieves the stored item name from localStorage.
Finds and clicks on the tab element whose title matches the stored item name.
Adds a class to the matched item for visual feedback and clears the stored item from localStorage.
document.addEventListener('DOMContentLoaded', function () {
    // Retrieve the stored dropdown item name from localStorage
    const storedItemName = localStorage.getItem('dropdown_item_name');

    if (storedItemName) {
        // Debugging: Check what value was retrieved
        console.log('Stored item name:', storedItemName);

        // Add a delay to ensure the elements are fully loaded
        setTimeout(() => {
            // Find all tab elements on the page
            const items = document.querySelectorAll('#uc_ue_buttons_post_filter_elementor_3062a31 .ue_taxonomy_item');

            let found = false;
            items.forEach(function (item) {
                // Get the text of the title within the tab
                const tabTitle = item.querySelector('.ue_taxonomy_item_content .ue_taxonomy_item_title')?.textContent.trim();

                // Debugging: Check each tab's title
                console.log('Tab Title:', tabTitle);

                // Check if the stored item matches the tab title
                if (storedItemName === tabTitle) {
                    console.log("Values Matched:", tabTitle);
                    found = true;

                    // Trigger a click on the .ue_taxonomy_item
                    item.click();

                    // Optionally, add a class to the matching item
                    item.classList.add('uc-selected');

                    // Clear the stored item after processing
                    localStorage.removeItem('dropdown_item_name');

                    // Exit the loop after finding the match
                    return;
                }
            });

            // If no match is found, log that the values didn't match
            if (!found) {
                console.log("Value Not Found");
            }
        }, 1000); // Delay to ensure elements are loaded
    } else {
        console.log("No item stored in localStorage.");
    }
});

**Usage**
**Deploy the Script:** Ensure both scripts are included in your web page. The first script should be on the page with the dropdown menu, and the second script should be on the education page.
**Test Functionality:** Click on a dropdown item and verify that you are redirected to the education page and that the correct tab is clicked.
**Debugging**
Check the console logs to verify that the dropdown item names are correctly stored and retrieved.
Ensure that the delay in the second script is sufficient for all elements to load.
**Notes**
Adjust the selectors and URLs in the scripts according to your specific setup.
Ensure cross-page functionality by including the correct script files on the relevant pages.
