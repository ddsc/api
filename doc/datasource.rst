The Lizard Datasource REST API
###################################

Descript of the Lizard Datasource API.

LayerTree
=========

Get a list of the layertrees
----------------------------

::

  GET /api/v1/layertree/   optional: <<sub_folder>>/<<sub_sub_folder>>/<<>>

**Response**::

  Status: 200 OK

.. code-block:: javascript

  {
    data: [
        {id: xx, name: 'folderA', leaf: false, children: [
             {id: xx, name: 'LayerA', leaf:true, icon: 'xxx', ...settings ..},
             {id: xx, name: 'LayerB', leaf:true, icon: 'xxx', ...settings ..}
        ]},
       {id: xx, name: 'folderB', leaf: false, children: [
       ]}
    ]
   }


**Parameters**

include_sub_tree
  ``Boolean``

Layers
=======

Get a list of Layers
-----------------------

These layers are not in a tree structure.

::

  GET /api/v1/layers/

**Response** ::

  Status: 200 OK


.. code-block:: javascript

  {
    count: {int},
    data: [
        {id: xx, name: 'LayerA', leaf:true, icon: 'xxx', ...settings ..},
        {id: xx, name: 'LayerB', leaf:true, icon: 'xxx', ...settings ..},
        {........}
    ]
   }

Get a layer
------------

::

  GET /api/v1/layer/:layer_id


.. code-block:: javascript

  {

    data: {
        id: {{id}},
        name: {{name}},
        ....: .....
    }
   }


Get a Layer's extent
--------------------

::

  GET /api/v1/layer/:layer_id/extent/


**Response** ::

  Status: 200 OK

.. code-block:: javascript


  {
	"layer_id": 104,
	"extent": [100, 100, 10, 10]
  }

Get a Layer's feature info list
-----------------------------------

::

  GET /api/v1/layer/:layer_id/features/


**Response** ::

  Status: 200 OK

.. code-block:: javascript

  {
	"layer_id": 104,
	"features": {
	  "{{feature_name}}": "{{value}}",
	  "{{feature_name2}}": "{{other value}}"
    }
  }

**Parameters**

start en limit
  Parameters voor pagination
filter
  Filter mogelijkheden
order_by
  Parameter waarop lijst is gefilterd
spatial
  Punt en buffer

Get a Layer's specific feature info
------------------------------------

informatie over feature met eventueel link naar aanliggende objection (tijdseries, etc)

::

  GET /api/v1/layer/:layer_id/features/:feature_id



WMS server bij remote WMS servers
=====================================

.. note::
  Why is this a special API?

Get at list of layers from the mapserver
-----------------------------------------

::

  GET /<map_server>/?request=GetMap

**Parameters**

layers
  `Required` List of layer ids

cql_filter
  Filter mogelijkheden
MaxFeatures
  Pagination
StartIndex
  Pagination


Geeft lijst met features en eigenschappen
::

  GET /<map_server>/?request=GetFeatureInfo

**Parameters**

layers en query_layers
  ``Required`` Lijst met LayerMapId's
cql_filter
  Filter mogelijkheden

Geeft lijst met features en eigenschappen
::
  GET /<map_server>/?request=GetLegendGraphic

**Parameters**

layers en query_layers
  ``Required`` Lijst met LayerMapId's
cql_filter
  Filter mogelijkheden
feature_count
  Max aantal features wat terug wordt gegeven

DDSC-portaal
=============

API ingang
----------
Overzicht van ingangen van de API (data entries). Inclusief list met beschikbare base layers en Folders

::

  GET /api/v1/services/

LayerTree
----------

Vergelijkbaar met WMS. Gaat hierbij om remote sensing beelden.


Get a list of BaseLayers
------------------------

::

  GET /api/v1/baselayers/

Get a BaseLayer
--------------
informatie over baseLayer en beschikbare BaseLayerFilters, basis URL

::

  GET /api/v1/baselayers/:base_layer_id/

BaseLayersFilter - lijst met waarden
------------------------------------

lijst met filter waarden

::

  GET /api/v1/baselayer/:baseLayerId/:baseLayerFilterSlug/


**Parameters**

filter

orderby

start

limit

feature lijst
-------------
Lijst met features in layer

::

  GET /baselayers/:baseLayerId/feature/


**Parameters**

base_layer_filter
  base_layer_filters die worden toegepast
start en limit
  Parameters voor pagination
filter
  Filter mogelijkheden
order_by
  Parameter waarop lijst is gefilterd
spatial
  Punt en buffer

feature get
-----------

informatie over feature met eventueel link naar aanliggende objection (tijdseries, etc)

::

  GET /baselayers/:baseLayerId/features/:featureID/

bevat link voor export en grafiek in geval dat tijdserie beschikbaar is

tijdserie
---------

Tijdserie van locatie

::

  GET /baselayers/:baseLayerSlug>/features/:featureId>/timeseries/:timeseriesId/

**Parameters**

start
  Start tijdstip
end
  Eind tijdstip
format
  Formaat (csv, png, ……)

meerdere tijdseries
-------------------
Geeft export van tijdseries

::

  GET /timeseries/


**Parameters**

tijdseries
  ``Required`` Lijst met tijdserie id's
start
  ``Required`` Start tijdstip
end
  ``Required`` Eind tijdstip
format
  ``Required`` export format

Grafieken
---------
Geeft grafiek van tijdseries (in eerste instantie alleen een plaatje. Later ook mogelijkheden voor andere grafiek type). Een uitwerking van deze service is te vinden op [[https://github.com/lizardsystem/lizard-graph/blob/master/README.rst][lizard-graph]]

::

  GET /timeseries/graph/

**parameters**
tijdseries
  Lijst met tijdserie id's
start
  Start tijdstip
end
  Eind tijdstip
format
  export format

WMS/ WFS server voor DDSC
---------------------------

geeft kaartlaag
-----------------
::

  GET /map/?request=GetMap

**Parameters**

layers
  ``Required`` Lijst met LayerMapId's
cql_filter
  Filter mogelijkheden
MaxFeatures, StartIndex
  parameters voor pagination

Get the layer's feature info
------------------------------

::

  GET /map/?request=GetFeatureInfo

**Parameters**

layers en query_layers
  ``Required`` Lijst met LayerMapId's
cql_filter
  Filter mogelijkheden

Get the layer legend
---------------------

::

  GET /map/?request=GetLegendGraphic

**Parameters**
layers en query_layers
  ``Required`` Lijst met LayerMapId's
cql_filter
  Filter mogelijkheden
feature_count
  Max aantal features wat terug wordt gegeven


Annotation
==========

Overzicht van ingangen van de API (data entries). Inclusief list met beschikbare base layers en Folders

::

  GET /api/v1/services/


BaseLayers en BaseLayersFilter
-------------------------------

Vergelijkbaar met DDSC.
Goed nadenken over Id's/slugs waaraan gekoppeld wordt.

Verder ook APi voor opvragen van annotaties van een object en het toevoegen van annotaties.
