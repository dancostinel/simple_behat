Simple Behat testing
====================
* Install new `symfony` project and cd into that directory. This will install the latest version.
```
$ symfony new project
cd project
```
* Require in all dependencies
```
project$ composer require --dev behat/behat
project$ composer require --dev behat/symfony2-extension
project$ composer require --dev behat/mink
project$ composer require --dev behat/mink-extension
project$ composer require --dev behat/mink-browserkit-driver
```
Or you can put them in a composer.json file, and require them all in once, using `composer install`.

* Create `features/` directory
```
$ vendor/bin/behat --init
```
* Change the context to be `MinkContext`
```
# features/bootstrap/FeatureContext.php

...
use Behat\MinkExtension\Context\MinkContext;

class FeatureContext extends MinkContext ...
```
* Simple test
```
# features/test.feature

Feature: test behat
  In order to test behat
  As regular user
  I need to be able to test behat

  Scenario: test behat
    Given I go to "http://127.0.0.1/app_dev.php/"
    Then I should see:
      """
	  Welcome to
      Symfony 3.1.2
	  """
```
* To run all tests
```
$ vendor/bin/behat ---> runs all the featured tests
```
8 To run a specific test
```
$ vendor/bin/behat features/test.feature
```
# Login test with Behat in Symfony. Using `FOSUserBundle` for logging in functionality.
* Make symfony redirect to the profile page, after a successfull login attempt
```
# app/config/security.yml:
security:
    firewalls:
        main:
            # ...
            default_target_path: fos_user_profile_show
```
* Create the test
```
# features/web/authentication.feature
Feature: Authentication
  In order to gain access to the site management area
  As an admin
  I need to be able to login and logout

  Scenario: Logging in
    Given I am on "/login"
    And I fill in "Username" with "user"
    And I fill in "Password" with "user"
    And I press "Log in"
    Then I should see "Logged in as user"
```
* Run the test
```
$ vendor/bin/behat features/test.feature
```
