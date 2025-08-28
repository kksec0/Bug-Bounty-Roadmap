

## 🔎 Subdomain Enumeration (Passive)

# Subfinder
subfinder -dL domains.txt -o subfinder.txt
subfinder -d inholland.nl -o subfinder.txt

# Amass
amass enum -passive -norecursive -noalts -df domains.txt -o amass.txt

# Assetfinder
echo test.com | assetfinder --subs-only >> asset.txt

# GitHub Subdomains
python github-subdomains.py -t <your-github-token> -d test.com | grep -v '@' | sort -u | grep "\.test.com" >> github-subs.txt

# crt.sh scraping
curl -s https://crt.sh/?q=%25.test.com | grep test.com | grep TD | sed -e 's/<//g' -e 's/>//g' -e 's/TD//g' -e 's/\///g' -e 's/ //g' | sed -n '1!p' | sort -u >> crt.txt

# Crtfinder
python3 crtfinder.py -u alloyhome.com

# Sublist3r
sublist3r -d safesavings.com -o sublist3r.txt

# Google dork
site:*.ibm.com -site:www.ibm.com
```

---

## 📂 Merge Subdomains into One File

```
cat subfinder.txt amass.txt asset.txt github-subs.txt crt.txt | anew all-subs.txt
```

---

## 🌐 Find Live Subdomains

```
cat all-subs.txt | httpx -o live-subs.txt
```

---

## 🚪 Active Subdomain Enumeration (Bruteforce)

```
# FFUF
ffuf -u "https://FUZZ.kaggle.com" -w best-dns-wordlist.txt -mc 200,403,404,302,301

# Gobuster
gobuster dns -d test.com -t 50 -w 2m-subdomains.txt -q -o g.txt

# Puredns
puredns bruteforce Subdomain.txt test.com resolvers.txt
```

📚 Wordlists: [https://wordlists.assetnote.io/](https://wordlists.assetnote.io/)

---

## 🏴 Subdomain Takeover

```bash
# Nuclei
nuclei -t /root/nuclei-templates/takeovers/ -l live-subs.txt

# Subzy
subzy run --targets live-subs.txt
```

---

## 🔗 Collecting URLs & Parameters

```bash
# Waymore (collect URLs from multiple sources)
waymore -i example.com -mode U -oU result.txt
cat result.txt | sort -u > sorted.txt

# Get live URLs
cat sorted.txt | httpx -mc 200 -o live-urls.txt

# Extract parameters
cat live-urls.txt | grep "=" > live-parameters.txt
```

➡️ Results: `params.txt`, `js-files.txt`, `github-urls.txt`

---

## 📜 JS Hunting

```bash
# Collect JS files
katana -u https://www.example.com | grep ".js$" | httpx -mc 200 | sort -u | tee js-files.txt
echo example.com | gau | grep ".js$" | httpx -mc 200 | sort -u | tee -a js-files.txt
cat waymore.txt | grep ".js$" | httpx -mc 200 | sort -u | tee -a js-files.txt

# Analyze JS files
cat js-files.txt | jscracker | tee jscracker-result.txt
nuclei -l js-files.txt -t /root/nuclei-templates/http/exposures/ | tee nuclei-result.txt
python3 JSScanner.py
python3 main.py -u https://example.com | tee pinkerton-result.txt
```

---

## 🧪 Vulnerability Hunting

### XSS

```bash
cat params.txt | Gxss -c 100 -p Xss | sort -u | dalfox pipe
```

### SQLi

```bash
sqlmap -m param.txt --batch --random-agent --level 1 | tee sqlmap.txt
```

### SSTI

```bash
./tplmap.py -u "domain.com/?parameter=SSTI*"
```

### CORS Misconfiguration

```bash
corscanner -i live_subdomains.txt -v -t 100
```

### Open Redirect

```bash
waybackurls tesorion.nl | grep -a -i \=http | qsreplace 'evil.com' | while read host; do curl -s -L $host -I| grep "evil.com" && echo "$host Vulnerable"; done
```

---

## ⚡ Port Scanning

```bash
# Masscan
masscan -p0-79,81-442,444-65535 -iL live-ips.txt --rate=10000 -oB temp

# Naabu
naabu -rate 10000 -l live-hosts.txt -silent

# Nmap
nmap -Pn -sV -iL live-hosts.txt -oN scanned-port.txt --script=vuln
```

---

## 🚀 Automated Scanning with Nuclei

```bash
nuclei -list live-subs.txt \
  -t /root/nuclei-templates/vulnerabilities \
  -t /root/nuclei-templates/cves \
  -t /root/nuclei-templates/exposures \
  -t /root/nuclei-templates/sqli.yaml
```

---

## ✅ Manual Checklist

* CSRF
* IDORs
* Business Logic Vulnerabilities
* API Testing
* SQL Injection
* XSS

---

## 📌 Resources & Tools

* [Amass](https://github.com/OWASP/Amass)
* [Subfinder](https://github.com/projectdiscovery/subfinder)
* [Httpx](https://github.com/projectdiscovery/httpx)
* [FFUF](https://github.com/ffuf/ffuf)
* [Nuclei](https://github.com/projectdiscovery/nuclei)
* [Dirsearch](https://github.com/maurosoria/dirsearch)
* [SQLMap](http://sqlmap.org/)
* [Waymore](https://github.com/xnl-h4ck3r/waymore)
* [Dalfox](https://github.com/hahwul/dalfox)
* [Katana](https://github.com/projectdiscovery/katana)
* [ParamSpider](https://github.com/devanshbatham/ParamSpider)
* [Masscan](https://github.com/robertdavidgraham/masscan)
* [Naabu](https://github.com/projectdiscovery/naabu)

---

🔻 **Author:** [kksec0](https://github.com/kksec0)

---
 
