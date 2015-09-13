mysql-test-schema Cookbook
=====================
The mysql-test-schema cookbook does the following:
- Sets up and loads the employees schema (https://dev.mysql.com/doc/employee/en/employees-introduction.html)
- Sets up and loads the sakila schema (http://dev.mysql.com/doc/sakila/en/sakila-introduction.html)

Requirements
------------
- Chef 11 or higher
- Ruby 1.9 or higher (preferably from the Chef full-stack installer)
- Network accessible package repositories

Platform Support
----------------
The following platforms are supported:
* CentOS
* Red Hat

The following 64-bit platforms have been tested:
* CentOS 6.4
* CentOS 6.5
* CentOS 7.0

Cookbook Dependencies
---------------------
- mysql

Usage
-----
Depending on which of the two schemas (or even both) you want to load include the necessary recipe in your node's `run_list`:

```json
{
  "name":"my_node",
  "run_list": [
    "recipe[mysql-test-schema::employees]"
    "recipe[mysql-test-schema::sakila]"
  ]
}
```

Or, place a dependency on the mysql-test-schema cookbook in your cookbook's  metadata.rb

```ruby
depends "mysql-test-schema", "~> 0.1"
```

Then, in a recipe:

```ruby
include_recipe "mysql-test-schema::employees"
include_recipe "mysql-test-schema::sakila"
```

#### MySQL versions supported
MySQL versions 5.1, 5.5 and 5.6 are supported

#### MySQL users used by the cookbook
The cookbook assumes that authentication using defaults-file has been setup so that it is not required to pass username and password on the command-line.

Attributes
----------
The following attributes are set by default:
```ruby
default["mysql_test_schema"]["employee"]["version"] = "1.0.6"
default["mysql_test_schema"]["employee"]["url"] = "https://launchpad.net/test-db/employees-db-1/#{node["mysql_test_schema"]["employee"]["version"]}/+download"
default["mysql_test_schema"]["employee"]["dump_filename"] = "employees_db-full-#{node["mysql_test_schema"]["employee"]["version"]}.tar.bz2"
default["mysql_test_schema"]["employee"]["checksum"] = "9be9b830a185e947758581cb06f529d1e8b675b29cde13a2860b1319b7e1cb7d"
default["mysql_test_schema"]["sakila"]["url"] = "http://downloads.mysql.com/docs"
default["mysql_test_schema"]["sakila"]["dump_filename"] = "sakila-db.tar.gz"
default["mysql_test_schema"]["sakila"]["checksum"] = "619bad5852078d30d7812492f4e75b3b4baeae99034b34a4934b3715c2abf2b8"
```

Contributing
------------
1. Fork the repository https://github.com/ovaistariq/cookbook-mysql-test-schema.git on Github
2. Create a named feature branch (like `add_component_x`)
3. Write your change
4. Write tests for your change (if applicable)
5. Run the tests, ensuring they all pass
6. Submit a Pull Request using Github

License & Authors
-----------------
- Author:: Ovais Tariq (<me@ovaistariq.net>)

```text
Copyright:: 2014-2015, Ovais Tariq (<me@ovaistariq.net>)

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
