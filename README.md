autokiosk(1) -- openbox kiosk starter for libvirt, web, rdp and vnc
=============================================

## DESCRIPTION

Openbox based kiosk desktop environment. That can be used to open a URL or
a libvirt domain, as full-screen kiosk application. Automatically
opens simple-kiosk, chromium or virt-viewer, depending on the URI passed.

## CONFIGURATION

Openbox is recommended as a window manager but not required. When using
openbox, autokiosk can be configured by running the autokiosk-init script. Run
this as root before first usage:

`autokiosk-init <TARGET_USER>`

This will configure the autokiosk environment for the specified user. Including
lightdm, openbox, openbox-rc, tint2rc theme and an autostart script to
/etc/xdg/openbox/autostart . Run autokiosk-init on top of a new openbox
installation. Don't run this if you already have a custom desktop.

Please read each file to get a better understanding of what is going on.

autokiosk comes with a custom openbox-rc.xml file that will execute the file
/etc/autokiosk_keys when the keycombo CTRL+SHIFT+F9 to F12 is pressed. To
override what happens when pressing these keys, create the file
'~/.autokiosk_keys' with something like this:

    #!/bin/sh
    case $1 in
    F9)
        xterm
        ;;
    F10)
        another command
        ;;
    F11)
        more commands
        ;;
    F12)
        even more commands
        ;;
    esac

The keycombination CTRL+SHIFT+F8 will run 'autokiosk --close-all'.

To add a custom startup shell script to autokiosk, create the file:
'~/.autokiosk_logon'

## USAGE

Syntax:

`autokiosk` **-h | --help**

`autokiosk` _<TARGET_URI>_ **[ --close | --hide ]**

`<TARGET_URI>` can be:

* `http:<WEBSITE>`
* `https:<WEBSITE>`
* `rdp:<RDP_HOST>`
* `vnc:<VNC_HOST>`
* `<LIBVIRT_DOMAIN>`

`autokiosk` **--close-all | --hide-all | --hide-vms | --hide-vnc | --hide-rdp**

Options explanation:

* `--close` will close a specific processes
* `--hide` will minimize a specific processes

* `--close-all` will close all these processes: simple-kiosk or chromium;
  virt-viewer, rdesktop and xtightvncviewer
* `--hide-all` will minimize all processes (same as above)
* `--hide-vms` will minimize all virt-viewer processes
* `--hide-rdp` will minimize all rdesktop processes
* `--hide-vnc` will minimize all xtightvncviewer processes

Autokiosk will only open one instance of each URL, RDP, VNC or libvirt domain.

Untrusted RDP certificates will be blindly accepted!

To override RDP parameters, you can set the following environment variables:  
AUTOKIOSK_RDP_KEYS: Keyboard Layout, default is the same as the host  
AUTOKIOSK_RDP_RES: Resolution, default is the same as the host  
AUTOKIOSK_RDP_PORT: Remote Desktop Port, default is 3389  
AUTOKIOSK_RDP_USER: Remote Desktop User, default is no user / userless  
AUTOKIOSK_RDP_PASS: Remote Desktop Password, default is no password

To override VNC parameters, you can set the following environment variables:  
AUTOKIOSK_VNC_PORT: VNC Port, default is 5900  
AUTOKIOSK_VNC_PASS: VNC Password, default is no password

To override the libvirt URI, set the LIBVIRT_DEFAULT_URI environment
variable before running autokiosk. Autokiosk will use 'qemu:///system' as
default if this variable is not set.

Log files can be found in ~/.local/share/autokiosk

## EXAMPLE

Open debian.org in simple-kiosk or Chromium full-screen:

    $ autokiosk https://www.debian.org/

Open a VM named my.domain in virt-viewer fullscreen:

    $ autokiosk my.domain

Open a Remote Desktop session to winhost.aa in fullscreen:

    $ autokiosk rdp:winhost.aa

Close the just opened kiosk windows

    $ autokiosk https://www.debian.org/ --close
    $ autokiosk my.domain --close
    $ autokiosk rdp:winhost.aa --close

Close all kiosk windows:

    $ autokiosk --close-all

Minimize the virt-viewer process with the title 'my.domain':

    $ autokiosk my.domain --hide

Minimize all virt-viewer processes:

    $ autokiosk --hide-all

Open a VNC session with a custom password:

    $ export AUTOKIOSK_VNC_PASS=secret
    $ autokiosk vnc:winhost.aa

## COPYRIGHT

See license file

## SEE ALSO

openbox(1), simple-kiosk(1), chromium(1), virt-viewer(1), rdesktop(1),
xtightvncviewer(1)
