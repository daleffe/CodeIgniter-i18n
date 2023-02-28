# Internationalization (i18n) library for CodeIgniter
It is a simple internationalization (i18n) for CodeIgniter 2.2.X

```
What do we do different from the original project?

The original project shows an error if text doesn't contain a translated text. In this, we present the raw text informed if translated text not found.
```

## Requirements
- CodeIgniter 2.2.X
- Enable Session

# What it does
Have the language field in the URL, exapmle:

- http://xxx.com/?lang=en-us
- http://xxx.com/index.php/welcome/index?lang=en-us

# Installation
- Copy application/config/language.php to your_app/application/config/
- Copy application/core/MY_Lang.php to your_app/application/core/

# Configuration
Open *application/config/language.php* file:

* language_field

You can find this field in URL, default value is "lang", example: xxx.com/?lang=zh-tw

* language_default_key

Default language you want to output.

* language_list

The language array lists you can support.

    key: defined from $_['HTTP_ACCEPT_LANGUAGE']
    value: corresponding to your language folder.

The language class will add prefix value on all language array key automatically.

example:

    about_lang.php => key: about.xxxx
    api_lang.php => Key: api.xxxx

## Enable language helper at *application\config\autoload.php*:
```php
$autoload['helper'] = array('language');
```

# How to use
Create a language file at *application/language/english/about_lang.php*:
```php
    <?php  if ( ! defined('BASEPATH')) exit('No direct script access allowed');
    $lang['home'] = "Home";
    $lang['introduction'] = "Introduction";
    $lang['location'] = "Location";
```
## Controller
Load language file at constructor:
```php
class About extends CI_Controller {
	
	public function __construct()
    {
		parent::__construct();

		$this->lang->load('about');
    }
```

At view:
```php
    <?php
    // Language_helper needed (deprecated)
    echo lang('about.home');
    echo lang('about.introduction');
    echo lang('about.location');
    echo lang('Text not translated');

    echo $this->lang->line('about.home');    
    echo $this->lang->line('about.introduction');    
    echo $this->lang->line('about.location');    
    echo $this->lang->line('Text not translated');
```
