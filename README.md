# KAIRO DDoS

A terminal-based HTTP stress tester with an animated ASCII console UI, built on `prompt_toolkit` and `aiohttp`. The header, skull blink animation, and progress bars run at a steady 20 FPS independently of network latency, so the interface never freezes while requests are in flight.

## Preview

![KAIRO Preview](https://i.ibb.co/nhvkvSd/image.png)

## Features

* Animated KAIRO header (blinking skull + red-to-wine color wave)
* Live attack dashboard: total requests, RPS, ok / failed counters, progress bar
* Async HTTP engine — concurrent persistent senders, no blocking batches
* Proxy support (`ip:port` or `user:pass@ip:port`, one per line)
* One-time legal consent stored in `.kairo_config.json`
* Auto-detects `proxy.txt` next to the script
* "Run another attack?" loop after each test
* Clean `Ctrl+C` handling (cancels the attack, keeps the UI alive)

## Requirements

* Python 3.10+
* A UTF-8 terminal with a monospaced font that includes box-drawing glyphs

## Install

```bash
pip install prompt_toolkit aiohttp
```

## Usage

1. (Optional) Create a `proxy.txt` in the same folder as the script:

```text
127.0.0.1:8080
user:pass@10.0.0.1:3128
http://192.168.1.5:8888
```

2. Run the tester:

```bash
python3 attack.py
```

3. Follow the prompts:

```text
[1] proxies  ->  auto-detects proxy.txt (or runs without proxies)
[2] target   ->  domain or IP
[3] power    ->  global concurrency OR requests-per-proxy
[4] duration ->  duration in seconds
```

4. During the test, press `Ctrl+C` to stop early. A final report is shown, then you can run another test.

## Project layout

```text
attack.py            main script
proxy.txt            optional proxy list
.kairo_config.json   auto-generated (stores legal consent)
```

## Notes

* SSL verification is disabled to allow testing of self-signed endpoints.
* No data is sent anywhere except the target you specify.
* The `.kairo_config.json` file only stores `{"terms_accepted": true}`.

---

## Legal notice

This tool is intended **strictly for educational purposes, security research, and authorized stress tests** on infrastructure you own or have **explicit written permission** to test. Running it against systems without prior authorization is illegal and may result in criminal prosecution. The authors assume no liability for misuse — **you are solely responsible for how you use this software.**
