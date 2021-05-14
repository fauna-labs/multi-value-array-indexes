This repository contains unofficial patterns, sample code, or tools to help developers build more effectively with [Fauna][fauna]. All [Fauna Labs][fauna-labs] repositories are provided “as-is” and without support. By using this repository or its contents, you agree that this repository may never be officially supported and moved to the [Fauna organization][fauna-organization].

---

# Multi-value array indexes

This repository contains a simple example of building and querying multi-value array indexes.

## Resources

When you apply the migration from this repository, Fauna creates two collections and one index in a single transaction.

* A [levels collection](fauna/resources/collections/levels.fql).
* A [sessions collection](fauna/resources/collections/sessions.fql).
* An index for [sessions_by_level](fauna/resources/indexes/sessions_by_level). This index illustrates how to create an MVA over a many-to-many relationship. In this case, one session has many levels and one level has many sessions.

## Pre-requisites

* To deploy this application you must have access to a Fauna account. You can [register for a free Fauna account][fauna-register] and benefit from [Fauna’s free tier][fauna-free-tier] while you learn and build. You do not need to provide payment information until you upgrade your plan.
* Install [Node.js version 14 or higher][nodejs-install].
* Install the [Fauna shell][fauna-shell] CLI.

## Using this repository

Perform the following steps in order to create a database, create the required collections and index, populate sample data, and query the index.

### Setup a Fauna database

1. After installing the Fauna shell, login to your account.
    ```bash
    fauna cloud-login
    ```
1. Create a database for this project.
    ```bash
    fauna create-database mva-indexes
    ```
1. Create an access key for this database.
    ```bash
    fauna create-key mva-indexes
    ```
1. Copy the secret that is generated (beginning with `fn`) and store it in a secure location. Optionally, load it into your environment as `FAUNA_ADMIN_KEY` to simplify the following steps.

    **IMPORTANT**: If you copy and paste the below to load the secret into your environment, be sure to include the leading space before `export` to avoid storing the secret in your shell's history.
    ```bash
     export FAUNA_ADMIN_KEY=&lt;secret&gt;
    ```

Every key is uniquely associated to a single database. Using this key will set the context or scope of operations to your `mva-indexes` database.

### Create required collections and index

1. Clone this repository.
    ```bash
    git clone https://github.com/fauna-labs/multi-value-array-indexes.git
    ```
1. Change to the repository directory
    ```bash
    cd multi-value-array-indexes
    ```
1. Install dependencies
    ```bash
    npm install
    ```
1. Create the collections and index
    ```bash
    npx fauna-schema-migrate apply all
    ```

### Populate sample data

1. Open the Fauna shell and connect to your database.
    ```bash
    fauna shell mva-indexes
    ```
1. Copy and paste the contents of [sessions.fql](fauna/documents/sessions.fql) into the shell and press the return key.
1. Copy and paste the contents of [levels.fql](fauna/documents/levels.fql) into the shell and press the return key.

### Query the index

With the Fauna shell open to your database, copy and paste any of the queries from [sessions_by_index.fql](fauna/queries/sessions_by_index.fql) to see the results.

## Cleaning up resources

Once you complete this tutorial, you may wish to remove the resources you create to avoid unexpected charges.

1. From the shell, delete your database. This deletes all associated collections, documents, keys, and indexes.
    ```bash
    fauna delete-database mva-indexes
    ```

---

Copyright Fauna, Inc. or its affiliates. All rights reserved. SPDX-License-Identifier: MIT-0

[fauna]: https://www.fauna.com/
[fauna-free-tier]: https://fauna.com/pricing
[fauna-labs]: https://github.com/fauna-labs
[fauna-organization]: https://github.com/fauna
[fauna-register]: https://dashboard.fauna.com/accounts/register
[fauna-shell]: https://github.com/fauna/fauna-shell
[nodejs-install]: https://nodejs.org/en/
