Events
======

Events

 * `loop.startup`
 * `loop.shutdown`
 * `pre.dispatch`
 * `post.dispatch`
 
Hooks
-----

The `loop.startup` and `loop.shutdown` is called once at the start and at the
end of the simple-mvc workflow.

The `pre.dispatch` and `post.dispatch` is called for every controlled pushed 
onto the stack (use the `then()` method).

Hooks params
~~~~~~~~~~~~

The `loop.startup` and the `loop.shutdown` have the `Application` object as 
first parameter.

The `pre.dispatch` hook has the `Route` object as first parameter and the
`Application` object as second.

The `post.dispatch` hook has the `Controller` object as first paramter.

 * The router object is useful for modify the application flow.
 
.. code-block:: php
    :linenos:

    <?php
    $app->getEventManager()->subscribe("pre.dispatch", function($router, $app) {
        // Use a real and better auth system
        if ($_SESSION["auth"] !== true) {
            $router->setControllerName("admin");
            $router->setActionName("login");
        
            $app->getBootstrap("layout")->setScriptName("admin.phtml");
        }
    });

Create new events
-----------------

.. code-block:: php
    :linenos:

    <?php
    // Call the hook named "my.hook" and pass the app as first arg.
    $app->getEventManager()->publish("my.hook", array($app));

You can use the self-created hook using

.. code-block:: php
    :linenos:

    <?php
    $app->getEventManager()->subscribe("my.hook", function($app) {/*The body*/});


