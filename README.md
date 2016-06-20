# 4D-Mandrill
Mandrill for 4D (Mailchimp's transactional email service)

####Goodbye SMTP! Easily send emails through REST API

##Usage

C_OBJECT($o_params)

OB SET($o_params;"email";"james@lex.no")
OB SET($o_params;"subject";"James tester")

  // choice either or both html and text (advisable: both should populated to cater all mail clients)
  //OB SET($o_params;"html";"```<h1>Hi</h1><p>James tester mandrill komponent. This is the body<p>```")
  // optional
  //OB SET($o_params;"text";"James tester mandrill komponent. This is the body")
  // optional (This will disregard html and text. This is an advanced mail sending using Mandrill templates.)
  // OB SET($o_params;"template_name";"Pedlex Faktura Epost")

  // Optional 
  //OB SET($o_params;"from_email";"it@lex.no")
  //OB SET($o_params;"from_name";"Pedlex IT")
  //OB SET($o_params;"merge_language";$Filnavn+".pdf")
  //OB SET($o_params;"Reply-To";"")
  //OB SET($o_params;"bcc_address";"regnskap@pedlex.no")
  //OB SET($o_params;"attachment_content";$file_in_base64)
  //OB SET($o_params;"attachment_type";"application/pdf")
  //OB SET($o_params;"attachment_name";$Filnavn+".pdf")

$sent:=_mndrl_send ($o_params)
