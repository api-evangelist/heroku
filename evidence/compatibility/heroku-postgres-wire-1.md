<!-- fetched 2026-10-13 from https://devcenter.heroku.com/articles/heroku-postgresql by sweep-shape-compat.py; text extracted from the provider's own page -->

Heroku Postgres | Heroku Dev Center 
 Skip Navigation 
 Dev Center 
 Get Started 
 Documentation 
 Changelog 
 Search 
 Dev Center 
 Get Started 
 Node.js 
 Ruby on Rails 
 Ruby 
 Python 
 Java 
 PHP 
 Go 
 Scala 
 Clojure 
 .NET 
 Documentation 
 Changelog 
 More 
 Additional Resources 
 Home 
 Elements 
 Products 
 Pricing 
 Careers 
 Help 
 Status 
 Events 
 Podcasts 
 Compliance Center 
 Heroku Blog 
 Heroku Blog 
 Find out what's new with Heroku on our blog.
 Visit Blog 
 Log in 
 or 
 Sign up 
 Show nav
 View categories
 Categories
 Heroku Architecture
 Compute (Dynos)
 Dyno Management
 Dyno Concepts
 Dyno Behavior
 Dyno Reference
 Dyno Troubleshooting
 Stacks (operating system images)
 Networking & DNS
 Platform Policies
 Platform Principles
 Buildpacks
 Developer Tools
 AI Tools
 Command Line
 Heroku VS Code Extension
 Deployment
 Deploying with Git
 Deploying with Docker
 Deployment Integrations
 Continuous Delivery & Integration (Heroku Flow)
 Continuous Integration
 Language Support
 .NET
 Working with .NET
 Clojure
 Front-end
 Go
 Go Dependency Management
 Java
 Java Behavior in Heroku
 Working with Java
 Working with Maven
 Working with Spring Boot
 Troubleshooting Java Apps
 Node.js
 Working with Node.js
 Troubleshooting Node.js Apps
 Node.js Behavior in Heroku
 PHP
 Working with PHP
 PHP Behavior in Heroku
 Python
 Working with Python
 Background Jobs in Python
 Python Behavior in Heroku
 Working with Django
 Ruby
 Rails Support
 Working with Rails
 Working with Bundler
 Working with Ruby
 Ruby Behavior in Heroku
 Troubleshooting Ruby Apps
 Scala
 Databases & Data Management
 Heroku Postgres
 Postgres Basics
 Postgres Getting Started
 Postgres Performance
 Postgres Data Transfer & Preservation
 Postgres Availability
 Postgres Special Topics
 Migrating to Heroku Postgres
 Heroku Postgres Advanced
 Heroku Key-Value Store
 Apache Kafka on Heroku
 Other Data Stores
 AI
 Inference Essentials
 Inference API
 Inference Quick Start Guides
 AI Models
 Tool Use
 AI Integrations
 Vector Database
 Monitoring & Metrics
 Logging
 App Performance
 Add-ons
 All Add-ons
 Collaboration
 Security
 App Security
 Identities & Authentication
 Single Sign-on (SSO)
 Private Spaces
 Infrastructure Networking
 Compliance
 Heroku Enterprise
 Enterprise Accounts
 Enterprise Teams
 Patterns & Best Practices
 Extending Heroku
 Platform API
 App Webhooks
 Heroku Labs
 Building Add-ons
 Add-on Development Tasks
 Add-on APIs
 Add-on Guidelines & Requirements
 Building CLI Plugins
 Developing Buildpacks
 Dev Center
 Accounts & Billing
 Troubleshooting & Support
 Integrating with Salesforce
 Heroku AppLink
 Getting Started with Heroku AppLink
 Working with Heroku AppLink
 Heroku AppLink Reference
 Heroku Connect (Salesforce sync)
 Heroku Connect Administration
 Heroku Connect Reference
 Heroku Connect Troubleshooting
 Other Salesforce Integrations
 Databases & Data Management 
 Heroku Postgres 
 Postgres Basics 
 Heroku Postgres 
 Heroku Postgres
 English — 日本語に切り替える 
 Table of Contents [expand] 
 Understanding Heroku Postgres Plans 
 Provisioning Heroku Postgres 
 Local Setup 
 Using the CLI 
 Manage Your Heroku Postgres Database 
 Version Support 
 Migrating Between Plans 
 Connecting to Heroku Postgres 
 Monitor Your Heroku Postgres Database 
 High Availability 
 Maintenance 
 Security and Compliance 
 Support 
 Last updated October 06, 2026
 Heroku Postgres is a managed SQL database service provided directly by Heroku. You can access a Heroku Postgres database from any language with a PostgreSQL driver, including all languages Heroku officially supports .
 In addition to a variety of Heroku CLI commands to manage your database, Heroku Postgres provides a web dashboard from the Heroku Dashboard , Dataclips to share queries , and several other helpful features.
 Understanding Heroku Postgres Plans
 Heroku Postgres offers a variety of plans, spread across different tiers of service: Advanced, Essential, and “classic” tiers which include Standard, Premium, Private, and Shield. For more information on what each plan provides, see Choosing the Right Heroku Postgres Plan .
 Pricing information for Heroku Postgres plans is available on the Heroku Postgres add-on page .
 If your app’s requirements eventually outgrow the resources provided by the initial plan you selected, you can upgrade Essential and classic Postgres databases to a new plan, or update the configuration on Advanced databases .
 Provisioning Heroku Postgres
 For more information about how to provision a Heroku Postgres database, see:
 Essential and Classic Databases : Provisioning Heroku Postgres 
 Advanced Databases : Provisioning Heroku Postgres Advanced 
 Local Setup
 Heroku recommends running Postgres locally to ensure parity between environments . For more information about how to set up Heroku Postgres to run in your local environment, see Local Setup for Heroku Postgres .
 Using the CLI
 For more information about managing Heroku Postgres using the CLI, see:
 Essential and Classic Databases : Managing Heroku Postgres Using the CLI 
 Advanced Databases : Managing Heroku Postgres Using the CLI 
 Manage Your Heroku Postgres Database
 Designating a Primary Database
 For more information about designating a primary database, see:
 Essential and Classic Databases : Provisioning Heroku Postgres. 
 Advanced Databases : Provisioning Heroku Postgres Advanced 
 Sharing Heroku Postgres Between Applications
 For more information about sharing your database between applications, see:
 Essential and Classic Databases : Provisioning Heroku Postgres. 
 Advanced Databases : Provisioning Heroku Postgres Advanced 
 Importing and Exporting Databases
 For more information about exporting to or importing from external PostgreSQL databases with PGBackups, see Importing and Exporting Heroku Postgres Databases .
 Configure Database Settings
 For information about configuring settings on your database, see Heroku PGSettings .
 Destroying the Add-on
 For more information about removing your database add-on, see:
 Classic Databases : Provisioning Heroku Postgres 
 Advanced Databases : Provisioning Heroku Postgres Advanced 
 Version Support
 The PostgreSQL project releases new major versions on a yearly basis. Heroku Postgres supports each major version after testing for compatibility with the platform. For more information about version support on Heroku Postgres, see Heroku Postgres Version Support .
 For more information about upgrading the version on your database, see Upgrading the Version of a Heroku Postgres Database .
 Migrating Between Plans
 On Advanced databases , you can update an existing database’s plan level instead of migrating to a new plan.
 For more information about upgrading and migrating Essential and classic database plans, see Changing the Plan or Infrastructure of a Heroku Postgres Database .
 Connecting to Heroku Postgres
 For examples on connecting to Heroku Postgres, see:
 Connecting to Heroku Postgres 
 Connecting to Common Runtime Heroku Postgres Databases from an External Resource 
 Connecting to a Private or Shield Heroku Postgres Database from an External Resource 
 Monitor Your Heroku Postgres Database
 Performance Analytics
 For more information about performance analytics, see Heroku Postgres Performance Analytics .
 Metrics Logs
 For more information about Heroku Postgres metrics logs, see Heroku Postgres Metrics Logs .
 To get started on monitoring your database and best practices, see:
 Getting Started: Monitoring a Heroku Postgres Database 
 Heroku Postgres Monitoring Best Practices 
 High Availability
 For more information about high availability on Heroku Postgres, see High Availability on Heroku Postgres .
 Maintenance
 From time to time, Heroku performs maintenance tasks on a Heroku Postgres database. Typical tasks include updating the underlying infrastructure of the database. For more information, see Heroku Postgres Maintenance .
 Security and Compliance
 Data Residency
 When a database gets provisioned, the data associated with that database is stored within the region in which it’s created. However, some services ancillary to Heroku Postgres and the systems managing the database fleet aren’t located within the same region as the provisioned databases:
 Postgres Continuous Protection for disaster recovery stores the base backup and write-ahead logs in the same region that the database is located.
 Logs for the Common Runtime are routed in the same region the app is running within. For example, logs for an app in the us region gets routed through the us infrastructure.
 Logs for apps in Private Spaces stay within the same region as the space itself. For example, logs for an app in a Tokyo space routes through the infrastructure in Tokyo. You can deploy apps with strict compliance requirements in Shield Private Spaces , which uses Private Space Logging to route logs instead of Logplex.
 You can block the logging of Heroku Postgres queries and errors by using the --block-logs flag when creating the database with heroku addons:create heroku-postgres:... .
 Heroku PGBackups snapshots are stored in the US. To capture logical backups in another region, see Heroku Postgres Logical Backups .
 Dataclips are stored in the US.
 See the Salesforce Infrastructure & Sub-processors document for the list of sub-processors Heroku uses and the list of countries where Heroku data is stored and processed.
 Support
 Submit all Heroku Postgres support and runtime issues via one of the Heroku Support channels .
 Feedback
 Log in to submit feedback. 
 Information & Support
 Getting Started 
 Documentation 
 Changelog 
 Compliance Center 
 Training & Education 
 Blog 
 Support Channels 
 Status 
 Language Reference
 Node.js 
 Ruby 
 Java 
 PHP 
 Python 
 Go 
 Scala 
 Clojure 
 .NET 
 Other Resources
 Careers 
 Elements 
 Products 
 Pricing 
 RSS 
 Dev Center Articles 
 Dev Center Changelog 
 Heroku Blog 
 Heroku News Blog 
 Heroku Engineering Blog 
 Twitter 
 Dev Center Articles 
 Dev Center Changelog 
 Heroku 
 Heroku Status 
 Github 
 LinkedIn 
 © 2026 Salesforce, Inc. All rights reserved. Various trademarks held by their respective owners. Salesforce Tower, 415 Mission Street, 3rd Floor, San Francisco, CA 94105, United States
 heroku.com 
 Legal 
 Terms of Service 
 Privacy Information 
 Responsible Disclosure 
 Trust 
 Contact 
 Cookie Preferences 
 Your Privacy Choices
