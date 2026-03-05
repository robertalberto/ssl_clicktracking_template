## what is the template for?
Use this template to test the CDN configuration of your tracking domain—the mechanism supporting analytics for links within your emails. Common redirection issues typically result from an improper configuration between the CDN hosting the tracking domain and its associated SSL certificates or DNS CNAME records. These misconfigurations often cause users to receive a "connection is not secure" privacy error or a 404 failure after clicking a tracked email link.

### Key concepts

* A **Tracked URL** wraps the original HTTPS link in your tracking domain. When a user clicks it, the tracking domain resolves the request and redirects to the final destination. A CDN allows you to track secure (HTTPS) URLs; without it, users may encounter a "connection is not secure" privacy error.
* An **Untracked URL** maintains the original URL intact, bypassing the CDN to serve as a control environment.

> Note: This template uses "example.com" as the destination URL. To test your own links and tracking domain, simply replace the URL in the capture tag located on line 117. For instance, "https://example.com" becomes "https://braze.com/blog". After replacing your link, use the Preview & Test function to send an email to yourself. Click each button below to observe the link redirect behavior.


## Example of a Broken CDN configuration
![broken](brokencdn.gif)

## Example of a Working CDN configuration
![working](working_cdn_config.gif)


## How do I use the template
1. **Get the Code:** Click this [link](https://raw.githubusercontent.com/robertalberto/ssl_clicktracking_template/refs/heads/main/template.html) to open the raw HTML from the template.html file.
2. **Import to Braze:** Copy the HTML and paste it into a Braze HTML Email campaign.
3. **Configure your URL*:** This template uses example.com as the default destination. To test your own links and tracking domain, simply replace the URL in the capture tag located on line 117.
   1. For instance: replace "https://example.com" with "https://braze.com/blog".
4. **Test:** Use the Preview & Test function to send a test email to yourself and click both buttons.
5. **Verify:** The expected behavior and success criteria are described within the template itself.


## How do I troubleshoot results
* If your Untracked URL works but your Tracked URL fails, you likely have a configuration gap. To troubleshoot, refer to the documentation for your specific ESP and CDN provider:
  * ESP Documentation: SparkPost, SendGrid, or Amazon SES.
  * CDN Documentation: Cloudflare, AWS CloudFront, Akamai, etc.
  * Braze Resources: Review the SSL at Braze Guide for detailed requirements on certificate provisioning.

### Common errors

| Browser error/status code                                            | Likely cause                 | General Recommendation                                                                                                    |
| -------------------------------------------------------------------- | ---------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| "Your connection is not private" (NET::ERR_CERT_COMMON_NAME_INVALID) | SSL Certificate Mismatch     | Verify that your SSL certificate                                                                                          |
| "This site can’t be reached" (DNS_PROBE_FINISHED_NXDOMAIN)           | CNAME Misconfiguration       | Check your DNS settings. Ensure your tracking sub-domain is configured per your CDN and ESP recommended configuration     |
| 525 / 526 SSL Error (Cloudflare)                                     | Origin SSL Handshake Failure | Ensure the SSL setting in your CDN (like Cloudflare) matches your Origin's capability                                     |
| 404 Not Found                                                        | Path Masking / Routing Issue | Ensure your CDN is configured to forward the entire URL path to the ESP, rather than just hitting a blank root directory. |

> Note: The recommendations here are generic because every CDN is unique. If you encounter persistent issues, the best resource for help is your CDN’s support team, as these configurations take place outside of the Braze ecosystem.
