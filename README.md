# nixos-steam-console
A simple flake to turn any NixOS device into a SteamOS console. Inspired by [Jovian-NixOS](https://github.com/Jovian-Experiments/Jovian-NixOS).

## Features
- Gamescope realtime (always enabled)
- HDR/VRR
- [Decky Loader](https://github.com/SteamDeckHomebrew/decky-loader)
- 'Switch to Desktop' session

## Usage
```nixos
{
  inputs = {
    nixpkgs.url = "github:nixos/nixpkgs/nixos-unstable";
    steam-console.url = "github:n1chols/nixos-steam-console";
  };

  outputs = { nixpkgs, steam-console, ... }: {
    nixosConfigurations.steamConsole = nixpkgs.lib.nixosSystem {
      system = "x86_64-linux";
      modules = [
        ...
        steam-console.nixosModules.default
        ({ ... }: {
          steam-console = {
            enable = true;
            enableHDR = true;
            enableVRR = true;
            enableDecky = true;
            user = "your-user";
            desktopSession = "command-to-start-desktop";
          };
        })
      ];
    };
  };
}
```
