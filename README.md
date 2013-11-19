hubic-swift
==========

This is a wrapper arround swift to connect to the OAUTH as available
in hubic.

Dependency
----------

You obviously need to have swift to run this as it is only a wrapper.
You also need ruby and some of its gems : mechanize logger and highline.

On debian, 

    apt-get install swift ruby ruby-mechanize ruby-logger ruby-higline

will install everything that is needed. By the way this has only been
tested on Debian, but should work on any recent GNU/Linux.

You also need a `client_id` and `client_secret`. To have them,
register an application in your hubic
[account](https://hubic.com/home/browser/developers/), I use
`http://localhost:4567/` as a redirect_uri. You could use
anything else, but will have to change the value of `REDIRECT_URI` in
the source code.

I also use the `XDG_RUNTIME_DIR` (`echo $XDG_RUNTIME_DIR` to see if it's
configured) and `XDG_CONFIG_HOME` (or ~/.config) to put some config
files. And I use the `xdg-user-dir` (found in the `xdg-user-dirs`
debian package).

Running it
----------
The first time it run, it will ask for your `client_id`,
`client_secret`, and hubic username. It will store those information
in `$XDG_CONFIG_HOME/hubic-swift/creds`. It will also ask your
password to ask hubic for the identifying token swift will use.
It will store in `$XDG_RUNTIME_DIR/hubic-swift` those token for latter
use, and will try to refresh them when needed.

Afterward it will just call swift, so for example

    ./hubic-swift list default

will run

    swift --os-auth-token "somesecret" --os-storage-url "https://somwhere.hubic.com/somepath" list default

then swift will list what is in you default container.

Storing your password
---------------------

If you are fed up to enter your password too often, you can store it
in the creds file. Note that this is unsafe.

Open `$XDG_CONFIG_HOME/hubic-swift/creds`. It will look like

    {"CLIENT_ID":"api_hubic_longstring","CLIENT_SECRET":"xxxxxxxxxxxxxxxxxxxxxx","USERNAME":"me@example.com"}

You have to had `"PASSWD":"mysecretpassword"` there:

    {"CLIENT_ID":"api_hubic_longstring","CLIENT_SECRET":"xxxxxxxxxxxxxxxxxxxxxx","USERNAME":"me@example.com","PASSWD":"mysecretpassword"}

This is unsafe, but I don't now how the official client store this
information, and it might not be safer.

BUGS
----
No error detection is done. The way the hubic and openstack token are
store might be unsafe. I should probably try to find a safe for them. 

If something stop working you could try

    ./hubic-swift --cleanup

to remove the connexion token, and so to force hubic-swift to
reconnect. 

Report any bug to the [github project page](https://github.com/vanicat/hubic-swift/issues?state=open)


COPYING
-------

Copyright © Rémi Vanicat 2013
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions
are met:
1. Redistributions of source code must retain the above copyright
   notice, this list of conditions and the following disclaimer.
2. Redistributions in binary form must reproduce the above copyright
   notice, this list of conditions and the following disclaimer in the
   documentation and/or other materials provided with the distribution.
3. Neither the name of the University nor the names of its contributors
   may be used to endorse or promote products derived from this software
   without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY RÉMI VANICAT AND CONTRIBUTORS ``AS IS''
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
PURPOSE ARE DISCLAIMED.  IN NO EVENT SHALL THE REGENTS OR CONTRIBUTORS
BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR
BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE
OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN
IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.




