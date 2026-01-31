#!/usr/bin/env bash
# Author: Surya-Raghuram [GitHub: Surya-Raghuram]

echo "Created by Surya-Raghuram [GitHub: Surya-Raghuram]"
echo ""
echo "This is for IIITA campus proxy only, allows you to set your own Username and Password, and uses 8080 as Port number"

set -e

echo "=== Enable Proxy ==="

# don't let script run as root
if (( $EUID == 0 )); then
    echo -e "\n\nPlease DON'T run as root!\n"
    exit
fi

# Ensure /etc/profile is sourced for KDE terminals (for pacman)
if ! grep -q "/etc/profile" ~/.bashrc; then
cat >> ~/.bashrc <<'EOF'

# Load system profile (for proxy support)
if [ -f /etc/profile ]; then
    source /etc/profile
fi
EOF
fi

PROXY_PORT="8080"

read -p "Please enter the proxy host you want to apply (eg, 172.31.2.4) : " PROXY_HOST
echo ""
read -p "Please enter your proxy username: " PROXY_USER
echo ""
read -rsp "Password: " PROXY_PASS
echo ""

AUTH="${PROXY_USER}:${PROXY_PASS}@"

PROXY_HTTP="http://${AUTH}${PROXY_HOST}:${PROXY_PORT}"

#################################
# System environment
#################################

sudo tee /etc/profile.d/proxy.sh >/dev/null <<EOF
export http_proxy="$PROXY_HTTP"
export https_proxy="$PROXY_HTTP"
export HTTP_PROXY="$PROXY_HTTP"
export HTTPS_PROXY="$PROXY_HTTP"
export ftp_proxy="$PROXY_HTTP"
export no_proxy="localhost,127.0.0.1,::1"
EOF

#################################
# pacman
#################################
# pacman will end up using environment variables directly

# pacman Allow sudo to inherit proxy (run once)
if [[ ! -f /etc/sudoers.d/proxy ]]; then
    echo "Configuring sudo to keep proxy variables"
    sudo sh -c 'echo "Defaults env_keep += \"http_proxy https_proxy HTTP_PROXY HTTPS_PROXY ftp_proxy no_proxy\"" > /etc/sudoers.d/proxy'
    sudo chmod 440 /etc/sudoers.d/proxy
fi

#################################
# git
#################################

git config --global http.proxy "$PROXY_HTTP"
git config --global https.proxy "$PROXY_HTTP"

#################################
# npm
#################################

npm config set proxy "$PROXY_HTTP"
npm config set https-proxy "$PROXY_HTTP"

#################################
# KDE Plasma GUI (Plasma 6)
#################################

# Use Plasma 6 tools
KWRITE=kwriteconfig6

$KWRITE --file kioslaverc --group "Proxy Settings" --key ProxyType 1
$KWRITE --file kioslaverc --group "Proxy Settings" --key httpProxy "${PROXY_HOST}:${PROXY_PORT}"
$KWRITE --file kioslaverc --group "Proxy Settings" --key httpsProxy "${PROXY_HOST}:${PROXY_PORT}"
$KWRITE --file kioslaverc --group "Proxy Settings" --key AuthMode 1
$KWRITE --file kioslaverc --group "Proxy Settings" --key ProxyUser "$PROXY_USER"
$KWRITE --file kioslaverc --group "Proxy Settings" --key ProxyPass "$PROXY_PASS"

# Optional reload (may fail silently, that's fine)
qdbus6 org.kde.KIO.Scheduler /KIO/Scheduler reparseSlaveConfiguration 2>/dev/null || true

#################################
# snap
#################################

sudo systemctl restart snapd 2>/dev/null || true

#################################
# Firefox
#################################

FF_PROFILE="$HOME/.mozilla/firefox/r3my975k.default-release"

cat > "$FF_PROFILE/user.js" <<EOF
user_pref("network.proxy.type", 1);
user_pref("network.proxy.http", "$PROXY_HOST");
user_pref("network.proxy.http_port", $PROXY_PORT);
user_pref("network.proxy.ssl", "$PROXY_HOST");
user_pref("network.proxy.ssl_port", $PROXY_PORT);
user_pref("network.proxy.share_proxy_settings", true);
user_pref("network.proxy.no_proxies_on", "localhost, 127.0.0.1");
EOF

echo
echo "Proxy enabled!!"
