# plutus-apps-env-setup-ubuntu

## Resources:
- [NixOS download](https://nixos.org/download.html)
- [The Plutus-Apps repository](https://github.com/input-output-hk/plutus-apps)

## Step by step

1. install curl and git
```console
sudo apt update
sudo apt install curl
sudo apt install git
```
2. install nixos (https://nixos.org/download.html)
```console
sh <(curl -L https://nixos.org/nix/install)
```

Close terminal and restart

3. Set up the IOHK binary caches

IMPORTANT: If you do not set up the IOHK binary cache, it will takes several hours.
```console
cd /etc
sudo mkdir nix
cd nix
sudo nano nix.conf
```
and add the following lines:

```console
substituters        = https://hydra.iohk.io https://iohk.cachix.org https://cache.nixos.org/
trusted-public-keys = hydra.iohk.io:f/Ea+s+dFdN+3Y/G+FDgSq+a5NEWhJGzdjvKNGv0/EQ= iohk.cachix.org-1:DpRUyj7h7V830dp/i6Nti+NEO2/nhblbov/8MW7Rqoo= cache.nixos.org-1:6NCHdD59X431o0gWypbMrAURkbJ16ZPMQFGspcDShjY=
```
4. Save nix.conf and Restart Ubuntu

NOTE: since step 5 if error, restart ubuntu and start again from step 5

5. to check if nix is installed
```console
nix-env --version
```
6. Download the plutus-apps repository
```console
git clone https://github.com/input-output-hk/plutus-apps
```
7. Build plutus-playground server, at top of this repo (this takes around 3 mins) 
```console
cd plutus-apps
nix-build -A plutus-playground.server
```
8. Start plutus-playground-server (the first time you run nix-shell it takes around 20 minutes)
```console
nix-shell				
cd plutus-playground-client
plutus-playground-server
```
Wait for server to start, it'll log "Interpreter ready"

9. In second terminal at top of this repo
```console
nix-shell
cd plutus-playground-client
npm run start
```
Wait for the client to start, it'll log "webpack compiled with …”

10. In web browser, navigate to url https://localhost:8009/ (need to accept that ssl certificate is invalid)
```console
https://localhost:8009/
```
11. Compile and evaluate plutus code without DecodingError
