# nvidia-debug

Symptoms of the problem:

1. RHEL 9
2. You have installed the nvidia-driver packages and rebooted the machine.
3. `nvidia-smi` returns the following error: https://forums.developer.nvidia.com/t/nvidia-smi-has-failed-because-it-couldn-t-communicate-with-the-nvidia-driver-after-updating-ubuntu-20-04/170985/2
4. sudo modprobe nvidia returns nothing


How to fix:sudo dkms remove nvidia/545.23.06 --all

1. sudo dkms status to get the VERSION
2. sudo dkms install nvidia/VERSION -k $(uname -r)
3. sudo cp /boot/initramfs-$(uname -r).img /boot/initramfs-$(uname -r).bak.$(date +%m-%d-%H%M%S).img
4. sudo dracut -f -v
5. sudo sync
6. sudo reboot
7. `nvidia-smi`
