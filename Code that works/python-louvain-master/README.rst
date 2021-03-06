Louvain Community Detection
===========================

.. image:: https://travis-ci.org/taynaud/python-louvain.svg?branch=master
    :target: https://travis-ci.org/taynaud/python-louvain

.. image:: https://readthedocs.org/projects/python-louvain/badge/?version=latest
    :target: http://python-louvain.readthedocs.io/en/latest/?badge=latest
    :alt: Documentation Status

Installing
----------

To build and install from source, run

.. code-block:: shell

    python setup.py install

You can also install from pip with

.. code-block:: shell

    pip install python-louvain


The package name on pip is :code:`python-louvain` 
but it is imported as :code:`community` in python. 
More documentation for this module can be found at
`http://python-louvain.readthedocs.io/ <http://python-louvain.readthedocs.io/>`_


Usage
-----

To use as a Python library

.. code-block:: python

    from community import community_louvain
    import matplotlib.cm as cm
    import matplotlib.pyplot as plt
    import networkx as nx

    # load the karate club graph
    G = nx.karate_club_graph()

    # compute the best partition
    partition = community_louvain.best_partition(G)

    # draw the graph
    pos = nx.spring_layout(G)
    # color the nodes according to their partition
    cmap = cm.get_cmap('viridis', max(partition.values()) + 1)
    nx.draw_networkx_nodes(G, pos, partition.keys(), node_size=40, 
                           cmap=cmap, node_color=list(partition.values()))
    nx.draw_networkx_edges(G, pos, alpha=0.5)
    plt.show()



It can also be run on the command line

.. code-block:: bash

     $ community <filename>

where :code:`filename` is a binary file as generated by the
convert utility distributed with the C implementation at 
`https://sites.google.com/site/findcommunities/ <https://sites.google.com/site/findcommunities/>`_
However as this is mostly for debugging purposes its use should be avoided.
Instead importing this library for use in Python is recommended.


Documentation
-------------

You can find documentation at `https://python-louvain.readthedocs.io/ <https://python-louvain.readthedocs.io/>`_

To generate documentation, run

.. code-block:: shell

     pip install numpydoc sphinx
     cd docs
     make

Tests
-----

To run tests, run

.. code-block:: shell

     pip install nose
     python setup.py test
