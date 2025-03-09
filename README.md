<div align="center">
  <a href="https://jto.dev">
    <img src="static/favicon/android-chrome-192x192.png"
         alt="Johnny To" 
         width="200"
         style="box-shadow: 0px 10px 15px rgba(0, 0, 0, 0.2); border-radius: 12px;">
  </a>
  <h1>Johnny's Personal Website</h1>
  <p>Built for sharing relevant information about me.</p>
</div>

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Installation](#installation)
	- [Clone the Project](#clone-the-project)
	- [Windows Environment](#windows-environment)
	- [Linux Environment](#linux-environment)
- [Deployment](#deployment)
    - [Configuration](#configuration)
    - [To Deploy the Site](#to-deploy-the-site)
- [Usage](#usage)
- [Contributing](#contributing)
- [Copyright](#copyright)
- [Contact](#contact)

## Overview

Developed with a mobile-first design approach as a digital business card & second as a personal website.

## Features

1. Curriculum Vitae (CV) Page - Detailed information about my work experience.
2. Portfolio Page - Showcases my personal projects.
3. Linkedin Link - Connect with me via Linkedin.
4. GitHub Link - Check out my GitHub profile.
5. Personal Wiki - Useful references at my finger tips.
6. Quick share QR Code to website.

## Installation

### Clone the Project

Clone the project to your local environment.

```bash
git clone https://github.com/348ab1a8-424a-43d8-b463-8e925d751c7f/jto-website.git
cd jto-website
```

### Windows Environment
If you are working on a computer using Windows OS, follow instructions below.

- Install an integrated development environment (IDE), I recommend [Visual Studio Community](https://visualstudio.microsoft.com/vs/).
- Install a package manager for Windows, I recommend [Chocolatey](https://chocolatey.org/).
- Use chocolatey to install Hugo via the following command,

``` powershell
choco install hugo-extended
```

- That's it, now you can launch the local server via the following command,

```
hugo server
```

- Access the website via web browser @ [http://localhost:1313/](http://localhost:1313/).

### Linux Environment
If you are working on a computer using Linux OS, follow instructions below.

- Install an integrated development environment (IDE), I recommend [Visual Studio Code](https://code.visualstudio.com/).
- Other instructions to come...

## Deployment

### Configuration
Hosted on Cloudflare Pages.

Note:
- Building with Cloudflare Pages is currently disabled and only used to deploy the static site due to the incompatibility reasons below.
    - Cloudflare Pages defaults to Hugo v0.118.2.
    - This projects environment uses Hugo v0.145.0.
    - LotusDocs hugo module requires at least Hugo v0.140.0.

Workaround:
- Go to Cloudflare / Workers & Pages / Your-Site / Build / Build Configuration.
    - Edit to
        - Framework Preset: None
        - Build command: echo "Skipping build"
- Then, go to ... / Build / Branch Control.
    - Make sure
        - Production branch: main

### To Deploy the Site

You will have to run the build command to generate static files locally
``` powershell
hugo build
```
- These files will be found in the Public folder.
- Cloudflare by default is set to look for build outputs in Public folder.
    - If the site doesn't load properly then check this setting under ... / Build / Build Configuration.

## Usage

- Make changes and preview the changes locally.
- Verify the website works as intended before pushing an update.

## Contributing

No other individual besides myself (Johnny To) will have the ability to contribute to this project.

## Copyright

For complete copyright details, please see the [COPYRIGHT.md](COPYRIGHT.md) file.

## Contact

Contact me directly via e-mail at [jto@amplivum.com](mailto:jto@amplivum.com?subject=Hello%20from%20GitHub).