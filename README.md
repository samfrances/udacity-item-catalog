udacity-item-catalog
=============
Forked from: udacity/rdb-fullstack

Admin interface
-------------
The admin interface can be found at `/admin/`. This allows the admin to view a table of information about users, and to activate and deactivate users.

Admin users can also edit and delete any item or category, regardless of ownership.

Admin privileges script
-------------
To make a user into an admin, use the script `make_admin.py` in `/vagrant/catalog`, specifying either `revoke` or `grant` and the email address of the relevant user, and then follow the prompts. For example:

```
vagrant@vagrant-ubuntu-trusty-32:/vagrant/catalog$ python make_admin.py grant example@example.com
Looking for a user with email address: example@example.com
Found the following users:

<User: name='Bob Example', email='example@example.com', id=2, activated=True, admin=False>

Grant admin privileges? (y/n): y
Admin privileges changed.

<User: name='Bob Example', email='example@example.com', id=2, activated=True, admin=True>

Goodbye

```

JSON API endpoints
-------------
- /catalog.json
    + Shows information on all tags and all items, referenced from 'Items' and 'Tags' keys
- /catalog/items.json
    + Shows only the 'Items' portion of the information in /catalog.json
- /catalog/tags.json
    + Shows only the 'Tags' portion of the information in /catalog.json
- /catalog/tags/view/\<tag_name>.json
    + Shows information for the tag with name <tag_name>
- /catalog/items/view/\<item_name>-\<int:item_id>.json
    + Shows information for the tag with the specified name and id

Atom Feed
--------------
An atom feed of the latest items can be accessed at /catalog/recent.atom .

Logging
--------------
Creation, deletion and editing of tags and items is recorded in a log file, configured by default as `catalog.log` in /vagrant/catalog/ .

Third-party code
--------------
- The lines in the `Item` model creating the automatically populated and updated `created_on` and `updated_on` columns relies heavily on this Stackoverflow answer:
    + http://stackoverflow.com/a/12155686
- The Atom feed borrows from the following examples:
    + http://flask.pocoo.org/snippets/10/
    + http://werkzeug.pocoo.org/docs/0.11/contrib/atom/
- The logging feature was created with help from the following tutorials and examples:
    + http://flask.pocoo.org/docs/0.10/quickstart/#logging
    + https://gist.github.com/ibeex/3257877
    + https://docs.python.org/2/howto/logging.html
- The Oauth code takes Udacity code samples as a starting point, but modifed these to use WTForms CSRF features and add other functionality:
    + https://github.com/udacity/ud330/blob/master/Lesson2/step5/project.py
    + https://github.com/udacity/ud330/blob/master/Lesson2/step4/templates/login.html
- The `gdisconnect` view from the Udacity code samples was used in full:
    + https://github.com/udacity/ud330/blob/master/Lesson2/step6/project.py
- The `login_required` decorator in the `auth_helpers` module is based on the example in this tutorial:
    + http://flask.pocoo.org/docs/0.10/patterns/viewdecorators/
- Used Udacity class methods `getByID`, `getIDByEmail` and `createForID` are based on the helper functions `getUserInfo`, `getUserId` and `createUSer` in:
    + https://github.com/udacity/ud330/blob/master/Lesson3/step2Quiz/project.py
- The basic Bootstrap template is adapted from here:
    + http://getbootstrap.com/examples/theme/
- The form styling is based on this Bootstrap tutorial:
    + http://getbootstrap.com/css/#forms