
# HEROKU SETUP


## Angular-decoupled-server

-First type into the command line: ‘npm install cors --save’

-Then go into app.js and add to the required files ‘var cors = require(‘cors’);

-Then go down to the route middlewares and add ‘app.use(cors()); above all the others

-Make sure it’s above the others! Ex below:

```
// cors npm package
app.use(cors());

// auth middleware
app.use(helpers.authMiddleWare);

//  auth route
app.use('/auth',  auth);

// auth middleware to ensure user is authenticated
app.use('/api', helpers.ensureauthenticated, api);
```

In your command line:
```
heroku create yourAppName-server

heroku addons:create heroku-postgresql

You now have your heroku remote automatically added to your git remotes which you can push the server to
```

## Angular-decoupled-db

```
Copy the heroku git remote from the decoupled-server (above)

You can get the remote address by typing git remote -v into the command line while in the directory for the decoupled server (above)

In your command line: git remote add heroku [paste the heroku git remote from above here]

Now type heroku config and copy everything after DATABASE_URL ex. postgres://hfjspeirugyfhr:DKeptjDsJajelgHEIGH@...... and add it to your .env file

Add it like “ DATABASE_URL=your-database-url-string-you-just-copied

No spaces or quotes anywhere

Now in your command line:
		- knex migrate:latest --env production
		- knex seed:run --env production
      		- Your heroku database is now ready
```

## Angular-decoupled-view
```
For heroku
Change all the http requests from localhost to the new app url for the decoupled server from heroku so instead of localhost:3000/api/list it would be your-new-herku-url-for-the-api-server.herokuapp.com/api/list. Make sure to change all of them including the auth ones.
In your command line:
heroku create your-app-name (different and separate from the name and heroku app you created for the server)
     - You now have a heroku git remote to push to for this app and this will be the site that users actually interact with. This heroku app communicates with the deployed server-api app you just made which communicates with the database tied to it. Decoupled!
```

For firebase set up go to
https://www.firebase.com/docs/hosting/guide/deploying.html
