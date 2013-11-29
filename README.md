cache-resolver
==============

Describe a graph of dependencies, notify about a change in a dependency and notify the other dependencies that rely on it.

Setup
=====
```

// define an entity to have a cacheable property
var Cachie = require('cachie');
Cachie.entity('Invoice',{
  'total': {
    timeout: inf,
    deps: [
      {
        type: 'event',
        entity: 'InvoiceLineItem',
        event: 'create'
      }
    ]
  }
});

// set the property
cachie.set({
  entity: 'Invoice',
  property: 'total',
  value: 0,
  timeout: inf
});

// get the property
var total = cache.get({entity: 'Invoice', property: 'total'});

// invalidate it
cachie.broadcast({
  entity: 'InvoiceLineItem'
  event: 'create'
});

// add a property to an entity
cachie.entity('Invoice').addProperty('number_of_items',{
  timeout: inf,
  deps: [
    {
      type: 'event',
      entity: 'InvoiceLineItem',
      event: 'create'
    }
  ]
});
}
```  


Expectation
===========
- Ticket record is created, Event.total_sales is invalidated
```
cachie.watch('Model.created','invalidate:Event.total_sales'
- Ticket field refunded is changed, Event.total sales is invalided
- Field on a model changes, broadcasts event about changed field
- Field on a model changes, broadcasts event about model updated
- Model is created, broadcasts event about new Model created
- Register cache key by Model, name and identifiers
- 
