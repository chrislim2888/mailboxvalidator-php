MailboxValidator PHP Module
===========================

This PHP module provides an easy way to call the MailboxValidator API which validates if an email address is a valid one.

This module can be used in many types of projects such as:

 - validating a user's email during sign up
 - cleaning your mailing list prior to an email marketing campaign
 - a form of fraud check


Installation Using PHP Composer
===============================

Add the following to your composer.json file:

```
"require": {
	"mailboxvalidator/mailboxvalidator-php": "1.1.*"
}
```


Dependencies
============

An API key is required for this module to function.

Go to https://www.mailboxvalidator.com/plans#api to sign up for FREE API plan and you'll be given an API key.


Usage for validating emails
===========================

```php
<?php
require_once __DIR__ . '/vendor/autoload.php';

use MailboxValidator\SingleValidation;

$mbv = new SingleValidation('PASTE_YOUR_API_KEY_HERE');

$results = $mbv->ValidateEmail('example@example.com');

if ($results === false) {
	echo "Error connecting to API.\n";
}
else if (trim($results->error_code) == '') {
	echo 'email_address = ' . $results->email_address . "\n";
	echo 'domain = ' . $results->domain . "\n";
	echo 'is_free = ' . $results->is_free . "\n";
	echo 'is_syntax = ' . $results->is_syntax . "\n";
	echo 'is_domain = ' . $results->is_domain . "\n";
	echo 'is_smtp = ' . $results->is_smtp . "\n";
	echo 'is_verified = ' . $results->is_verified . "\n";
	echo 'is_server_down = ' . $results->is_server_down . "\n";
	echo 'is_greylisted = ' . $results->is_greylisted . "\n";
	echo 'is_disposable = ' . $results->is_disposable . "\n";
	echo 'is_suppressed = ' . $results->is_suppressed . "\n";
	echo 'is_role = ' . $results->is_role . "\n";
	echo 'is_high_risk = ' . $results->is_high_risk . "\n";
	echo 'is_catchall = ' . $results->is_catchall . "\n";
	echo 'mailboxvalidator_score = ' . $results->mailboxvalidator_score . "\n";
	echo 'time_taken = ' . $results->time_taken . "\n";
	echo 'status = ' . $results->status . "\n";
	echo 'credits_available = ' . $results->credits_available . "\n";
}
else {
	echo 'error_code = ' . $results->error_code . "\n";
	echo 'error_message = ' . $results->error_message . "\n";
}
?>
```

Functions
=========

### SingleValidation(api_key)

Creates a new instance of the MailboxValidator object with the API key.

### ValidateEmail(email_address)

Performs email validation on the supplied email address.

Result Fields
=============

### email_address

The input email address.

### domain

The domain of the email address.

### is_free

Whether the email address is from a free email provider like Gmail or Hotmail.

Return values: True, False

### is_syntax

Whether the email address is syntactically correct.

Return values: True, False

### is_domain

Whether the email address has a valid MX record in its DNS entries.

Return values: True, False, -&nbsp;&nbsp;&nbsp;(- means not applicable)

### is_smtp

Whether the mail servers specified in the MX records are responding to connections.

Return values: True, False, -&nbsp;&nbsp;&nbsp;(- means not applicable)

### is_verified

Whether the mail server confirms that the email address actually exist.

Return values: True, False, -&nbsp;&nbsp;&nbsp;(- means not applicable)

### is_server_down

Whether the mail server is currently down or unresponsive.

Return values: True, False, -&nbsp;&nbsp;&nbsp;(- means not applicable)

### is_greylisted

Whether the mail server employs greylisting where an email has to be sent a second time at a later time.

Return values: True, False, -&nbsp;&nbsp;&nbsp;(- means not applicable)

### is_disposable

Whether the email address is a temporary one from a disposable email provider.

Return values: True, False, -&nbsp;&nbsp;&nbsp;(- means not applicable)

### is_suppressed

Whether the email address is in our blacklist.

Return values: True, False, -&nbsp;&nbsp;&nbsp;(- means not applicable)

### is_role

Whether the email address is a role-based email address like admin@example.net or webmaster@example.net.

Return values: True, False, -&nbsp;&nbsp;&nbsp;(- means not applicable)

### is_high_risk

Whether the email address contains high risk keywords.

Return values: True, False, -&nbsp;&nbsp;&nbsp;(- means not applicable)

### is_catchall

Whether the email address is a catch-all address.

Return values: True, False, Unknown, -&nbsp;&nbsp;&nbsp;(- means not applicable)

### mailboxvalidator_score

Email address reputation score.

Score > 0.70 means good; score > 0.40 means fair; score <= 0.40 means poor.

### time_taken

The time taken to get the results in seconds.

### status

Whether our system think the email address is valid based on all the previous fields.

Return values: True, False

### credits_available

The number of credits left to perform validations.

### error_code

The error code if there is any error. See error table below.

### error_message

The error message if there is any error. See error table below.


Usage for checking if an email is from a disposable email provider
==================================================================

```php
<?php
require_once __DIR__ . '/vendor/autoload.php';

use MailboxValidator\SingleValidation;

$mbv = new SingleValidation('PASTE_YOUR_API_KEY_HERE');

$results = $mbv->DisposableEmail('example@example.com');

if ($results === false) {
	echo "Error connecting to API.\n";
}
else if (trim($results->error_code) == '') {
	echo 'email_address = ' . $results->email_address . "\n";
	echo 'is_disposable = ' . $results->is_disposable . "\n";
	echo 'credits_available = ' . $results->credits_available . "\n";
}
else {
	echo 'error_code = ' . $results->error_code . "\n";
	echo 'error_message = ' . $results->error_message . "\n";
}
?>
```

Functions
=========

### SingleValidation(api_key)

Creates a new instance of the MailboxValidator object with the API key.

### DisposableEmail(email_address)

Check if the supplied email address is from a disposable email provider.

Result Fields
=============

### email_address

The input email address.

### is_disposable

Whether the email address is a temporary one from a disposable email provider.

Return values: True, False

### credits_available

The number of credits left to perform validations.

### error_code

The error code if there is any error. See error table below.

### error_message

The error message if there is any error. See error table below.


Usage for checking if an email is from a free email provider
============================================================

```php
<?php
require_once __DIR__ . '/vendor/autoload.php';

use MailboxValidator\SingleValidation;

$mbv = new SingleValidation('PASTE_YOUR_API_KEY_HERE');

$results = $mbv->FreeEmail('example@example.com');

if ($results === false) {
	echo "Error connecting to API.\n";
}
else if (trim($results->error_code) == '') {
	echo 'email_address = ' . $results->email_address . "\n";
	echo 'is_free = ' . $results->is_free . "\n";
	echo 'credits_available = ' . $results->credits_available . "\n";
}
else {
	echo 'error_code = ' . $results->error_code . "\n";
	echo 'error_message = ' . $results->error_message . "\n";
}
?>
```

Functions
=========

### SingleValidation(api_key)

Creates a new instance of the MailboxValidator object with the API key.

### FreeEmail(email_address)

Check if the supplied email address is from a free email provider.

Result Fields
=============

### email_address

The input email address.

### is_free

Whether the email address is from a free email provider like Gmail or Hotmail.

Return values: True, False

### credits_available

The number of credits left to perform validations.

### error_code

The error code if there is any error. See error table below.

### error_message

The error message if there is any error. See error table below.


Errors
======

| error_code | error_message |
| ---------- | ------------- |
| 100 | Missing parameter. |
| 101 | API key not found. |
| 102 | API key disabled. |
| 103 | API key expired. |
| 104 | Insufficient credits. |
| 105 | Unknown error. |

Copyright
=========

Copyright (C) 2018 by MailboxValidator.com, support@mailboxvalidator.com
