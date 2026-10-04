# office-windows-setup

# Custom Microsoft Office Installation Guide

A complete, step-by-step guide on how to perform a selective installation of Microsoft Office (e.g., installing only **Word** and **Excel**) using the official **Microsoft Office Deployment Tool (ODT)**.

---

## 📌 Prerequisites

Before beginning, ensure your system meets the following requirements:
* Operating System: **Windows 10** or **Windows 11**
* Active Internet Connection
* Administrator Access on the PC

---

## ⚙️ Step-by-Step Instructions

### Step 1: Remove Conflicting Office Versions
Microsoft does not allow older **MSI (Windows Installer)** versions of Office to coexist with modern **Click-to-Run (ODT)** installations.

1. Press `Win + R` to open the Run dialog.
2. Type `appwiz.cpl` and press **Enter**.
3. Locate any existing Microsoft Office installations (such as *Microsoft Office Professional Plus 2016*).
4. Right-click the installation and click **Uninstall**.
5. **Restart your computer** after uninstallation finishes.

---

### Step 2: Download the Office Deployment Tool (ODT)
1. Download the tool directly from Microsoft:
   * 🔗 [Microsoft Office Deployment Tool](https://www.microsoft.com/en-us/download/details.aspx?id=49117)
2. Create a dedicated folder on your primary drive named `ODT` (e.g., `C:\ODT`).
3. Run `officedeploymenttool.exe` and extract its contents into `C:\ODT`.

---

### Step 3: Create the Custom Configuration File

You can generate the setup XML file either manually or visually.

#### Option A: Visual Generator (Recommended)
1. Visit the [Microsoft Office Customization Tool](https://config.office.com/).
2. Select your architecture (**64-bit** or **32-bit**).
3. Choose your Office Suite (e.g., *Microsoft 365 Apps for Enterprise* or *Office LTSC*).
4. In the **Apps** section, **toggle off** any applications you do not need (such as *Access*, *Publisher*, *Outlook*, or *PowerPoint*). Keep only **Word** and **Excel** turned on.
5. Click **Export** at the top right, select **Keep Current Settings**, and save the file as `Configuration.xml` inside `C:\ODT`.

#### Option B: Manual Configuration
Create a file named `Configuration.xml` in `C:\ODT` using Notepad and paste the following XML structure:

```xml
<Configuration>
  <Add OfficeClientEdition="64" Channel="Current">
    <Product ID="O365ProPlusRetail">
      <Language ID="en-us" />
      <!-- Exclude applications you do NOT wish to install -->
      <ExcludeApp ID="Access" />
      <ExcludeApp ID="Bing" />
      <ExcludeApp ID="Groove" />
      <ExcludeApp ID="Lync" />
      <ExcludeApp ID="OneDrive" />
      <ExcludeApp ID="OneNote" />
      <ExcludeApp ID="Outlook" />
      <ExcludeApp ID="PowerPoint" />
      <ExcludeApp ID="Publisher" />
      <ExcludeApp ID="Teams" />
    </Product>
  </Add>
  <Display Level="Full" AcceptEULA="TRUE" />
</Configuration>
```

---

### Step 4: Verify Folder Directory Structure

Your `C:\ODT` folder should contain the following files:

```text
C:\ODT\
├── setup.exe
└── Configuration.xml
```

---

### Step 5: Execute the Installation

1. Open the Start Menu, search for **Command Prompt**, right-click it, and select **Run as Administrator**.
2. Navigate to your installation folder:
   ```cmd
   cd C:\ODT
   ```
3. Run the configuration command:
   ```cmd
   setup.exe /configure Configuration.xml
   ```
4. Click **Yes** when prompted by User Account Control (UAC).
5. The official Microsoft installer window will appear and start downloading and installing your selected apps.

---

## 🛠️ Troubleshooting

### Error: "We can't install..."
* **Cause:** An older version of Office (such as Office 2016 or 2013) is still installed via MSI installer.
* **Fix:** Go to **Control Panel > Programs and Features**, uninstall the old Office version completely, and reboot your computer before re-running the installation command.

### Command Line Exits Immediately Without Action
* **Cause:** Running `setup.exe Configuration.xml` without the `/configure` parameter.
* **Fix:** Ensure you include `/configure` in your command:
  ```cmd
  setup.exe /configure Configuration.xml
  ```

---

## 📄 License
This repository and documentation are for educational and configuration purposes using official Microsoft deployment utilities.