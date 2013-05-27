EdpModuleLayouts
================
Version 1.0 Created by Evan Coury

Introduction
------------

EdpModuleLayouts is a very simple ZF2 module (less than 20 lines) that simply
allows you to specify alternative layouts to use for each module and action.

Usage
-----

Using EdpModuleLayouts is very, very simple. In any module config or autoloaded
config file simply specify the following:

```php
array(
    'module_layouts' => array(
        'ModuleName' => array(
            'default' => 'layout/default-layout',
            'someaction' => 'layout/someAction',
            ),
    ),
);
```

Example usage in an Album module config
----------------------------------------
module/Album/config/module.config.php

```php
return array(
    'controllers' => array(
        'invokables' => array(
            'Album\Controller\Album' => 'Album\Controller\AlbumController',
        ),
    ),
    // The following section is new and should be added to your file
    'router' => array(
        'routes' => array(
            'album' => array(
                'type'    => 'segment',
                'options' => array(
                    'route'    => '/album[/:action][/:id]',
                    'constraints' => array(
                        'action' => '[a-zA-Z][a-zA-Z0-9_-]*',
                        'id'     => '[0-9]+',
                    ),
                    'defaults' => array(
                        'controller' => 'Album\Controller\Album',
                        'action'     => 'index',
                    ),
                ),
            ),
        ),
      ),

    'view_manager' => array(

        'display_not_found_reason' => true,
        'display_exceptions'       => true,
        'doctype'                  => 'HTML5',
        'not_found_template'       => 'error/404',
        'exception_template'       => 'error/index',
        'template_map' => array(
            'layout/album'           => __DIR__ . '/../view/layout/layout.phtml',
            'layout/albumEdit'           => __DIR__ . '/../view/layout/albumEdit.phtml',
            'error/404'               => __DIR__ . '/../view/error/404.phtml',
            'error/index'             => __DIR__ . '/../view/error/index.phtml',
        ),

        'template_path_stack' => array(
            'album' => __DIR__ . '/../view',
        ),
      ),

    'module_layouts' => array(
      'Album' => array(
          'default' => 'layout/album',
          'edit'    => 'layout/albumEdit',
        )
     ),


);

```

The template files are in "module/Album/view/layout"
---------------------------------------------------
albumEdit.phtml
album.phtml
layout.phtml





That's it!
