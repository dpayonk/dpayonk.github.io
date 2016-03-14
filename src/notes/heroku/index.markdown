---
layout: page
title: "heroku"
date: 2013-09-07 10:59
comments: true
sharing: true
footer: true
---
## Config Environment
Heroku uses by convention some of the following environment variables to provide
connectivity to data stores
   * REDISTOGO
   * DATABASE_URL

##Database Connection Strings for Postgres
```
jdbc:postgresql://postgresuri.url.com/db_name?user=db_user&password=db_password&ssl=true&sslfactory=org.postgresql.ssl.NonValidatingFactory
---Example---
url: jdbc:postgresql://localhost/railsdb_dev?user=rails_username&password=rails_password
```
***You will need to enable appropriate ports for Heroku apps to read from amazon database***
