# Jinteia on Linux

Run **Nihor2 / Chronicles of Jinteia** on Linux with Lutris using a custom Proton build.

> **Status:** Public Beta  
> **Runner:** `Jinteia-Proton-0.1`  
> **Base:** GE-Proton 11-7  
> **Confirmed working:** CachyOS, Linux Mint 22.3 with Lutris + UMU  
> **Architecture:** x86_64

This setup uses the **Jinteia Patcher** as the main entry point.  
The patcher can be used both to **download/install the game** and to **launch an existing installation**.

---

## Recommended setup

For most users, only one Lutris entry is needed:

```text
Jinteia Patcher
├── Runner: Jinteia-Proton-0.1
└── Prefix: ~/Games/jinteia-prefix
```

The patcher can then handle the game itself.

If you already have the game files and want to launch the client directly from Lutris, you can optionally add a second entry later.

---

## 1. Download Jinteia-Proton

Go to the **Releases** section of this repository and download:

```text
Jinteia-Proton-0.1-installer.run
```

If the release also contains:

```text
Jinteia-Proton-0.1-installer.run.sha256
```

place both files in the same folder and optionally verify the download with:

```bash
sha256sum -c Jinteia-Proton-0.1-installer.run.sha256
```

---

<details>
<summary><strong>2. Install Jinteia-Proton</strong></summary>

Open a terminal in the folder containing:

```text
Jinteia-Proton-0.1-installer.run
```

Make the installer executable:

```bash
chmod +x Jinteia-Proton-0.1-installer.run
```

Then run it:

```bash
./Jinteia-Proton-0.1-installer.run
```

If your system does not allow launching it directly, you can also use:

```bash
bash Jinteia-Proton-0.1-installer.run
```

The installer automatically extracts and installs `Jinteia-Proton-0.1` into the appropriate Lutris runner directory.

Typical locations are:

**Regular Lutris:**

```text
~/.local/share/lutris/runners/wine/Jinteia-Proton-0.1/
```

**Flatpak Lutris:**

```text
~/.var/app/net.lutris.Lutris/data/lutris/runners/wine/Jinteia-Proton-0.1/
```

After the installer finishes:

1. Fully close Lutris
2. Start Lutris again
3. `Jinteia-Proton-0.1` should now be available as a Wine version

> The installer only installs the custom Proton runner. It does **not** install Jinteia itself or Microsoft Edge WebView2 Runtime.

</details>

---

<details>
<summary><strong>3. Set up the Wine/Proton prefix</strong></summary>

Recommended prefix:

```text
~/Games/jinteia-prefix
```

Which normally expands to:

```text
/home/YOUR-USERNAME/Games/jinteia-prefix
```

You do not need to create it manually. Lutris/Proton will create it when needed.

If you later add a separate Jinteia Client entry, use this **same prefix** there as well.

</details>

---

<details open>
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

**Executable:**

```text
/PATH/TO/JINTEIA/Nihor2-Patcher.exe
```

**Wine prefix:**

```text
/home/YOUR-USERNAME/Games/jinteia-prefix
```

**Working directory:**

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
<summary><strong>5. Install Microsoft Edge WebView2 Runtime</strong></summary>

The Jinteia patcher requires **Microsoft Edge WebView2 Runtime x64**.

Download the current **Microsoft Edge WebView2 Evergreen Runtime x64** from Microsoft.
https://go.microsoft.com/fwlink/p/?LinkId=2124703

It must be installed into the same prefix used by the Jinteia Patcher:

```text
~/Games/jinteia-prefix
```

### Recommended method

1. Select **Jinteia Patcher** in Lutris
2. Open the Wine menu for that game
3. Choose **Run EXE inside Wine prefix**
4. Select the WebView2 x64 installer
5. Complete the installation

If Wine asks to install **Wine Mono**, choose:

```text
Install
```

Do **not** cancel the Mono installation.

After WebView2 has been installed, fully restart Lutris.

</details>

---

## 6. Install or launch Jinteia

Start:

```text
Jinteia Patcher
```

The first launch may take longer because Proton can initialize:

- the prefix
- DXVK
- shader caches
- WebView2-related components

If the patcher closes on the very first launch, wait for the process to finish and try once more.

### If you do not have the game files yet

Use the Jinteia Patcher to download/install the game.

After the download is complete, continue launching Jinteia through the patcher.

### If you already have the game files

Place/configure the patcher together with your existing Jinteia installation and launch it using the setup above.

If the patcher detects and launches the existing game correctly, no second Lutris entry is required.

---

<details>
<summary><strong>Optional: Add the Jinteia Client directly to Lutris</strong></summary>

This step is **not required** if you are happy launching the game through the patcher.

Add a second locally installed game only if you want a separate direct-launch entry.

**Name:**

```text
Jinteia
```

**Runner:**

```text
Wine
```

### Game options

**Executable:**

```text
/PATH/TO/JINTEIA/Nihor2 - Chronicles of Jinteia - Release.exe
```

**Wine prefix:**

```text
/home/YOUR-USERNAME/Games/jinteia-prefix
```

**Working directory:**

```text
/PATH/TO/JINTEIA/
```

### Runner options

Select:

```text
Jinteia-Proton-0.1
```

Save the entry.

> If you create this optional second entry, it must use the **same prefix** and the **same Jinteia-Proton runner** as the patcher.

</details>

---

## Final configuration

### Recommended

```text
Jinteia Patcher
├── Runner: Jinteia-Proton-0.1
└── Prefix: ~/Games/jinteia-prefix
```

### Optional direct client entry

```text
Jinteia Patcher
├── Runner: Jinteia-Proton-0.1
└── Prefix: ~/Games/jinteia-prefix

Jinteia
├── Runner: Jinteia-Proton-0.1
└── Prefix: ~/Games/jinteia-prefix
```

---

<details>
<summary><strong>Troubleshooting</strong></summary>

### Jinteia-Proton-0.1 does not appear in Lutris

Fully close Lutris and start it again.

For a regular Lutris installation, check:

```bash
ls ~/.local/share/lutris/runners/wine/Jinteia-Proton-0.1/proton
```

For Flatpak Lutris:

```bash
ls ~/.var/app/net.lutris.Lutris/data/lutris/runners/wine/Jinteia-Proton-0.1/proton
```

If the file exists, the runner was installed successfully.

---

### Permission denied when starting the installer

Run:

```bash
chmod +x Jinteia-Proton-0.1-installer.run
./Jinteia-Proton-0.1-installer.run
```

Or launch it through Bash:

```bash
bash Jinteia-Proton-0.1-installer.run
```

---

### The patcher shows a white or blank window

WebView2 is most likely missing from the selected prefix.

Make sure WebView2 was installed into:

```text
~/Games/jinteia-prefix
```

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

### Direct client launch does not work

Make sure the optional client entry uses exactly the same:

```text
Runner: Jinteia-Proton-0.1
Prefix: ~/Games/jinteia-prefix
```

as the patcher.

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

### Confirmed working

- **CachyOS**
- **Linux Mint 22.3**
- Lutris
- UMU
- Jinteia-Proton-0.1
- Microsoft Edge WebView2 Runtime x64
- Jinteia Patcher
- Jinteia Client
- Launching Jinteia through the patcher
- Optional direct client launch using the same prefix

### Not yet fully verified

- SteamOS
- Flatpak Lutris
- Other Linux distributions

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
