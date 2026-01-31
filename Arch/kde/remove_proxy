#!/usr/bin/env bash
# Author: Surya-Raghuram [GitHub: Surya-Raghuram]

echo "Created by Surya-Raghuram [GitHub: Surya-Raghuram]"
echo ""

set -e

echo "=== Disable Proxy ==="

#################################
# System env
#################################

sudo rm -f /etc/profile.d/proxy.sh

#################################
# git
#################################

git config --global --unset http.proxy || true
git config --global --unset https.proxy || true

#################################
# npm
#################################

npm config delete proxy || true
npm config delete https-proxy || true

#################################
# KDE Plasma GUI (Plasma 6)
#################################

# Use Plasma 6 tools
KWRITE=kwriteconfig6

$KWRITE --file kioslaverc --group "Proxy Settings" --key ProxyType 0
$KWRITE --file kioslaverc --group "Proxy Settings" --key ProxyUser ""
$KWRITE --file kioslaverc --group "Proxy Settings" --key ProxyPass ""
$KWRITE --file kioslaverc --group "Proxy Settings" --key httpProxy ""
$KWRITE --file kioslaverc --group "Proxy Settings" --key httpsProxy ""
$KWRITE --file kioslaverc --group "Proxy Settings" --key ftpProxy ""
$KWRITE --file kioslaverc --group "Proxy Settings" --key socksProxy ""

# Optional reload (may fail silently, that's fine)
qdbus6 org.kde.KIO.Scheduler /KIO/Scheduler reparseSlaveConfiguration 2>/dev/null || true

#################################
# snap
#################################

sudo systemctl restart snapd 2>/dev/null || true

#################################
# Firefox
#################################

FF_PROFILE="/home/poke/.mozilla/firefox/r3my975k.default-release"

cat > "$FF_PROFILE/user.js" <<EOF
user_pref("network.proxy.type", 0);
EOF


echo
echo "Proxy disabled everywhere."
