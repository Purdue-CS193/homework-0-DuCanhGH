# Ngo Duc Anh's First CS193 Homework

## Favorite things about CS193:

- Teaching freshmen, most of which are probably Mac or Windows users, how to use Git and Unix commands (stuff that will matter).

  - Will the class be filled with "I use Arch btw" at the end of the semester?
  
    - I use NixOS btw @ https://github.com/DuCanhGH/nixos-config (mandatory NixOS config drop)

      ```nix
      {
        inputs = {
          nixpkgs.url = "github:NixOS/nixpkgs/nixos-unstable";
          # The `follows` keyword in inputs is used for inheritance.
          # Here, `inputs.nixpkgs` of is kept consistent with the
          # `inputs.nixpkgs` of the current flake,
          # to avoid problems caused by different versions of nixpkgs.
          home-manager = {
            url = "github:nix-community/home-manager/master";
            inputs.nixpkgs.follows = "nixpkgs";
          };
          lanzaboote = {
            url = "github:nix-community/lanzaboote/v0.4.2";
            inputs.nixpkgs.follows = "nixpkgs";
          };
        };
        outputs = inputs@{ nixpkgs, home-manager, lanzaboote, ... }: {
          nixosConfigurations.pneuma = nixpkgs.lib.nixosSystem {
            system = "x86_64-linux";
            specialArgs = { inherit inputs; };
            modules = [
              home-manager.nixosModules.home-manager
              lanzaboote.nixosModules.lanzaboote
              ./systems/pneuma/configuration.nix
            ];
          };
          nixosConfigurations.ousia = nixpkgs.lib.nixosSystem {
            system = "x86_64-linux";
            specialArgs = { inherit inputs; };
            modules = [
              home-manager.nixosModules.home-manager
              ./systems/ousia/configuration.nix
            ];
          };
        };
      }
      ```

- Relies on previous students who've gone through the pains of Git and Unix rather than professors (those who probably existed before Linux was even a thing and as such have way more experience with this) -> class feels more engaging and relatable.

- Reminded me to add my Purdue email to my GitHub account and claim the GitHub Student Developer Pack!

## Not so favorite things about CS193:

- Attendance quiz.