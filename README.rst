health-ok.sh
============

DeepSea integration test automation script


Overview
--------

This script runs DeepSea stages 0-3 (or 0-4, depending on options) to deploy
a Ceph cluster (with various options to control the cluster configuration).
After the last stage completes, the script checks for HEALTH_OK.

The script makes no assumptions beyond those listed below, under "Assumptions".

After HEALTH_OK is reached, the script also runs various sanity tests
depending on the options provided.

On success (HEALTH_OK is reached, sanity tests pass), the script returns 0.
On failure, for whatever reason, the script returns non-zero.

The script produces verbose output on stdout, which can be captured for later
forensic analysis.

The script's entry point is ``health-ok.sh``, which is an executable file.
That file uses ``source`` to run several helper scripts, which are located
in the ``common/`` subdirectory.


Assumptions
-----------

1. there are at least two test nodes (VMs or physical machines) that are
running the same OS (e.g. Leap 42.3) and can see eachother over the network. 
2. all the test nodes are configured as a Salt cluster, i.e.: one node is
configured as both a master and a minion, the remaining nodes are configured
as minions only, the master can "salt '*' test.ping" all the minions, and 
it is desirable for the script to deploy a Ceph cluster across all the minions
(``deepsea_minions: *``)
3. the nodes have at least one external drive (>= 10GB) for OSD and there are
at least four OSDs, total, in the cluster
4. the DeepSea code under test has already been installed on the master node
5. the Ceph repos have already been set up on all nodes, so DeepSea can install
the RPMs it needs


Caveats
-------

1. Ceph will not work properly unless the nodes have (at least) short
hostnames. That means the health-ok.sh script won't pass, either. There are two
options: ``/etc/hosts`` or DNS
2. Node targeting: DeepSea suite sets ``deepsea_minions: *`` in
``/srv/pillar/ceph/deepsea_minions.sls``. Just something to keep in mind.
