# DeepSea integration test automation script "health-ok.sh"
#
# This script runs DeepSea stages 0-3 (or 0-4, depending on options) to deploy
# a Ceph cluster (with various options to control the cluster configuration).
# After the last stage completes, the script checks for HEALTH_OK.
#
# The script makes no assumptions beyond those listed in README.
#
# After HEALTH_OK is reached, the script also runs various sanity tests
# depending on the options provided.
#
# On success (HEALTH_OK is reached, sanity tests pass), the script returns 0.
# On failure, for whatever reason, the script returns non-zero.
#
# The script produces verbose output on stdout, which can be captured for later
# forensic analysis.
