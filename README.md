This architecture enables dynamic functionality for static websites without traditional server management, handling form processing, AI integration, and email communication seamlessly in the cloud. The serverless contact form solution follows these steps:

A static contact form on the website initiates the process.

When a visitor submits the form, it sends an HTTP POST request to Amazon API Gateway.

API Gateway receives this request and invokes the AWS Lambda function.

The Lambda function, the core of the solution:
-Processes the form data
-Contains a pre-defined prompt for inspirational quote generation
-Invokes the Amazon Bedrock API with this prompt
-Amazon Bedrock processes the prompt and generates a unique inspirational quote.

The Lambda function then:
-Receives the response from the Bedrock API
-Initiates the email-sending process using Amazon Simple Email Service (SES)
-Amazon SES handles the email delivery:

-Sends a notification email to the website owner
-Sends a confirmation email, including the inspirational quote, to the website visitor

Key Components
AWS Lambda: Core logic for data processing and service orchestration
Amazon API Gateway: RESTful API endpoint for the contact form
Amazon Bedrock: AI service for generating inspirational quotes
Amazon SES: Email delivery service

---
lambda_test_event.json

{
  "body": "{\"name\":\"John Doe\",\"email\":\"your.email@example.com\",\"message\":\"This is a test message.\"}"
}

---
main.js

		// Contact form handling
            var $contact = $('#contact');
            var $form = $contact.find('form');
            var $submit = $form.find('input[type="submit"]');

            $form.submit(function(event) {
                event.preventDefault();

                // Disable submit button (using template's existing disabled class)
                $submit.addClass('disabled');

                // Send data asynchronously
                $.ajax({
                    url: "YOUR_API_ENDPOINT_HERE",
                    type: "POST",
                    data: JSON.stringify(Object.fromEntries(new FormData($form[0]))),
                    contentType: "application/json",
                    success: function(result) {
                        $form.find('.response').remove();
                        $form.append('<div class="response success">Message sent successfully!</div>');
                        $form[0].reset();

                        // Close the form after 3 seconds using template's hash navigation
                        setTimeout(function() {
                            location.hash = '';
                        }, 3000);
                    },
                    error: function(error) {
                        $form.find('.response').remove();
                        $form.append('<div class="response error">There was an error sending your message. Please try again.</div>');
                    },
                    complete: function() {
                        // Re-enable submit button
                        $submit.removeClass('disabled');
                    }
                });
            });

            ---
lambda_test_event.json
     {
  "body": "{\"name\":\"John Doe\",\"email\":\"your.email@example.com\",\"message\":\"This is a test message.\"}"
}
	    ---
template.py
  def generate_quote_prompt():
    """
    Generates a strict template for requesting concise and original quotes from an AI model.

    Returns:
    str: A formatted string containing the prompt template for generating quotes.
    """
    # Define the template string
    template = """
    Provide a concise, original, and engaging quote about life, success, or personal growth.

    Important:
    1. Respond with ONLY the quote text.
    2. Do NOT include any phrases like 'Here is...' or meta-descriptions of the quote.
    3. The quote should be thoughtful, impactful, and limited to 2 sentences.
    4. Begin the response directly with the quote itself.
    """
    return template
    #Notes

    # 1. This template is designed for use with AI language models.
    # 2. It provides clear instructions to generate a standalone quote.
    # 3. The output is easy to extract and use without additional processing.

    # CUSTOMIZATION:
    # - To change the theme: 
    #   Replace "life, success, or personal growth" with your desired topic.
    #   Example: "technology, innovation, or artificial intelligence."

    # - To adjust the style:
    #   Add style instructions in the "Important" section.
    #   Example: "5. The quote should have a positive tone."

    # - To specify an audience:
    #   Add audience information in the "Important" section.
    #   Example: "5. The quote should be suitable for a professional audience."

  P2C self service portal: https://youtu.be/dxiRs0VYRwQ

  https://excalidraw.com/#json=Otvz3TfI_191OiiZf51pR,fzWswIP69p0BvRxTnkB2hw
  
  https://readme.so
  
 <img width="1325" height="807" alt="p2c" src="https://github.com/user-attachments/assets/33099d65-b5af-4c93-9a1b-5c779e1375e4" />

