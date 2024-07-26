# free-cookie-consent
How to Display Cookie Consent Banner for EU users, Free and Unlimited

A cookie consent banner is essential for complying with privacy laws such as the GDPR in Europe. This article provides a simple and effective way to create a cookie consent banner using HTML, CSS, and JavaScript. The solution is free and unlimited, meaning it can be used on any number of websites without restrictions.

Step-by-Step Implementation
1. Adding the HTML and CSS
First, you need to create the HTML structure and style the cookie consent banner. Here is the code:

<code><pre>
<style>
#CookieNotice {
    background: #444;
    color: #fff;
    padding: 6px;
    font-size: 13px;
    text-align: center;
    position: fixed;
    bottom: 0;
    width: 100%;
    z-index: 10;
}
</style>
<div id="CookieNotice"></div>
</pre></code>

This code creates a fixed banner at the bottom of the page with a dark background and white text.

2. Adding the JavaScript
The JavaScript code is responsible for displaying the banner based on the user's location and managing cookie consent. Here's the code:

<code><pre>
<script>
var endpoint = 'https://apip.cc/json';
var xhr = new XMLHttpRequest();
xhr.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
        var response = JSON.parse(this.responseText);
        if(response.status !== 'success') {
            console.log('Query failed: ' + response.message);
            return;
        }
        var xcookie = document.getElementById('CookieNotice');
        switch(response.ContinentCode) {
            case "EU":
                xcookie.innerHTML = 'We value your privacy. We use cookies to enhance your browsing experience, serve personalized ads or content, and analyze our traffic. By clicking this notice, you consent to our use of cookies.';
                break;
            default:
                xcookie.innerHTML = '<style>#CookieNotice {display:none}</style>';
        }
    }
};
xhr.open('GET', endpoint, true);
xhr.send();
</script>
</pre></code>


This script sends a request to a free API to determine the user's location. If the user is in Europe, it displays the cookie consent message. Otherwise, it hides the banner.

3. Managing Cookie Consent
To manage cookie consent and ensure the banner doesn't reappear once the user has consented, add the following JavaScript:

<code><pre>
<script>
// Function to set a cookie
function setCookie(name, value, days) {
    let expires = "";
    if (days) {
        const date = new Date();
        date.setTime(date.getTime() + (days * 24 * 60 * 60 * 1000));
        expires = "; expires=" + date.toUTCString();
    }
    document.cookie = name + "=" + (value || "") + expires + "; path=/";
}
// Function to get a cookie
function getCookie(name) {
    const nameEQ = name + "=";
    const ca = document.cookie.split(';');
    for(let i = 0; i < ca.length; i++) {
        let c = ca[i];
        while (c.charAt(0) == ' ') c = c.substring(1, c.length);
        if (c.indexOf(nameEQ) == 0) return c.substring(nameEQ.length, c.length);
    }
    return null;
}
// Check if the cookie exists on page load
window.onload = function() {
    if (getCookie('OkCookie') === 'clicked') {
        document.getElementById('CookieNotice').style.display = 'none';
    }
};
// Add event listener to the div
document.getElementById('CookieNotice').addEventListener('click', function() {
    // Set a cookie named 'OkCookie' with the value 'clicked' that expires in 7 days
    setCookie('OkCookie', 'clicked', 7);
    // Hide the div after it is clicked
    this.style.display = 'none';
    //alert('Cookie has been set and the div is now hidden for 7 days!');
});
</script>
</pre></code>


This code handles setting and retrieving cookies to check if the user has already consented. If they have, the banner is hidden on subsequent visits.

How It Works
HTML and CSS: Create a fixed banner at the bottom of the page.
JavaScript for Location Detection: Uses an API to check if the user is in Europe and displays the banner if they are.
Cookie Management: Sets a cookie when the user clicks the banner, hiding it for 7 days.
Conclusion
This implementation provides a straightforward, free, and unlimited way to display a cookie consent banner. By integrating this code into your website, you can ensure compliance with privacy laws and improve user experience.


<p>Source: <a href="https://apip.cc/display-cookie-banner-consent-eu-free-unlimited.html">How to Display Cookie Consent Banner for EU users, Free and Unlimited</a></p>
