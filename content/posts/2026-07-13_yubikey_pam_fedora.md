+++
title = "Protecting Fedora Atomic login with PAM and FIDO2"
weight = 0
updated = 2026-07-14

[taxonomies]
tags = ["linux", "pam", "yubikey", "security", "cryptography", "fedora", "atomic", "fido2"]
+++

## Protecting Fedora logins with FIDO2

As we previously setup our Yubikey with FIDO2 and PIN protection for the challenge there to be used for opening the [systems LUKS partition](@/posts/2026-07-07_yubikey_luks_fedora.md) lets protect our user account with it as well.

Here I shall also instruct on how to setup this on Fedora Atomic spin, but replacing all rpm-ostree commands with dnf commands should do the trick mostly for a standard Fedora Linux.

### Install necessary software

There are two ways to get our Yubikey working with PAM in Fedora. `pam_yubico` and `pam-u2f`. The former requires an internet connection to verify the token from Yubikey cloud which might not always be available for a laptop so I opted to use the u2f PAM module instead.

To layer in all our required depedencies install them and do an system reboot.

```bash
rpm-ostree install pam-u2f fido2-tools pamu2fcfg
systemctl reboot
```

Do not do a live apply here as the pam modules and their configurations are "fragile" in a sense that since we modify files in `/etc` you might lock yourself out if not all is present fully under all circuimstances.

### Create a challenge

The pam module will look into certain path on users home folder for the FIDO2 challenge. First we need to create that path and populate the file 

```bash
mkdir -p ~/.config/Yubico/
pamu2fcfg --pin-verification > ~/.config/Yubico/u2f_keys
```

If you plan to remove password from your user account completely it is recommended that you add another Yubikey token as a backup here. If you primary one gets lost or damaged you might end up locking yourself out of your system.

```bash
pamu2fcfg --nouser >> ~/.config/Yubico/u2f_keys
```

Note: be sure to append via `>>` pipe to the file instead of overwriting it with `>` and losing your primary challenge.

### Enable FIDO2 PAM module

After the challenge is in place and all required software is installed it is time to enable the configuration.

```bash
sudo authselect enable-feature with-pam-u2f
```

#### Test it

Open a new terminal and issue `sudo -k` to invalidate any possible currently open sudo session and then test with `sudo true`. If the configuration is working as expected and you have your Yubikey inserted the system should prompt you for the PIN and then to touch the key.

If the key is not present the system will fallback to password authentication.

### Finalizing

Instead of removing a password completely from your user I recommend instead that you change the password to something really long and complex that you keep on a notepad or in a password manager. Use the password only in emergencies (e.g. lost or damaged Yubikey).

