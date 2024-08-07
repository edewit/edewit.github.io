---
layout: post
title: Announcing New Keycloak UI Component Libraries!
date: '2023-09-06'
author: Erik Jan de Wit
---

We're excited to announce the release of two new npm packages designed to supercharge your Keycloak customization efforts.
These React component libraries, built on top of PatternFly, provide the essential building blocks for crafting account and admin consoles.

The packages are:

- [@keycloak/keycloak-admin-ui](https://www.npmjs.com/package/@keycloak/keycloak-admin-ui)
  - This package provides the building blocks for creating a Keycloak admin console.
- [@keycloak/keycloak-account-ui](https://www.npmjs.com/package/@keycloak/keycloak-account-ui)
  - This package provides the building blocks for creating a Keycloak account console.
- [@keycloak/ui-shared](https://www.npmjs.com/package/@keycloak/ui-shared)
  - This package provides shared components and utilities for building Keycloak UIs.


### Accelerate Your Development with Our Quickstart Tool

To get you up and running in no time, we've also created a handy command-line tool: `npm init keycloak-theme my-theme`.
This tool sets up a new project with the necessary dependencies, configuration, and a basic structure, saving you valuable time and effort.
For more information, see the [README](https://github.com/keycloak/keycloak/blob/main/js/apps/create-keycloak-theme/README.md).

Once you have ran the command, you can start developing your custom theme by editing the files in the `src` directory.
Changes will be automatically reflected in your running instance of the theme.
When you're ready to deploy your theme, simply run `mvn install` to generate a production-ready version of your theme, hat you can then deploy to your Keycloak instance.
