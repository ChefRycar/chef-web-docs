

=====================================================
chef-shell (executable)
=====================================================

.. tag chef_shell

.. This file describes a command or a subcommand for Knife.
.. This file should not be changed in a way that hinders its ability to appear in multiple documentation sets.

chef-shell is a recipe debugging tool that allows the use of breakpoints within recipes. chef-shell runs as an Interactive Ruby (IRb) session. chef-shell supports both recipe and attribute file syntax, as well as interactive debugging features.

.. end_tag

.. tag ctl_chef_shell_24

The chef-shell executable is run as a command-line tool.

.. end_tag

.. note:: .. tag notes_chef_shell_was_shef

          chef-shell is the new name for Shef as of chef-client version 11.0. chef-shell is backwards compatible and aside from the name change, has the same set of functionality as with previous releases.

          .. end_tag

Modes
=====================================================
.. tag chef_shell_modes

.. This file describes a command or a subcommand for Knife.
.. This file should not be changed in a way that hinders its ability to appear in multiple documentation sets.

chef-shell is tool that is run using an Interactive Ruby (IRb) session. chef-shell currently supports recipe and attribute file syntax, as well as interactive debugging features. chef-shell has three run modes:

.. list-table::
   :widths: 200 300
   :header-rows: 1

   * - Mode
     - Description
   * - Standalone
     - Default. No cookbooks are loaded, and the run-list is empty.
   * - Solo
     - chef-shell acts as a chef-solo client. It attempts to load the chef-solo configuration file and JSON attributes. If the JSON attributes set a run-list, it will be honored. Cookbooks will be loaded in the same way that chef-solo loads them. chef-solo mode is activated with the ``-s`` or ``--solo`` command line option, and JSON attributes are specified in the same way as for chef-solo, with ``-j /path/to/chef-solo.json``.
   * - Client
     - chef-shell acts as a chef-client. During startup, it reads the chef-client configuration file and contacts the Chef server to get attributes and cookbooks. The run-list will be set in the same way as normal chef-client runs. chef-client mode is activated with the ``-z`` or ``--client`` options. You can also specify the configuration file with ``-c CONFIG`` and the server URL with ``-S SERVER_URL``.

.. end_tag

Options
=====================================================
.. tag ctl_chef_shell_options

This command has the following syntax:

.. code-block:: bash

   chef-shell OPTION VALUE OPTION VALUE ...

This command has the following options:

``-a``, ``--standalone``
   Run chef-shell in standalone mode.

``-c CONFIG``, ``--config CONFIG``
   The configuration file to use.

``-h``, ``--help``
   Show help for the command.

``-j PATH``, ``--json-attributes PATH``
   The path to a file that contains JSON data.

   .. tag node_ctl_run_list

   .. This file documents specifc behavior related to the -j option in the chef-client, chef-solo, and chef-shell executables.

   Use this option to define a ``run_list`` object. For example, a JSON file similar to:

   .. code-block:: javascript

      "run_list": [
        "recipe[base]",
        "recipe[foo]",
        "recipe[bar]",
        "role[webserver]"
      ],

   may be used by running ``chef-client -j path/to/file.json``.

   In certain situations this option may be used to update ``normal`` attributes.

   .. end_tag

   .. warning:: .. tag node_ctl_attribute

                .. This file documents specifc behavior related to the -j option in the chef-client, chef-solo, and chef-shell executables.

                Any other attribute type that is contained in this JSON file will be treated as a ``normal`` attribute. For example, attempting to update ``override`` attributes using the ``-j`` option:

                .. code-block:: javascript

                   { 
                     "name": "dev-99",
                     "description": "Install some stuff",
                     "override_attributes": {
                       "apptastic": {
                         "enable_apptastic": "false",
                         "apptastic_tier_name": "dev-99.bomb.com"
                       }  
                     }  
                   }

                will result in a node object similar to:

                .. code-block:: javascript

                   { 
                     "name": "maybe-dev-99",
                     "normal": {
                     "name": "dev-99",
                       "description": "Install some stuff",
                       "override_attributes": {
                         "apptastic": {
                           "enable_apptastic": "false",
                           "apptastic_tier_name": "dev-99.bomb.com"
                         }  
                       }  
                     }
                   }

                .. end_tag

``-l LEVEL``, ``--log-level LEVEL``
   The level of logging to be stored in a log file.

``-s``, ``--solo``
   Run chef-shell in chef-solo mode.

``-S CHEF_SERVER_URL``, ``--server CHEF_SERVER_URL``
   The URL for the Chef server.

``-v``, ``--version``
   The version of the chef-client.

``-z``, ``--client``
   Run chef-shell in chef-client mode.

.. end_tag

