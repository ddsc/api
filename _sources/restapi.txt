.. _`chapter-restapi`


The Lizard Portal API
#####################

This describes the resources that make up the Lizard API v1.

Portal
=======

Get a Portal List
-------------------

::

  GET /api/v1/portals

**Response** ::

  Status: 200 OK

.. code-block:: javascript

  {
    data: [
      {
        "id" : "{portal id}",
        "name": "{portal name}",
        "description": "{portal description}",
        "url": "/api/v1/portals/{portal id}"
      }
    ]
    count: 1
  }


  {
    data: {
      "id": "{portal id}"
      "name": "{portal name}"
      "description": "{portal description}",
      "icon": "/api/v1/icons/4"
	  "appScreenUrl": "/api/v1/portals/{portalid}/appScreen/"
      "links": [
         {
           "name": "{link name}",
           "url": "{link url}"
         },
      ],
    }
  }


Application Screen
====================

Get a list of Application Screens
----------------------------------

::

  GET /api/v1/portals/:portalid/appscreens/

**Response** ::

  Status: 200 OK

.. code-block:: javascript

  {
    "data": [
      {
        "id": "{app id}",
		"name": "{app name}",
		"description": "{app description}",
		"url": "/api/v1/portal/{app id}",
		"icon": "/api/v1/icon/{icon id}",
		"actionType": "lizard.app.xxxxx"
	  },
      {
	    "id": '{app id2}",
		"name": "{app name2}",
		"description": "{app description}",
		"url": "/api/v1/portal/{app id2}",
		"icon": "/api/v1/icon/{icon id}",
		"actionType": "linkTo"
	  }
    ],
	"count": 1
   }

Get a Application Screen
---------------------------

::

  GET /api/v1/portals/:portalid/appscreens/:appscreenid

**Response** ::

  Status: 200 OK

.. code-block:: javascript

  {
    "data": {
      "id": "{app id}",
	  "name": "{app name}",
	  "description": "{app description}",
	  "url": "/api/v1/portal/{app id}",
	  "icon": "/api/v1/icon/{icon id}",
	  "actionType": "lizard.app.xxxxx"
     }
   }

Applications
===============

Get a list of Applications
----------------------------

.. note::

  This seems to be the same as the Application Screen.

::

  GET /api/v1/apps

**Response** ::

  Status: 200 OK

.. code-block:: javascript


  {
    "data": [
      {
        "id": "{app id}",
        "name": "{app name}",
        "description": "{app description}",
        "url": "/api/v1/apps/{app id}",
        "icon": "/api/v1/icons/{icon id}",
        "actionType": "{lizard.app.xxxxx}",
      },
    ],
    "count": 1
  }

Get a Application
-----------------------

.. note::

  This seems to be a double way to specify the Application Screens.

::

  GET /api/v1/apps/:portalid

**Response** ::

  Status: 200 OK

.. code-block:: javascript

  {
    data: {
        id: '{app_id}',
        name: '{app_name}',
        description: '{app_description}',
        icon: '/api/v1/icon/{app_id}/',
        actionType: 'lizard.app.xxxxx',
        actionConfig: {
               <<configuration of Action/ App>>
        }
     }
  }


Icons
=====

Get a list of Icons
-----------------------

::

  GET /api/v1/icons

**Response** ::

  Status: 200 OK

.. code-block:: javascript

  {
    data: [
      {
        "id": "{icon id}",
        "url": "/api/v1/icons/{icon_id}",
      }
	]
    count: 1
  }


Get an Icon
-----------------------

::

  GET /api/v1/icons/:iconid

**Response** ::

  Status: 200 OK
  Body: a png image

**Parameters**

size

  `Integer` of the size. Options are: 8 (8x8), 16 (16x16), 32 (32x32) pixels.
  The default is 32.


Workspaces
============

Get a list of Workspaces
---------------------------

::

  GET /api/v1/workspaces/

**Response** ::

  Status: 200 OK

.. code-block:: javascript

  {
    "total": 1,
    "count": 1,
    "start": 1,
    "data": [
      {
        "id": "{id}",
        "name": "{name}",
        "description": "{description}",
        "tags": [
          "{tag}",
          "{tag}"
        ],
        "ownerType": "{owner_type}",
        "status": "{status}",
        "owner": {
          "id": {"id"},
          "name": "{owner_name}"
        },
        "url": "/api/v1/workspaces/:workspaceid",
        "lastModifiedAt": "{last_modified_at}"
      }
    ]
  }

**Parameters**:

start
  `Integer` of the record to start with. Default is 0.
limit
  `Integer` of the number of records in the response. Default is 25.
filter
  `Object` Applied filters in the request.
  .. note::
    Add an example
order
  `String` of the field name on which the list is orderd.
  Default is 'Modification Date'.
reverse
  `Boolean` if the data should be reversed or not. Default is False.


Create a Workspace
------------------------

::

  POST /api/v1/workspaces/

**Parameters**:

name
  `String` of the workspace name
description
  `String` of the description of the workspace
tags
  `Array of Strings` of the tags
ownerType
  `String` of the owner type. Options are: private, shared, organization, public
status
  `String` of the status
.. note::
    Add a list of acceptable statuses
owner
  `String` of the slug of the owner
lastModifiedAt
  `Timestamp` of when this object was last edited

**Response** ::

  Status: 201 Created
  Location: api/v1/workspaces/:id

.. code-block:: javascript

  {
    "message": "{Optional message with the result of the action}",
	"data": {
      "id": "{id}",
      "name": "{name}",
      "description": "{description}",
      "tags": [
        "{tag}",
        "{tag}"
      ],
      "ownerType": "{owner_type}",
      "status": "{status}",
      "owner": {
        "id": {"id"},
        "name": "{owner_name}"
      },
      "url": "/api/v1/workspaces/:workspaceid",
      "lastModifiedAt": "{last_modified_at}"
	}
  }

Get a Workspace
------------------

::

  GET /api/v1/workspaces/

**Response** ::

  Status: 200 OK

.. code-block:: javascript

  {
    "data": {
      "id": "{id}",
      "name": "{name}",
      "description": "{description}",
      "tags": [
        "{tag}",
        "{tag}"
      ],
      "ownerType": "{owner_type}",
      "status": "{status}",
      "owner": {
        "id": {"id"},
        "name": "{owner_name}"
      },
      "url": "/api/v1/workspaces/:workspaceid"
      "lastModifiedAt": "{last_modified_at}"
    }
  }

Update a Workspace
---------------------

::

  PATCH /api/v1/workspaces/:id

**Optional Parameters**

Only the fields that are updated are needed.

name
  `String` of the workspace name
description
  `String` of the description of the workspace
tags
  `Array of Strings` of the tags
ownerType
  `String` of the owner type
status
  `String` of the status
.. note::
    Add a list of acceptable statuses
owner
  `String` of the slug of the owner
lastModifiedAt
  `Timestamp` of when this object was last edited



The Lizard Datasource REST API
###################################
