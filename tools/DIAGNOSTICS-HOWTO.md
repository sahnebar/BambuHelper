# How to Send Diagnostics

If something in BambuHelper looks wrong (filament colors, AMS slots, temperatures, anything),
running this short script and emailing the result helps fix it fast.

## What you need

- A computer (Windows, Mac or Linux) on the same network as the printer
- Python 3.8 or newer ([download here](https://www.python.org/downloads/) if you don't have it)
- Your printer powered on

## Steps

**1. Open a terminal in this `tools/` folder.**

  - Windows: Shift + Right-click in the folder, then "Open PowerShell window here"
  - Mac/Linux: right-click the folder, "Open in Terminal"

**2. Install the required packages (one-time, copy-paste):**

```
pip install paho-mqtt curl_cffi
```

**3. Run the diagnostic:**

```
python bambu_diag.py
```

**4. Answer the prompts.** The script will ask:

  - **LAN or Cloud** - pick whichever you use in BambuHelper
  - **LAN mode:** printer IP, Access Code, Serial Number (all on the printer LCD under Settings)
  - **Cloud mode:** your Bambu Lab email + password (and a 2FA code if your account uses it)

That's it. The script does the rest and finishes in about 30 seconds.

**5. Email the results to** **keralots@gmail.com**

  Attach the file the script created in this folder:

  - `pushall_dump.json`

  In the email, briefly describe what looks wrong (one or two sentences is enough).

## Privacy note

- Your password is never saved or sent anywhere except to Bambu Lab's own login server
- `pushall_dump.json` contains your printer's serial number and current state. It does **not**
  contain your password or cloud token. You can open it in any text editor to inspect it
  before sending.

## Troubleshooting

- **`python` not found:** try `python3` instead, or reinstall Python with the
  "Add to PATH" checkbox ticked.
- **`pip` not found:** try `python -m pip install paho-mqtt curl_cffi`
- **Login fails on Cloud mode:** double-check email/password by logging into bambulab.com
  in a browser. If you use 2FA, have your authenticator app or email ready.
- **LAN mode "TCP fail":** printer and computer must be on the same WiFi/network,
  and LAN Only Mode must be enabled on the printer (Settings > LAN Only Mode).
