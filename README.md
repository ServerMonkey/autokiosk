autokiosk(1) -- openbox kiosk starter for libvirt and web
=============================================

## DESCRIPTION

Open a URL or libvirt domain, as full-screen kiosk application. Automatically
opens simple-kiosk, chromium or virt-viewer, depending on the URI passed.

## USAGE

Syntax:

`autokiosk -h, --help`

`autokiosk [<URL>|<LIBVIRT_DOMAIN>|close-all|hide-all|hide-vms] [close|hide]`

* Will only open one instance of the URL or libvirt domain
* Best used with openbox

* `close` will close a specific processes
* `hide` will minimize a specific processes
* `close-all` will close all simple-kiosk, chromium and virt-viewer processes
* `hide-all` will minimize all simple-kiosk, chromium and virt-viewer processes
* `hide-vms` will minimize all virt-viewer processes

## EXAMPLE

Open debian.org in simple-kiosk or Chromium full-screen:

    $ autokiosk https://www.debian.org/

Open a VM named my.domain in virt-viewer fullscreen:

    $ autokiosk my.domain

Close the just opened kiosk windows

    $ autokiosk www.debian.org close
    $ autokiosk my.domain close

Quit every simple-kiosk, Chromium and virt-viewer process:

    $ autokiosk close-all

Minimize the virt-viewer process with the title 'my.domain':

    $ autokiosk my.domain hide

Minimize all virt-viewer processes:

    $ autokiosk hide-all

## COPYRIGHT

See license file

## SEE ALSO

openbox(1), simple-kiosk(1), chromium(1), virt-viewer(1)
