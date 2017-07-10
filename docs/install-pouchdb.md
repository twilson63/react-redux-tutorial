## Install PouchDB

PouchDB is where we will store our data for our application, we will start by storing the data locally with just our browser, then in the advanced exercises we will store the data in the cloud.

If you want to read up on PouchDB - check this link out - https://pouchdb.com/ 

For now, we are going to create a new module file called `db.js`, this file will be a factory function for all of our database methods, that way we only have one place that our db is being connected.

``` js
import PouchDB from 'pouchdb'
import R from 'ramda'
const { pluck } = R

const db = PouchDB('error-log')

export const allDocs = () => {
  return db.allDocs({include_docs: true})
    .then(res => pluck('doc', res.rows))
}

```

We will add more functions as we go through the tutorial, but for now, we just added a function to get all the docs from the database.

To verify that we did not break anything, click the `Show` Link at the top of glitch and make sure you can still see `Hello React`

---

[Menu](./?path=README.md:1:0)