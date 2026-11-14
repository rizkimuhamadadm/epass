<div align="center">

# ePass

![License](https://shields.io)
![Category](https://shields.io)
![Maintained](https://shields.io)

A custom Wi-Fi password wordlist containing the most commonly used passwords, numbers, and letter combinations (minimum 8 characters for WPA/WPA2), curated by **Engkq**.

</div>

---

## 📦 Installation

1. Clone this repository to your local machine:
```bash
git clone https://github.com/rizkimuhamadadm/epass.git
cd epass
```

2. Extract the wordlist (if compressed):
```bash
gunzip epass.txt.gz
```

---

## 📶 Wi-Fi Auditing Usage Examples (15 Tools)

You can integrate `epass.txt` with a wide variety of wireless security auditing, handshake cracking, and network testing tools:

### 1. Aircrack-ng
* **Standard WPA/WPA2 Handshake Audit:**
  ```bash
  aircrack-ng -w epass.txt -b AA:BB:CC:DD:EE:FF capture.cap
  ```

### 2. Hashcat (GPU Accelerated)
* **WPA-PBKDF2-PMKID+EAPOL Audit (Mode 22000):**
  ```bash
  hashcat -m 22000 capture.hc22000 epass.txt
  ```
* **Hybrid Rule-Based Audit:**
  ```bash
  hashcat -m 22000 capture.hc22000 epass.txt -r /usr/share/hashcat/rules/best64.rule
  ```

### 3. John the Ripper
* **Convert `.cap` and Run Audit:**
  ```bash
  hcxpcapngtool -o wifi.hash capture.cap
  john --wordlist=epass.txt wifi.hash
  ```
* **Pipe Mutated Passwords Directly to Aircrack-ng:**
  ```bash
  john --wordlist=epass.txt --rules --stdout | aircrack-ng -w - -b AA:BB:CC:DD:EE:FF capture.cap
  ```

### 4. Wifite (Automated Wireless Auditor)
* **Automated WPA/PMKID Audit with `epass.txt`:**
  ```bash
  wifite --wpa --dict epass.txt
  ```

### 5. Cowpatty
* **Audit Capture with Specific SSID:**
  ```bash
  cowpatty -f epass.txt -r capture.cap -s "Target_WiFi_Name"
  ```

### 6. Pyrit
* **Database-Free Passthrough Attack:**
  ```bash
  pyrit -r capture.cap -i epass.txt -b AA:BB:CC:DD:EE:FF attack_passthrough
  ```

### 7. Bettercap (Wi-Fi Recon & Handshake Capture)
* **Automate Handshake Capture to Audit Later with `epass.txt`:**
  ```bash
  bettercap -iface wlan0mon -eval "wifi.recon on; set wifi.handshakes.file capture.pcap; wifi.deauth all"
  ```

### 8. Wacker (WPA3-SAE Online Dictionary Tool)
* **Audit WPA3 Personal Networks Using `epass.txt`:**
  ```bash
  python3 wacker.py --wordlist epass.txt --ssid "Target_WPA3_SSID" --bssid AA:BB:CC:DD:EE:FF --interface wlan0
  ```

### 9. Wpa_supplicant (Direct Live Connection Testing)
* **Test Single/Scripted Passwords Directly Against an Access Point:**
  ```bash
  wpa_passphrase "Target_WiFi_Name" $(head -n 1 epass.txt) > test.conf && wpa_supplicant -i wlan0 -c test.conf
  ```

### 10. WiFi-Brute / nmcli (NetworkManager CLI Scripting)
* **Loop Through `epass.txt` Directly via Linux NetworkManager:**
  ```bash
  while read pass; do nmcli dev wifi connect "Target_WiFi_Name" password "$pass" && echo "Found: $pass" && break; done < epass.txt
  ```

### 11. Crunch (Filtering & Combining with `epass.txt`)
* **Filter Only 8 to 12 Character Passwords Before Auditing:**
  ```bash
  awk 'length($0) >= 8 && length($0) <= 12' epass.txt | aircrack-ng -w - -b AA:BB:CC:DD:EE:FF capture.cap
  ```

### 12. Hashcat-utils (`combinator.bin`)
* **Combine Words Inside `epass.txt` to Create Compound Passphrases:**
  ```bash
  /usr/lib/hashcat-utils/combinator.bin epass.txt epass.txt | aircrack-ng -w - -b AA:BB:CC:DD:EE:FF capture.cap
  ```

### 13. Airgeddon (Multi-Use Wireless Bash Script)
* **Interactive Menu Selection:**
  Select **Handshake Tools Menu** -> **Offline WPA/WPA2 dictionary decryption** -> Enter the full path:
  ```text
  /root/epass/epass.txt
  ```

### 14. Fluxion (WPA/WPA2 Security Auditing Framework)
* **Handshake Verification Path:**
  When prompted for a dictionary to verify captured handshakes, provide the file location:
  ```text
  /root/epass/epass.txt
  ```

### 15. Fern WiFi Cracker (GUI Wireless Auditor)
* **Graphical Interface Selection:**
  Open **Fern WiFi Cracker** -> Select interface & target AP -> Click **Browse** under the wordlist section -> Load **`epass.txt`**.

---

## ⚠️ Disclaimer

This wordlist is intended **strictly for educational purposes and authorized wireless security testing**. 
* Using this wordlist against Wi-Fi networks without explicit, written permission from the network owner is illegal.
* **Engkq** assumes no liability and is not responsible for any misuse or damage caused by this material.

---

## 📝 License

Distributed under the **MIT License**. See `LICENSE` for more information.
