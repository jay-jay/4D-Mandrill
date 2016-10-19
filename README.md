# 4D-Mandrill
Mandrill for 4D (Mailchimp's transactional email service)

####Goodbye SMTP! Easily send emails through REST API

##Usage

```
C_OBJECT($o_params)

OB SET($o_params;"email";"james@mymail.com")
OB SET($o_params;"subject";"James tester")

//choice either or both html and text (advisable: both html and text should be populated to cater all mail clients)
OB SET($o_params;"html";"<h1>Hi</h1><p>This is a mail in html<p>")
//optional
OB SET($o_params;"text";"This is the text body of the mail. A good alternate for mail clients that can't parse html")
// optional (This will disregard html and text. This is an advanced mail sending using Mandrill templates.)
OB SET($o_params;"template_name";"My Mandrill Template")

// Optional 
OB SET($o_params;"from_email";"mail@verified.com") // From mail should be a verified domain in Mandrill or else mail won't send
OB SET($o_params;"from_name";"Beautiful name")
OB SET($o_params;"Reply-To";"") // if empty, from_email will be used instead
OB SET($o_params;"bcc_address";"bccemail@mail.com") // cc is not advisable because all recipients will see each other's email addresses
OB SET($o_params;"attachment_content";$file_in_base64) // use _mndrl_base64_encode to cleanup your base64 file
OB SET($o_params;"attachment_type";"application/pdf")
OB SET($o_params;"attachment_name";"Filename.pdf")

// Dynamic Data in Mandrill Template (A template that handles dynamic data is required)
OB SET($o_params;"merge_language";"handlebars") // default: handlebars (you can use mailchimp merge_language too)
ARRAY OBJECT($ao_global_merge;0)
C_OBJECT($o_global_merge)

// Add First dynamic data
OB SET($o_global_merge;"name";"url_receipt";"content";"http://www.jamesborillo.com/receipt/12345.html")
$a_ref:=OB Copy($o_global_merge)
APPEND TO ARRAY($ao_global_merge;$a_ref)

// Add second dynamic data
OB SET($o_global_merge;"name";"recipient_name";"content";"John Doe")
$a_ref:=OB Copy($o_global_merge)
APPEND TO ARRAY($ao_global_merge;$a_ref)

OB SET ARRAY($o_params;"global_merge_vars";$ao_global_merge)

$sent:=_mndrl_send ($o_params)
```

####Roadmap
- multiple "to" recipients in a single REST request
- multiple attachments
- schedule when to send email (good for marketing)
