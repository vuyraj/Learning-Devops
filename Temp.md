
CLASS DIAGRAM

```
classDiagram
    class PasswordManager {
        - passwords: Map<String, String>
        - settings: UserSettings
        + generatePassword(length: int, useSymbols: bool, useNumbers: bool): String
        + savePassword(site: String, password: String)
        + retrievePassword(site: String): String
        + deletePassword(site: String)
    }

    class PasswordGenerator {
        - defaultLength: int
        - includeSymbols: bool
        - includeNumbers: bool
        + generate(length: int, useSymbols: bool, useNumbers: bool): String
        + setDefaultLength(length: int)
        + enableSymbols(enable: bool)
        + enableNumbers(enable: bool)
    }

    class StorageManager {
        - storageType: String
        + storeData(key: String, value: String)
        + retrieveData(key: String): String
        + deleteData(key: String)
    }

    class EncryptionService {
        - encryptionKey: String
        + encryptData(data: String): String
        + decryptData(data: String): String
    }

    class UserSettings {
        - passwordLength: int
        - useSymbols: bool
        - useNumbers: bool
        + setPreferences(length: int, useSymbols: bool, useNumbers: bool)
        + getPreferences(): Map<String, Object>
    }

    class Dashboard {
        - storedPasswords: List<String>
        - userPreferences: UserSettings
        + displayPassword(password: String)
        + getUserInput(): Map<String, Object>
        + showStoredPasswords()
        + updatePreferences(settings: UserSettings)
    }

    PasswordManager --> PasswordGenerator : 1 Uses 1
    PasswordManager --> StorageManager : 1 Uses 1
    StorageManager --> EncryptionService : 1 Uses 1
    PasswordManager --> UserSettings : 1 Reads/Writes 1
    Dashboard --> StorageManager : 1 Interacts with n
    Dashboard --> UserSettings : 1 Reads 1
    PasswordManager --> Dashboard : 1 Displays n
    StorageManager --> PasswordManager : n Stores 1
```


sequenceDiagram


```
sequenceDiagram
    participant User
    participant PasswordManager
    participant Database

    User ->> PasswordManager: Open password manager extension
    PasswordManager ->> Database: Check user login status
    Database -->> PasswordManager: Return login status
    PasswordManager ->> User: Prompt login if necessary
    User ->> PasswordManager: Enter credentials
    PasswordManager ->> Database: Authenticate user
    Database -->> PasswordManager: Return authentication result
    PasswordManager ->> User: Display main menu

    User ->> PasswordManager: Choose option (Generate or Retrieve Password)
    
    par Generate Password
        PasswordManager ->> PasswordManager: Generate secure password
        PasswordManager ->> User: Prompt to save password
        User ->> PasswordManager: Provide website for saving password
        PasswordManager ->> PasswordManager: Encrypt password
        PasswordManager ->> Database: Store encrypted password
        Database -->> PasswordManager: Acknowledge storage
    and Retrieve Password
        User ->> PasswordManager: Request stored password
        PasswordManager ->> Database: Retrieve encrypted password
        Database -->> PasswordManager: Return encrypted password
        PasswordManager ->> PasswordManager: Decrypt password
        PasswordManager -->> User: Return decrypted password
    end

    User ->> PasswordManager: Exit or log out
    PasswordManager ->> Database: Logout user
    PasswordManager -->> User: Session ended


```



activity Diagram

```
@startuml
|User|
start
:Open password manager extension;

|PasswordManager|

if (User is logged in?) then (Yes)
  |PasswordManager|
  :Proceed to main menu;
else (No)
  |PasswordManager|
  :Prompt user for login ;
  |User|
  :Enter credentials;

  |PasswordManager|
  if (Login successful?) then (Yes)
    :Proceed to main menu;
  else (No)
    :Show error message;
    stop
  endif
endif

|PasswordManager|
:Present options to user 
(Generate or Retrieve Password);

|User|
:Choose action;
split
  if (Generate Password?) then (Yes)
    |PasswordManager|
    :Generate secure password;
    |User|
    :Decide whether to save password?;
    
    if (Save password?) then (Yes)
      |PasswordManager|
      :Prompt user for website;
      |User|
      :Provide website;
      |PasswordManager|
      :Save password securely;
    else (No)
      :Return to main menu;
    endif
  endif
split again
  if (Retrieve Password?) then (Yes)
    |PasswordManager|
    :Prompt user for website;
    |User|
    :Provide website;
    |PasswordManager|
    :Decrypt password;
  endif
end split

|PasswordManager|
:Display password to User;

|User|
:View displayed password;

|PasswordManager|
:Allow user to exit or log out;

|User|
:Exit or log out;

stop
@enduml


```


component diagram 

```

graph TD
    A[User] --> B[PasswordManager]
    B --> C[Database]
    B --> D[PasswordGenerator]
    B --> E[EncryptionService]
    
    A -->|Choose Action (Generate/Retrieve)| B
    B -->|Check Login Status| C
    B -->|Store/Retrieve Encrypted Password| C
    D -->|Generate Password| B
    E -->|Encrypt/Decrypt Password| B

```
