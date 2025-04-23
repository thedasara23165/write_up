Reflected XSS in HTML Context - Challenge Write-Up
Introduction
Welcome to the Reflected XSS in HTML Context challenge in the "XSS Basics" room (https://tryhackme.com/jr/xssbasics)! This challenge introduces you to Reflected Cross-Site Scripting (XSS), a common web vulnerability where attackers inject malicious scripts into a web page that are then executed in a victim’s browser. Your task is to identify and exploit this vulnerability in a web application’s search feature to capture a hidden flag, learning the risks of XSS along the way.
In this lab, the HTML context lacks proper encoding, making it vulnerable to script injection.
Challenge Setup
The challenge features a basic web application with a search functionality on a page (e.g., search.php). The search feature fails to sanitize user input, resulting in a Reflected XSS vulnerability. When a user submits a search query, the input is reflected directly into the HTML response, allowing script execution. Your goal is to exploit this to retrieve the hidden flag.
Objective

Locate the Reflected XSS vulnerability in the search feature.
Inject a JavaScript payload to trigger an alert box.
Use the vulnerability to extract the hidden flag.

Step-by-Step Solution
Step 1: Inspect the Web Application
Access the web application’s search page (e.g., search.php) via the "XSS Basics" room interface. Find the search input field and test it with a harmless query, such as "hello". Submit the form and observe the response. You’ll see the input reflected in the HTML, for example: <div>Results for: hello</div>. This indicates the input is directly embedded in the page.
Step 2: Inject a Basic XSS Payload
Since the search input is reflected without sanitization, exploit this by injecting a simple XSS payload. In the search field, enter:<script>alert('XSS')</script>Submit the query. If the vulnerability is present, a pop-up alert box will display "XSS", confirming that the Reflected XSS vulnerability can be exploited.
Step 3: Capture the Flag
With the vulnerability confirmed, extract the hidden flag, which is typically stored in the session or cookie. Use a payload to access the cookie:<script>alert(document.cookie)</script>Enter this into the search field and submit. The resulting alert box will show the cookie contents, including the flag, in the format: FLAG{xss_basics_reflected_123}. For example, the alert might display: session=xyz; flag=FLAG{xss_basics_reflected_123}.
Example Output
After injecting the second payload, the alert box will show:FLAG{xss_basics_reflected_123}
Remediation
Preventing Reflected XSS in real-world applications is critical. Here are key mitigation strategies:  

Input Validation: Sanitize user input by rejecting or escaping special characters like <, >, and &.  
Output Encoding: Encode input before rendering in HTML, converting < to < to prevent script execution.  
Content Security Policy (CSP): Use CSP headers to block inline scripts, e.g., Content-Security-Policy: script-src 'self';.  
Use Secure Frameworks: Opt for frameworks like React or Angular, which automatically handle sanitization of inputs and outputs.

Conclusion
This challenge illustrates the dangers of Reflected XSS vulnerabilities, where unsanitized user input in a search feature allows attackers to execute malicious scripts in a victim’s browser. By implementing input validation, output encoding, and security headers like CSP, developers can significantly reduce the risk of XSS attacks. Well done on completing this challenge and advancing your understanding of web security!
References

OWASP XSS Prevention Cheat Sheet  
Mozilla Developer Network (MDN) - Cross-Site Scripting (XSS)

