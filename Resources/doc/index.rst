Getting Started With MsalsasVotingBundle
========================================

This bundle provides a way for voting posts.

Prerequisites
-------------

This version of the bundle requires Symfony 4.0+.

Translations
~~~~~~~~~~~~

If you wish to use default texts provided in this bundle, you have to make
sure you have translator enabled in your config.

.. code-block:: yaml

    # config/packages/translation.yaml

    framework:
        translator: ~

For more information about translations, check `Symfony documentation`_.

Installation
------------

Installation is a quick 6 step process:

1. Download MsalsasVotingBundle using composer
2. Enable the Bundle
3. Create your Reference class (post, article or whatever)
4. Configure the MsalsasVotingBundle
5. Import MsalsasVotingBundle routing
6. Update your database schema

Step 1: Download MsalsasVotingBundle using composer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Require the bundle with composer:

.. code-block:: bash

    $ composer require msalsas/voting-bundle

Composer will install the bundle to your project's ``vendor/msalsas/voting-bundle`` directory.


Step 2: Enable the bundle
~~~~~~~~~~~~~~~~~~~~~~~~~

Enable the bundle in the kernel::

    <?php
    // app/AppKernel.php

    public function registerBundles()
    {
        $bundles = array(
            // ...
            new Msalsas\VotingBundle\MsalsasVotingBundle(),
            // ...
        );
    }

Step 3: Create your Reference class
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The goal of this bundle is to handle votes and clicks for a ``Reference``
(or ``Post``, ``Article`` or whatever) class and persist them to a database (MySql).
Your first job, then, is to create the ``Reference`` class
for your application. This class can look and act however you want: add any
properties or methods you find useful. This is *your* ``Reference`` class.

Step 4: Configure the MsalsasVotingBundle
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Add the following configuration to your ``config/packages/msalsas_voting.yaml`` file.

.. configuration-block::

    .. code-block:: yaml

        # config/packages/msalsas_voting.yaml
        msalsas_voting:
            user_provider: \App\Entity\User # Your ``User`` class
            negative_reasons: # You can override the default reasons with your translation references
                - msalsas_voting.negative_reasons.irrelevant
                - msalsas_voting.negative_reasons.old
                - msalsas_voting.negative_reasons.tiredness
                - msalsas_voting.negative_reasons.sensationalist
                - msalsas_voting.negative_reasons.spam
                - msalsas_voting.negative_reasons.duplicated
                - msalsas_voting.negative_reasons.microblogging
                - msalsas_voting.negative_reasons.erroneous
                - msalsas_voting.negative_reasons.plagiarism


Only user_provider is required to use the bundle:


Step 5: Import MsalsasVotingBundle routing files
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Now that you have activated and configured the bundle, all that is left to do is
import the MsalsasVotingBundle routing file.

.. configuration-block::

    .. code-block:: yaml

        # config/routes/msalsas_voting.yml
        positive_vote:
            path: /vote-positive/{id}
            controller: Msalsas\VotingBundle\Controller\VoteController:votePositive
            methods: POST
        negative_vote:
            path: /vote-negative/{id}
            controller: Msalsas\VotingBundle\Controller\VoteController:voteNegative
            methods: POST

Step 6: Update your database schema
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Now that the bundle is configured, the last thing you need to do is update your
database schema.

Run the following command.

.. code-block:: bash

    $ php bin/console doctrine:schema:update --force

Next Steps
~~~~~~~~~~

Now that you have completed the basic installation and configuration of the
MsalsasVotingBundle, you are ready to learn about more advanced features and usages
of the bundle.

The following documents are available:

.. toctree::
:maxdepth: 1

        displaying_widgets
        clicks_or_views
        routing
        configuration_reference



[1. Displaying widgets][1]
[2. Clicks or views][2]
[3. Routing][3]
[4. Configuration reference][4]

[1]: ./displaying_widgets.rst
[2]: ./clicks_or_views.rst
[3]: ./routing.rst
[4]: ./configuration_reference.rst
