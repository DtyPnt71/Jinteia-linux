# Jinteia on Linux

Run **Nihor2 / Chronicles of Jinteia** on Linux with Lutris using a custom Proton build.

> **Status:** Public Beta  
> **Runner:** `Jinteia-Proton-0.1`  
> **Base:** GE-Proton 11-7  
> **Tested:** CachyOS + Lutris + UMU  
> **Other distributions:** Not yet fully verified

The goal of this project is to provide a simple Linux setup for both the **Jinteia Patcher** and the **Jinteia Client** using the same Proton runner and the same Wine/Proton prefix.

---

## Quick overview

You need:

- Lutris
- The Jinteia game files
- `Jinteia-Proton-0.1.run` from the **Releases** section
- Microsoft Edge WebView2 Runtime x64
- One shared prefix for both the patcher and the client

Recommended shared prefix:

```text
~/Games/jinteia-prefix
```

Both Lutris entries must use:

```text
Runner: Jinteia-Proton-0.1
Prefix: ~/Games/jinteia-prefix
```

---

## 1. Download Jinteia-Proton

Go to the **Releases** section of this repository and download:

```text
Jinteia-Proton-0.1.tar.gz
```

If a checksum file is provided, you can verify the download with:

```bash
sha256sum -c Jinteia-Proton-0.1.tar.gz.sha256
```

---

<details>
<summary><strong>2. Install Jinteia-Proton</strong></summary>

### Regular Lutris installation

Open a terminal in the folder containing:

```text
Jinteia-Proton-0.1.tar.gz
```

Run:

```bash
mkdir -p ~/.local/share/lutris/runners/wine
tar -xzf Jinteia-Proton-0.1.tar.gz -C ~/.local/share/lutris/runners/wine
```

Afterwards, this directory should exist:

```text
~/.local/share/lutris/runners/wine/Jinteia-Proton-0.1/
```

Verify it with:

```bash
ls ~/.local/share/lutris/runners/wine/Jinteia-Proton-0.1
```

You should see files/folders such as:

```text
proton
files/
```

Then **fully close Lutris and start it again**.

### Lutris installed as Flatpak

If Lutris was installed as a Flatpak, use:

```bash
mkdir -p ~/.var/app/net.lutris.Lutris/data/lutris/runners/wine
tar -xzf Jinteia-Proton-0.1.tar.gz -C ~/.var/app/net.lutris.Lutris/data/lutris/runners/wine
```

Then fully restart Lutris.

> Flatpak support is included in this guide, but it has not yet been tested as thoroughly as the regular Lutris installation.

</details>

---

<details>
<summary><strong>3. Create the shared Wine/Proton prefix</strong></summary>

The patcher and client must use the **same prefix**.

Recommended:

```text
~/Games/jinteia-prefix
```

Which normally expands to:

```text
/home/YOUR-USERNAME/Games/jinteia-prefix
```

You do not need to create it manually. Lutris/Proton will create it when needed.

</details>

---

<details>
<summary><strong>4. Add the Jinteia Patcher to Lutris</strong></summary>

In Lutris:

1. Click **+**
2. Choose **Add locally installed game**
3. Set the name to:

```text
Jinteia Patcher
```

4. Set the runner to:

```text
Wine
```

### Game options

Executable:

```text
/PATH/TO/JINTEIA/Nihor2-Patcher.exe
```

Wine prefix:

```text
/home/YOUR-USERNAME/Games/jinteia-prefix
```

Optional working directory:

```text
/PATH/TO/JINTEIA/
```

### Runner options

Select this Wine version:

```text
Jinteia-Proton-0.1
```

Save the entry.

</details>

---

<details>
<summary><strong>5. Add the Jinteia Client to Lutris</strong></summary>

Add another locally installed game.

Name:

```text
Jinteia
```

Runner:

```text
Wine
```

### Game options

Executable:

```text
/PATH/TO/JINTEIA/Nihor2 - Chronicles of Jinteia - Release.exe
```

Wine prefix:

```text
/home/YOUR-USERNAME/Games/jinteia-prefix
```

Working directory:

```text
/PATH/TO/JINTEIA/
```

### Runner options

Select:

```text
Jinteia-Proton-0.1
```

Save the entry.

</details>

---

<details>
<summary><strong>6. Install Microsoft Edge WebView2 Runtime</strong></summary>

The Jinteia patcher requires **Microsoft Edge WebView2 Runtime x64**.

Download the current **Microsoft Edge WebView2 Evergreen Runtime x64** from Microsoft.

It must be installed into the same prefix used by both Jinteia entries:

```text
~/Games/jinteia-prefix
```

### Recommended method

1. Select **Jinteia Patcher** in Lutris
2. Open the Wine menu for that game
3. Choose **Run EXE inside Wine prefix**
4. Select the WebView2 x64 installer
5. Complete the installation

If Wine asks to install **Wine Mono**:

```text
Choose Install
```

Do **not** cancel the Mono installation.

After WebView2 has been installed, fully restart Lutris.

</details>

---

## 7. First launch

Start the **Jinteia Patcher** first.

The first launch may take longer because Proton can initialize:

- the prefix
- DXVK
- shader caches
- WebView2 related components

If the patcher closes on the very first launch, wait for the process to finish and try once more.

After the patcher works, start:

```text
Jinteia
```

If both applications start correctly, the setup is complete.

---

## Required final configuration

```text
Jinteia Patcher
├── Runner: Jinteia-Proton-0.1
└── Prefix: ~/Games/jinteia-prefix

Jinteia
├── Runner: Jinteia-Proton-0.1
└── Prefix: ~/Games/jinteia-prefix
```

> Do not use separate prefixes for the patcher and client.

---

<details>
<summary><strong>Troubleshooting</strong></summary>

### Jinteia-Proton-0.1 does not appear in Lutris

Fully close and restart Lutris.

For a regular Lutris installation, check:

```bash
ls ~/.local/share/lutris/runners/wine/Jinteia-Proton-0.1/proton
```

For Flatpak Lutris:

```bash
ls ~/.var/app/net.lutris.Lutris/data/lutris/runners/wine/Jinteia-Proton-0.1/proton
```

If the file exists, Lutris should detect the runner after a restart.

---

### The patcher shows a white or blank window

WebView2 is most likely missing from the selected prefix.

Make sure WebView2 was installed into:

```text
~/Games/jinteia-prefix
```

Also verify that both the patcher and client use this exact same prefix.

---

### Wine asks to install Mono

Choose:

```text
Install
```

Do not select Cancel.

---

### The patcher does not work on the first launch

The first run can initialize the prefix, DXVK and WebView2 components.

Try launching the patcher again after the first process has fully exited.

---

### Login or authorization is required again after deleting the prefix

This is expected.

The prefix contains local Windows and WebView2 session data.

Do not delete a working prefix unless necessary.

</details>

---

<details>
<summary><strong>What does Jinteia-Proton change?</strong></summary>

`Jinteia-Proton-0.1` is based on **GE-Proton 11-7**.

The Jinteia-specific compatibility fix changes Wine/Proton so that an internal Wine-generated memory region is no longer left permanently both:

```text
Writable + Executable (RWX)
```

at the same time.

The Jinteia client executable itself is **not modified**.

No Jinteia security checks are disabled or bypassed.

</details>

---

<details>
<summary><strong>Known test status</strong></summary>

Confirmed working:

```text
CachyOS
Lutris
UMU
Jinteia-Proton-0.1
Microsoft Edge WebView2 Runtime x64
Jinteia Patcher
Jinteia Client
Shared prefix
```

Not yet fully verified:

```text
SteamOS
Linux Mint
Flatpak Lutris
Other distributions
Fresh systems with no previous Jinteia prefix
```

Feedback and additional distribution tests are welcome.

</details>

---

<details>
<summary><strong>Credits / Notes</strong></summary>

This project uses a custom Proton build based on:

```text
GE-Proton 11-7
```

Jinteia, GE-Proton, Wine, Valve, Microsoft and Lutris are separate projects and trademarks of their respective owners.

This repository provides a Linux compatibility setup and is not an official Jinteia Linux release.

</details>

---

## Release files

A typical release should contain:

```text
Jinteia-Proton-0.1.tar.gz
Jinteia-Proton-0.1.tar.gz.sha256
```

The README itself stays in the repository as:

```text
README.md
```
