.. _service-radarr-troubleshooting:

Troubleshooting
###############

Add Pre-existing Series to Radarr
*********************************

#. Existing files should be in a folder for each movie.
#. :cmdmenu:`Movie --> Bulk Import Movies --> /data/movies`
#. Be sure to set appropriate import behavior.
#. Be sure to search for correct match for episode if needed.
#. Import may timeout if initial import library is large. Restart import.

   :cmdmenu:`Movies --> Update Library`.

Ensure no Duplicate Plex Updates
********************************
Plex will trigger updates on ``inotify`` events if configured to do so. If that
is the case: :cmdmenu:`Connect --> Plex --> Update Library --> Disable`.

Otherwise duplicate items will appear on single files.

Failures with TMdb
******************
These are DNS resolution failures. Generally these happened because of rate
limiting due to large number of changes at one time. See
:ref:`service-pihole-troubleshooting-rate-limit`. Upgrade system packages to
ensure the latest mono project certificates are installed as well.

.. code-block:: bash
  apt update && apt upgrade
