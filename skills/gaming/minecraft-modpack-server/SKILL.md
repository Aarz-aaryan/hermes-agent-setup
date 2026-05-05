# Minecraft Modpack Server — Host Modded Minecraft Servers

## Overview
Two ways to host modded Minecraft servers:
1. **CurseForge modpack** — easiest, use CurseForge app to download and export
2. **Modrinth modpack** — open source alternative, use Prism Launcher or modrinth-launcher

## Method 1: CurseForge Modpack

### 1. Download modpack via CurseForge app
- Install CurseForge app
- Browse modpacks, click Install
- Wait for download and install to complete

### 2. Export the server files
- In CurseForge, go to the modpack → Settings → Export
- Export as "CurseForge (Minecraft) modpack"
- This creates a `.zip` file

### 3. Upload to your server
```bash
scp modpack.zip user@your-server:/opt/minecraft/
ssh user@your-server
cd /opt/minecraft
unzip modpack.zip
```

### 4. Install Java and run
```bash
apt install openjdk-21-jdk-headless  # or use apt install java-21-jdk

# Run the installer if provided
chmod +x install.sh
./install.sh

# Or manually run the server
java -Xmx8G -Xms4G -jar minecraft_server.jar nogui
```

### 5. Accept EULA
```bash
echo "eula=true" > eula.txt
```

### 6. Configure server.properties
```bash
nano server.properties
# Set: max-players, difficulty, pvp, whitelist, etc.
```

## Method 2: Modrinth (Prism Launcher)

### 1. Download via Prism Launcher
- Install Prism Launcher
- Add instance → Download from Modrinth
- Search for modpack (e.g. "Enigmatica 2", "RLCraft")
- Download and install

### 2. Locate files
```bash
~/.local/share/PrismLauncher/instances/<instance-name>/minecraft/
```

### 3. Upload to server
```bash
rsync -avz ~/.local/share/PrismLauncher/instances/<instance-name>/minecraft/ user@server:/opt/minecraft/
```

## Server Management

### Systemd service
```ini
[Unit]
Description=Minecraft Server
After=network.target

[Service]
User=minecraft
WorkingDirectory=/opt/minecraft
ExecStart=/usr/bin/java -Xmx8G -Xms4G -jar server.jar nogui
Restart=on-failure
RestartSec=30

[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl enable minecraft
sudo systemctl start minecraft
sudo journalctl -u minecraft -f
```

### Docker alternative
```bash
docker run -d \
  --name mc-server \
  -p 25565:25565 \
  -v /opt/minecraft:/data \
  -e EULA=TRUE \
  -e MEMORY=8G \
  itzg/minecraft-server
```

## Performance Tips
- Use Paper or Purpur server JAR for better performance
- Allocate 8-16GB RAM for modded servers
- Use SSD storage
- Set `view-distance=10` in server.properties
- Enable `sync-chunk-writes=false` in Paper
- Use `netty-worker-threads=4` for many players

## Backup
```bash
# In-game or RCON
say Server backing up...
save-off
save-all
tar -czf backup-$(date +%Y%m%d-%H%M%S).tar.gz world/
save-on
say Backup complete.
```
