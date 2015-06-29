[![Build Status](https://travis-ci.org/fullybaked/pslackr.svg?branch=master)](https://travis-ci.org/fullybaked/pslackr) [![Code Climate](https://codeclimate.com/github/fullybaked/pslackr/badges/gpa.svg)](https://codeclimate.com/github/fullybaked/pslackr)

# pslackr [slak-er]

pSlackr is a library for integrating Slack.com's inbound web hook
into your application enabling you to send messages to your group
chat channels from your application

## Installing 

Via [Composer][1]

```
composer require fullybaked/pslackr
composer update
```

### Slack API Token

Pslackr uses the old style of sending the token with the request to Slack, so to find the correct token go to your inbound web hook on Slack and you should see 

```
https://hooks.slack.com/services/A111AA1AA/B00BB0BBB/aBCDe1FGHijKlmNoP
```

Where ever Pslackr requires an API token you need to use the last string in the URL `aBCDe1FGHijKlmNoP` in the example above.

## Usage

### Example of basic usage with suplied classes

```
<?php
require_once 'vendor/autoload.php';

use FullyBaked\Pslackr\Messages\CustomMessage;
use FullyBaked\Pslackr\Pslackr;

$message = new CustomMessage('Testing from Pslackr');

$config = ['token' => 'YOUR_TOKEN', 'domain' => 'YOUR_DOMAIN'];
$slack = new Pslackr($config);
$slack->send($message);
```

### Customise the message

The supplied CustomMessage class details the optional parameters that can be sent as part of the request. These
parameters allow you to customise the message.

1. Channel
2. Username
3. Icon (url or emoji)

```
<?php 

use FullyBaked\Pslackr\Messages\CustomMessage;

$message = new CustomMessage('Testing from Pslackr');

$message->channel('#my-other-channel');

$message->username('slackbot');

$message->iconUrl('http://example.tld/path/to/my.png');
// OR //
$message->iconEmoji(':ghost:');

```

### Changing the HTTP Client

By default Pslackr was built with [Guzzle][2] and has it listed as a dependency, however for various reasons you may
wish to use your own HTTP client.  If so, this can be acheived by implementing the `Transport` interface using your
own choice of HTTP client.

[1]: https://getcomposer.org/
[2]: http://docs.guzzlephp.org/en/latest/index.html
[3]: https://github.com/fullybaked/pslackr/issues/4
