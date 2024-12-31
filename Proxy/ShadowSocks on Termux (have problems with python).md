
give me command to isntall Shadowsocks server on termux and working with tcp and udp

###### ChatGPT said:

ChatGPT

To install and set up **Shadowsocks** server on **Termux** with support for both TCP and UDP, follow these steps:

### 1. **Install Dependencies**

First, you'll need to install the required dependencies in Termux.

Open Termux and run the following commands to update packages and install the necessary dependencies:

bash

Copy code

`pkg update pkg install python python-dev clang make git`

### 2. **Install Shadowsocks Server**

You can install **Shadowsocks** using **Python** since it's available via **pip** (Python's package manager). Run the following command:

bash

Copy code

`pip install shadowsocks`

### 3. **Configure Shadowsocks**

Once installed, you can configure the Shadowsocks server by creating a configuration file.

1. Create a directory for Shadowsocks configuration:
    
    bash
    
    Copy code
    
    `mkdir -p ~/shadowsocks cd ~/shadowsocks`
    
2. Create a configuration file named `config.json`:
    
    bash
    
    Copy code
    
    `nano config.json`
    
    Add the following configuration to the `config.json` file:
    
    json
    
    Copy code
    
    `{     "server": "0.0.0.0",  # Listen on all interfaces     "server_port": 1080,   # You can choose another port     "local_address": "127.0.0.1",     "local_port": 1080,    # Local port for the client     "password": "your_password_here",  # Set your password     "timeout": 300,     "method": "aes-256-cfb",  # Encryption method, can choose other options     "fast_open": false,     "workers": 1 }`
    
    Replace `"your_password_here"` with a secure password of your choice.
    

### 4. **Run the Shadowsocks Server**

After configuring, run the Shadowsocks server with the following command:

bash

Copy code

`ssserver -c ~/shadowsocks/config.json`

This will start the Shadowsocks server and it will be listening on port **1080** (or whatever port you configured). The server will support both **TCP** and **UDP** traffic.

### 5. **Verify UDP Support**

Shadowsocks supports UDP traffic by default through its protocol. You don’t need additional configuration to enable UDP. To test UDP traffic, you can use a compatible Shadowsocks client (on Android, PC, etc.) that is configured to use the same server settings.

### 6. **Optional: Run Shadowsocks Server in the Background**

If you want to run the Shadowsocks server in the background, use **nohup** or **tmux**:

Using **nohup**:

bash

Copy code

`nohup ssserver -c ~/shadowsocks/config.json &`

Or using **tmux**:

bash

Copy code

`tmux new-session -d -s shadowsocks 'ssserver -c ~/shadowsocks/config.json'`

### 7. **Firewall / NAT Settings**

If you're running this server on an Android device, make sure that any firewall or NAT (Network Address Translation) settings allow traffic to pass through the port you've chosen (1080 or any other custom port). You might also need to configure port forwarding if running this in a network with a router.

---

This setup will allow you to run a Shadowsocks server on your Android device (via Termux), and it will support both TCP and UDP connections.

Let me know if you encounter any issues during installation or setup!

4o mini

##### You said:

~/shadowsocks $ ssserver -c ~/shadowsocks/config.json Traceback (most recent call last): File "/data/data/com.termux/files/usr/bin/ssserver", line 5, in <module> from shadowsocks.server import main File "/data/data/com.termux/files/usr/lib/python3.12/site-packages/shadowsocks/server.py", line 27, in <module> from shadowsocks import shell, daemon, eventloop, tcprelay, udprelay, \ File "/data/data/com.termux/files/usr/lib/python3.12/site-packages/shadowsocks/udprelay.py", line 71, in <module> from shadowsocks import encrypt, eventloop, lru_cache, common, shell File "/data/data/com.termux/files/usr/lib/python3.12/site-packages/shadowsocks/lru_cache.py", line 34, in <module> class LRUCache(collections.MutableMapping): ^^^^^^^^^^^^^^^^^^^^^^^^^^ AttributeError: module 'collections' has no attribute 'MutableMapping' ~/shadowsocks $

###### ChatGPT said:

ChatGPT

The error you're seeing (`AttributeError: module 'collections' has no attribute 'MutableMapping'`) is caused by a change in Python 3.10 and later, where `MutableMapping` was moved from `collections` to `collections.abc`.

To fix this issue, you can edit the Shadowsocks source code or modify the dependencies to be compatible with the version of Python you're using.

### Option 1: Modify the `lru_cache.py` File

You can directly modify the `lru_cache.py` file in the Shadowsocks source code to make it compatible with Python 3.10+.

1. Open the `lru_cache.py` file in the Shadowsocks directory:
    
    bash
    
    Copy code
    
    `nano /data/data/com.termux/files/usr/lib/python3.12/site-packages/shadowsocks/lru_cache.py`
    
2. In the `lru_cache.py` file, look for the line where `MutableMapping` is imported from `collections`. It will look like this:
    
    python
    
    Copy code
    
    `from collections import MutableMapping`
    
3. Change it to:
    
    python
    
    Copy code
    
    `from collections.abc import MutableMapping`
    
4. Save and close the file (`CTRL + X`, then press `Y` and `Enter` to confirm).
    

### Option 2: Reinstall Shadowsocks with Python 3.9 or Lower

If modifying the file doesn’t resolve the issue or you prefer an easier approach, you could try using Python 3.9 or lower. To install an older version of Python on Termux:

1. Uninstall the current Python version:
    
    bash
    
    Copy code
    
    `pkg uninstall python`
    
2. Install Python 3.9:
    
    bash
    
    Copy code
    
    `pkg install python3.9`
    
3. Then reinstall Shadowsocks using the older Python version:
    
    bash
    
    Copy code
    
    `pip install shadowsocks`
    
4. Try running the server again with:
    
    bash
    
    Copy code
    
    `ssserver -c ~/shadowsocks/config.json`
    

### Option 3: Use a Shadowsocks Package from a Different Source

Alternatively, you could try using a precompiled version of Shadowsocks from a repository that supports your version of Python.

---

Let me know if you need further assistance!

4o mini

##### You said:

* `nano /data/data/com.termux/files/usr/lib/python3.12/site-packages/shadowsocks/lru_cache.py`

i edited after that again have error .../site-packages/shadowsocks $ ssserver -c ~/shadowsocks/config.json Traceback (most recent call last): File "/data/data/com.termux/files/usr/bin/ssserver", line 5, in <module> from shadowsocks.server import main File "/data/data/com.termux/files/usr/lib/python3.12/site-packages/shadowsocks/server.py", line 27, in <module> from shadowsocks import shell, daemon, eventloop, tcprelay, udprelay, \ File "/data/data/com.termux/files/usr/lib/python3.12/site-packages/shadowsocks/udprelay.py", line 71, in <module> from shadowsocks import encrypt, eventloop, lru_cache, common, shell File "/data/data/com.termux/files/usr/lib/python3.12/site-packages/shadowsocks/lru_cache.py", line 34, in <module> class LRUCache(collections.MutableMapping): ^^^^^^^^^^^^^^^^^^^^^^^^^^ AttributeError: module 'collections' has no attribute 'MutableMapping' .../site-packages/shadowsocks $

###### ChatGPT said:

ChatGPT

It looks like the issue is persisting even after modifying the `lru_cache.py` file, indicating that there might still be other places in the Shadowsocks code where `collections.MutableMapping` is used.

To fully resolve this, let's search for all instances of `MutableMapping` in the Shadowsocks code and update them to use `collections.abc.MutableMapping` instead. Here's how you can proceed:

### Steps to Fix the Issue:

1. **Search for all `MutableMapping` references:**
    
    You can search through the Shadowsocks code to find all occurrences of `MutableMapping` and update them to `collections.abc.MutableMapping`.
    
    Run this command in Termux to find all occurrences:
    
    bash
    
    Copy code
    
    `grep -r "MutableMapping" /data/data/com.termux/files/usr/lib/python3.12/site-packages/shadowsocks/`
    
2. **Edit the necessary files:**
    
    For each file that contains the reference to `MutableMapping`, you need to change the import from `collections` to `collections.abc`. For example:
    
    - **Before**:
        
        python
        
        Copy code
        
        `from collections import MutableMapping`
        
    - **After**:
        
        python
        
        Copy code
        
        `from collections.abc import MutableMapping`
        
    
    You can manually edit these files using `nano`:
    
    bash
    
    Copy code
    
    `nano /data/data/com.termux/files/usr/lib/python3.12/site-packages/shadowsocks/<file_name>.py`
    
    Make the necessary changes and save the files.
    
3. **Check if there are other Python 3.10+ compatibility issues:**
    
    If you continue to face issues, it might be helpful to check for other potential compatibility problems with Python 3.10 or higher. You could try using an earlier Python version (like 3.9) as an alternative if this doesn’t work.
    

---

Once you've updated all instances of `MutableMapping`, try running the Shadowsocks server again:

bash

Copy code

`ssserver -c ~/shadowsocks/config.json`

Let me know if you encounter further issues!

4o mini

##### You said:

.../site-packages/shadowsocks $ cat lru_cache.py #!/usr/bin/python # -*- coding: utf-8 -*- # # Copyright 2015 clowwindy # # Licensed under the Apache License, Version 2.0 (the "License"); you may # not use this file except in compliance with the License. You may obtain # a copy of the License at # # http://www.apache.org/licenses/LICENSE-2.0 # # Unless required by applicable law or agreed to in writing, software # distributed under the License is distributed on an "AS IS" BASIS, WITHOUT # WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the # License for the specific language governing permissions and limitations # under the License. from __future__ import absolute_import, division, print_function, \ with_statement import collections import logging import time # this LRUCache is optimized for concurrency, not QPS # n: concurrency, keys stored in the cache # m: visits not timed out, proportional to QPS * timeout # get & set is O(1), not O(n). thus we can support very large n # TODO: if timeout or QPS is too large, then this cache is not very efficient, # as sweep() causes long pause class LRUCache(collections.MutableMapping): """This class is not thread safe""" def __init__(self, timeout=60, close_callback=None, *args, **kwargs): self.timeout = timeout self.close_callback = close_callback self._store = {} self._time_to_keys = collections.defaultdict(list) self._keys_to_last_time = {} self._last_visits = collections.deque() self._closed_values = set() self.update(dict(*args, **kwargs)) # use the free update to set keys def __getitem__(self, key): # O(1) t = time.time() self._keys_to_last_time[key] = t self._time_to_keys[t].append(key) self._last_visits.append(t) return self._store[key] def __setitem__(self, key, value): # O(1) t = time.time() self._keys_to_last_time[key] = t self._store[key] = value self._time_to_keys[t].append(key) self._last_visits.append(t) def __delitem__(self, key): # O(1) del self._store[key] del self._keys_to_last_time[key] def __iter__(self): return iter(self._store) def __len__(self): return len(self._store) def sweep(self): # O(m) now = time.time() c = 0 while len(self._last_visits) > 0: least = self._last_visits[0] if now - least <= self.timeout: break if self.close_callback is not None: for key in self._time_to_keys[least]: if key in self._store: if now - self._keys_to_last_time[key] > self.timeout: value = self._store[key] if value not in self._closed_values: self.close_callback(value) self._closed_values.add(value) for key in self._time_to_keys[least]: self._last_visits.popleft() if key in self._store: if now - self._keys_to_last_time[key] > self.timeout: del self._store[key] del self._keys_to_last_time[key] c += 1 del self._time_to_keys[least] if c: self._closed_values.clear() logging.debug('%d keys swept' % c) def test(): c = LRUCache(timeout=0.3) c['a'] = 1 assert c['a'] == 1 time.sleep(0.5) c.sweep() assert 'a' not in c c['a'] = 2 c['b'] = 3 time.sleep(0.2) c.sweep() assert c['a'] == 2 assert c['b'] == 3 time.sleep(0.2) c.sweep() c['b'] time.sleep(0.2) c.sweep() assert 'a' not in c assert c['b'] == 3 time.sleep(0.5) c.sweep() assert 'a' not in c assert 'b' not in c global close_cb_called close_cb_called = False def close_cb(t): global close_cb_called assert not close_cb_called close_cb_called = True c = LRUCache(timeout=0.1, close_callback=close_cb) c['s'] = 1 c['s'] time.sleep(0.1) c['s'] time.sleep(0.3) c.sweep() if __name__ == '__main__': test()

###### ChatGPT said:

ChatGPT

The issue you're encountering with the `MutableMapping` in Python 3.10+ occurs because, in newer Python versions, `MutableMapping` has been moved to `collections.abc`. In the `lru_cache.py` file you showed, the import statement still references `collections` instead of `collections.abc`.

To fix this issue, you'll need to modify the import statement in `lru_cache.py`:

### 1. **Edit `lru_cache.py` to fix the `MutableMapping` import**

Open the `lru_cache.py` file and change the import line for `MutableMapping` from:

python

Copy code

`import collections`

to:

python

Copy code

`from collections.abc import MutableMapping`

This ensures that the code uses the correct location for `MutableMapping` in Python 3.10+.

### 2. **Save the file**

After making this change, save the file and then try running the Shadowsocks server again.

### 3. **Run the Shadowsocks Server**

bash

Copy code

`ssserver -c ~/shadowsocks/config.json`

Let me know if you encounter any other issues after making this change!

4o mini