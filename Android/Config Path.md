

```bash
export ANDROID_HOME=/home/mint/Android/Sdk
export PATH=$ANDROID_HOME/tools:$ANDROID_HOME/tools/bin:$ANDROID_HOME/platform-tools:$PATH

```

better:
```bash
# Set ANDROID_HOME
export ANDROID_HOME=~/Android/Sdk

# Add Android SDK tools to PATH
export PATH=$PATH:$ANDROID_HOME/platform-tools
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/build-tools/35.0.0 

```