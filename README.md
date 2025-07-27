# Customer Registration Automation via Selenium and IP Management Script

**Customer Registration and IP Management Script**

This project automates the process of registering new customers into a web-based AAA (Authentication, Authorization, Accounting) system using Selenium WebDriver and Python. Additionally, it handles the assignment of IP addresses from a pool stored in an Excel workbook and updates the pool with newly assigned IPs.

It includes functionality to:

Assign IP addresses (automatically or manually)

Parse and format customer data

Generate secure PPPoE passwords

Interact with a browser to input data into the AAA web interface

Maintain and update an Excel-based IP address pool

**What is AAA?**

AAA stands for:

Authentication – Verifies the identity of a user (e.g., using username and password).

Authorization – Determines what resources or services a user is permitted to access.

Accounting – Logs user activity for billing or auditing purposes.

In ISP or telecom environments, AAA systems manage customer sessions for services like broadband or PPPoE internet. This script automates new account registration on such systems.

## Features
- **Browser Automation**: Uses Selenium WebDriver to automate browser interactions for customer registration.
- **IP Address Assignment**: Automatically or manually assigns IP addresses to customers based on a workbook and updates the pool.
- **Password Generation**: Generates a secure password based on customer details.
- **Phone Number Standardization**: Converts raw phone numbers into an international format (e.g., +91).
- **Excel Integration**: Updates the IP pool workbook with new customer information.

## Requirements
Ensure you have Python installed on your system.
### Libraries
This project requires the following Python libraries:
- `selenium`
- `openpyxl`
- `ipaddress`
- `re`

Install the required libraries using `pip`:

`pip install selenium openpyxl ipaddress`

### ChromeDriver
You'll need ChromeDriver to run Selenium with the Chrome browser. Download it from https://developer.chrome.com/docs/chromedriver/ and place it in your system's PATH or specify its location in the script (`driver_path`).

## How to Use
### 1. Setup Configuration
- Ensure that you have **ChromeDriver** installed.
- Specify the correct path to ChromeDriver in the `configure_browser()` function (variable: `driver_path`).
- Update the path to your IP pool Excel workbook in the `workbook_path` variable.

### 2. Customize Customer Details
- Modify the `customer_ID`, `name`, `raw_phone`, and `city` variables in the `main` function to match the customer details you wish to register.

### 3. Choose IP Assignment Method
- Set the `IP_assignment_method` to either `'auto'` or `'manual'`.
  - In `'auto'` mode, the script fetches the next available IP from the Excel workbook.
  - In `'manual'` mode, the IP is hardcoded to `192.168.1.15`.

### 4. Run the Script
Execute the script using the following command:
`python customer_registration.py`
This will:

- Automatically assign an IP address.
- Register the customer in the "AAA system" via the browser.
- Update the IP pool workbook with the new IP address.

### 5. Script Output
- The script will register the customer, including details such as:
  - Customer ID.
  - First Name
  - Last Name
  - Phone Number (in international format)
  - City
  - Assigned IP Address
  - Generated Password
- It will also update the IP pool workbook with the new IP address.

## Functions
`configure_browser()`
Configures and returns a Selenium Chrome WebDriver instance with the necessary options for debugging.

`get_next_ip_address(ip_assignment_method, workbook_path)`
Fetches the next available IP address from the Excel workbook if the assignment method is 'auto', otherwise returns a hardcoded IP for 'manual' method.

`parse_customer_name(name)`
Parses the full name of the customer into a first and last name.

`standardize_phone_number(raw_phone)`
Standardizes the phone number into an international format (e.g., +91 for India).

`generate_password(customer_ID, name)`
Generates a secure password based on the customer’s ID and name.

`register_customer(browser, customer_details)`
Uses Selenium to automate the process of registering the customer in the "AAA system."

`update_ip_pool(ip_assignment_method, workbook_path, next_ip, customer_ID)`
Updates the IP pool Excel workbook with the newly assigned IP address if the assignment method is 'auto'.

## Example
### Example Customer Details:
> customer_ID = 11223
> 
> name = 'John Doe'
>
> raw_phone = '0123456789'
>
> city = 'Dubai'
>
> IP_assignment_method = 'auto'
>
> workbook_path = r"C:/path/to/your/IP pool/IP Updated.xlsx"``

### Output:
1. Customer is registered on the "AAA system" with the following details:
- Username: 11223
- Password: Generated based on the name and ID.
- Phone Number: +91 123456789
- IP Address: 192.168.1.100 (next available IP from the workbook)
2. IP pool workbook is updated with the new IP.

## Notes
- The script assumes that the "AAA system" registration form is structured with specific ID fields (username, password, etc.). Modify the field identifiers as per the actual form you're automating.
- Ensure the Excel workbook is structured correctly with the IP addresses and relevant columns.
- Use proper error handling and testing before deploying for production use.
