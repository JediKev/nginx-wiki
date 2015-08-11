Nginx systemd service file
==========================

Should work on Fedora, OpenSUSE, Arch Linux. Tested on Fedora 16 and 17.

The location of the PIDFile and the nginx binary may be different depending on how nginx was compiled.

Save this file as ``/lib/systemd/system/nginx.service``

.. code-block:: ini

    [Unit]
    Description=The nginx HTTP and reverse proxy server
    After=syslog.target network.target remote-fs.target nss-lookup.target

    [Service]
    Type=forking
    PIDFile=/run/nginx.pid
    ExecStartPre=/usr/sbin/nginx -t
    ExecStart=/usr/sbin/nginx
    ExecReload=/bin/kill -s HUP $MAINPID
    ExecStop=/bin/kill -s QUIT $MAINPID
    PrivateTmp=true

    [Install]
    WantedBy=multi-user.target
