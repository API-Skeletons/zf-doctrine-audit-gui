ORM Audit for Doctrine View Layer
=================================

This is a complimentary module for api-skeletons/zf-doctrine-audit and provides a view layer for 
browsing the audit record.


Identifier column values from the audited entity will be added to defaults to generate urls through routing.

```
    <?php
        $options = $this->auditEntityOptions($revisionEntity->getTargetEntityClass());
        $routeOptions = array_merge($options['defaults'], $revisionEntity->getEntityKeys());
    ?>
    <a class="btn btn-info" href="<?=
        $this->url($options['route'], $routeOptions);
    ?>">Data</a>
```

This is how to map from your application to it's current revision entity:

```
    <a class="btn btn-info" href="<?=
        $this->url('audit/revision-entity',
            array(
                'revisionEntityId' => $this->auditCurrentRevisionEntity($auditedEntity)->getId()
            )
        );
    ?>">
        <i class="icon-list"></i>
    </a>
```


View Helpers
------------

Return the audit service.  This is a helper class.  The class is also available via dependency injection factory ```auditService```
This class provides the following:

1. setComment();
    Set the comment for the next audit transaction.  When a comment is set it will be read at the time the audit Revision is created and added as the comment.

2. getAuditEntityValues($auditEntity);
    Returns all the fields and their values for the given audit entity.  Does not include many to many relations.

3. getEntityIdentifierValues($entity);
    Return all the identifying keys and values for an entity.

4. getRevisionEntities($entity)
    Returns all RevisionEntity entities for the given audited entity or RevisionEntity.

````
$view->auditService();
```

Return the latest revision entity for the given entity.
