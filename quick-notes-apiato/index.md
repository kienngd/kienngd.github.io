# 🚧 Quick-notes working with APIATO


<!--more-->
# Some Quick-notes

<font color="#0000FF">These notes will be moved to another place soon</font>

## What is apiato

## Translate
- **Container Languages Folder Structure**
  ```
    - app
      - Containers
          - MyContainer
              - Resources
                  - Languages
                    - en
                        - messages.php
                        - users.php
                    - ar
                        - messages.php
                        - users.php
  ```
  ```php
    // Namspace is container-name with to lower: MyContainer --> mycontainer
    __('mycontainer::messages.welcome', [], 'vi');
    // 2nd param is bind params.
    // 3rd param is locale-name
  ```

- **Default Languages Folder Structure**
  ```
    - resources/lang/en/messages.php
    - resources/lang/vi/messages.php
    - resources/lang/vi.json
    - resources/lang/en.json
  ```
  ```php
    // Namspace is container-name with to lower: MyContainer --> mycontainer
    __('messages.welcome', [], 'vi'); // Get key welcome from file messsages
    __('welcome', [], 'vi'); // Get key welcom from file vi.json
    // 2nd param is bind params.
    // 3rd param is locale-name
  ```

- **Overriding Package Language Files**
  - `resources/lang/vendor/{package}/{locale}`

- Config: `config/app.php` `locale` and `fallback_locale`

- **Support new languages** (don't need this container?!)
  - `supported_languages` in **app/Containers/Localization/Configs/localization.php**

- Middleware set language:
  - `app/Http/Middleware/LocalizationSystemMiddleware.php`
- Change language
  - Route: `lang/{locale}`
  - Route name: `??`
  - Controller: `app/Containers/User/UI/WEB/Controllers/LanguageController.php` function `changeLang`
