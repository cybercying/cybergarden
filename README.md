# cybarGarden - A Quartz v5 Full Template for Personal Digital Garden

> A personal [digital garden](https://jzhao.xyz/posts/networked-thought) powered by [**Quartz 5**](https://quartz.jzhao.xyz/), built to share thoughts, essays, and notes—while serving as a fully functional, open-source template for building your own knowledge site.

---

## 💡 About This Project

Publishing a personal digital garden using Quartz is immensely powerful, but coming from tools like **Obsidian** or building a setup tailored for **multilingual content** comes with a steep learning curve.

**cyberGarden** was created to bridge that gap. 

Rather than just listing documentation, this repository serves as both:
1. **A Live Digital Garden:** My personal published notes, essays, and technical insights.
2. **A Concrete Blueprint:** A battle-tested Quartz 5 setup with real source content (`/content`) and its corresponding generated output (`/public`), allowing you to study, inspect, and fork a fully working architecture.

---

## ✨ Key Customizations & Features

### 🌐 Multilingual Essay Support
Quartz 5 out-of-the-box requires custom architecture to smoothly handle multi-language essays (e.g., Chinese, English, Japanese). 
* Customized routing, layout structure, and navigation tags to support multi-language content seamlessly.
* Solves common localization and layout issues when serving essays across different target languages.

### ✍️ Obsidian Hard Line Break Fix
If you write notes in Obsidian, you likely rely on standard newline behavior (`hardLineBreaks: true`), whereas standard Markdown renderers collapse single line breaks into a single line.
* Configured and tuned the Markdown parsing pipeline to correctly honor Obsidian-style hard line breaks.
* Ensures your rendered web pages match your local Obsidian reading experience line-for-line without manual `<br>` hacks or trailing double spaces.

### 🔍 Fully Functional & Transparent Structure
* **Source (`/content`):** Real-world raw Markdown notes, demonstrating internal links (`[[wikilinks]]`), frontmatter setup, tag hierarchies, and multilingual folder organizations.
* **Build Target (`/public`):** Included or referenceable build output so you can inspect how Quartz compiles specific Markdown structures into final HTML/CSS/JS.

---

## 🛠️ Tech Stack & Prerequisites

* **Engine:** [Quartz 5](https://quartz.jzhao.xyz/)
* **Source Editor:** [Obsidian](https://obsidian.md/)
* **Runtime:** [Node.js](https://nodejs.org/) (v18.x or higher recommended)
* **Package Manager:** `npm` / `npx`

---

## 🚀 Quick Start

1. Clone the Repository
    ```bash
    git clone https://github.com/cybercying/cybergarden.git
    cd cybergarden
    ```

2. Install Dependencies and Quartz plugins

    ```bash
    npm install
    npx quartz plugin install --from-config
    ```

    Because this is a running site, naturally we already have a config file `quartz.config.yaml` in place, which is based on Quartz 5's default config file `quartz.config.default.yaml`. That's why `--from-config` would work properly. If you're starting a new project, following commands are needed to install additional plugins: (The choices of the plugin is, of course, opinionated.)

    ```bash
    npx quartz plugin add github:boxi-os/quartz-navigations
    npx quartz plugin add github:boxi-os/quartz-layout-box
    npx quartz plugin add github:boxi-os/quartz-multilanguage
    ```

3. Local Development Server

    Start the local Quartz preview server with hot-reloading:
    ```bash
    npx quartz build --serve
    ```
    Open your browser and navigate to http://localhost:3000.

4. Build for Production

    To compile the site into static HTML assets:

    ```bash
    npx quartz build
    ```

    The output will be placed in the `public/` directory.

## 📖 Learning from This Template
If you are using **cyberGarden** as a reference to fix or customize your own Quartz site:

Check `quartz.config.yaml`: Inspect the configurations for third-party plugins and line-break parsing settings.

Explore `/content` Structure: See how frontmatter parameters (tags, aliases, dates, language metadata) are structured for multi-language navigation.

## 🤝 Contributing & Feedback
Feel free to open an issue or pull request if you find bugs, have questions about the Quartz setup, or want to suggest improvements to the multilingual routing.

## 📄 License
This repository is dual-licensed / open for exploration:

- **Code / Configurations (/quartz, configs):** Released under the MIT License.

- **Personal Writings / Essays (/content):** All rights reserved by the author.