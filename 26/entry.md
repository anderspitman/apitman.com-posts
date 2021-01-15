This is a dump of everything I've learned about running 64 bit ARM on QEMU.

# General Notes

* I get the feeling that VGA isn't really supported on the -M virt machine.
  Closest I've been able to get is using ramfb, but I still can't start X. I
  think it might be best to use a specific qemu device such as a raspi.

# Alpine aarch64 best settings

```
qemu-system-aarch64 \
    -M virt \
    -cpu cortex-a57 \
    -smp 4 \
    -m 4096M \
    -device ramfb \
    -bios /usr/share/edk2-armvirt/aarch64/QEMU_EFI.fd \
    -device usb-ehci -device usb-mouse -device usb-kbd \
    -drive file=alpine.qcow2
```

# Links

* [Overflow answer][0] that helped me realize I needed a UEFI bios for aarch64
* [Blog post][1] that explained -serial and -nographic. Other useful things as
  well.
* [Graphics explainer][2]
* [Details][3] about different display options
* [Explanation][4] about lack of VGA on ARM.

[0]: https://unix.stackexchange.com/a/623044/183448

[1]: https://fadeevab.com/how-to-setup-qemu-output-to-console-and-automate-using-shell-script/

[2]: https://czak.pl/2020/04/09/three-levels-of-qemu-graphics.html

[3]: https://www.kraxel.org/blog/2019/09/display-devices-in-qemu/

[4]: https://superuser.com/a/717908/402047