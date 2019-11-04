# Commands

{% hint style="info" %}
You can invoke code.store CLI either by using the full **`codestore`** command, or by using the short version **`cs`**.
{% endhint %}

```bash
$ cs login
$ cs config # optional, allows switching Organizations
$ cs init {name} # Creates a new service group/project

-> Code.Store: Creating new project {name}
-> Code.Store: Do you need a database in your project? Y/N
-> Y
-> Code.Store: Please enter the name of database:
-> {dbName}
-> Code.Store: Created a database with name {name}
-> Code.Sotre: We've added a database for you.
-> Code.Store: Do you need a sample GraphQL configuration? Y/N
-> Code.Store: Sample GraphQL
-> Code.Store: Please use next command to add or remove new services to the project:

$ cs service:add {name} # Creates a new service with specific name
$ cs db:add {name} # Creates a new database for your project
$ cs service:remove {name} # Removes service from the project
$ cs db:remove {name} # Removes database from the project
$ cs service:check {env} # Verifies the difference between local and remote schema
$ cs test:run # Performs a test run for all existing tests in project
$ cs test:generate-data # Generates dummy test data for local environment
$ cs test:add {name} # Will we place a tests in root or per service?
$ cs test:remove {name} # Removes test from project

$ cs env:variable:add {name} {default} # Adds new environment variable
$ cs env:variable:remove {name} # Removes environment

$ cs run # Starts a GraphQL locally
$ cs logs # Starts a listener for a logs from cloud
$ cs deploy {env} (dev,staging,production) # Deploya a project to cloud
$ cs pull {name} # Pulls a project from cloud
$ cs list # Shows a list of projects in cloud
```

