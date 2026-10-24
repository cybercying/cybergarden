# cyberGarden - A Quartz v5 Full Template for Personal Digital Garden

> A personal [digital garden](https://jzhao.xyz/posts/networked-thought) powered by [**Quartz 5**](https://quartz.jzhao.xyz/), built to share thoughts, essays, and notes—while serving as a fully functional, open-source template for building your own knowledge site.

---

## 💡 About This Project

Publishing a personal digital garden using Quartz is immensely powerful, but coming from tools like **Obsidian** or building a setup tailored for **multilingual content** comes with a steep learning curve.

**cyberGarden** was created to bridge that gap. This repository is the source code of a live (my) digital garden website. The final generated result can be visited at _My Garden_ in the following link:
- https://cybercying.github.io/cybergarden/

Rather than just listing documentation, this repository serves as both:
1. **A Live Digital Garden:** My personal published notes, essays, and technical insights.
2. **A Concrete Blueprint:** A battle-tested Quartz 5 setup with real source content ([`/content`](content)) and its corresponding generated output, allowing you to study, inspect, and fork a fully working architecture.

    _**Note:** Because generally the default output folder, which is `/public`, is not checked-in into a git repo, the actual generated content is put inside another subdirectory [`/cybergarden`](cybergarden). This allow the developer who wants to try out this site to have an empty `/public` folder to test on, while the [`/cybergarden`](cybergarden) serves as the source of the GitHub pages of My Garden._


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
* **Source ([`/content`](content)):** Real-world raw Markdown notes, demonstrating internal links (`[[wikilinks]]`), frontmatter setup, tag hierarchies, and multilingual folder organizations.
* **Build Target (`/public`):** Build output. This is where Quartz compiles specific Markdown structures into final HTML/CSS/JS.
* **Live Static Site ([`/cybergarden`](cybergarden)):** This is where I put the actual generated content and checked in git for GitHub Pages to publish for me.

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

    Because this is a running site, naturally we already have a config file [`quartz.config.yaml`](quartz.config.yaml) in place, which is based on Quartz 5's default config file [`quartz.config.default.yaml`](quartz.config.default.yaml) (unmodified). That's why `--from-config` would work properly. If you're starting a new project from scratch, following commands are needed to install additional plugins: (The choices of the plugin is, of course, opinionated.)

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

## 📂 Project Structure
```plaintext
cyberGarden/
├── content/                    # Obsidian Markdown files & media assets
│   ├── index.zh.md             # Chinese landing page
│   ├── index.ja.md             # Japanese landing page
│   ├── index.ko.md             # Korean landing page
│   ├── index.es.md             # Spanish landing page
│   └── index.md                # Landing page
├── quartz/                     # Quartz core configurations, components, and layouts
│   ├── components/             # Custom TSX/JSX UI components
│   └── plugins/                # Markdown processors, transformers, and emitters
├── quartz.config.yaml          # Configuration file, adapted for cyberGarden
├── quartz.config.default.yaml  # Default configuration file template (unchanged)
├── cybergarden/                # Checked-in generated result for GitHub Pages
└── public/                     # Generated static website (HTML, CSS, JS). 
                                # Left empty for the convenience of the user.
```

## 📖 Learning from This Template
If you are using **cyberGarden** as a reference to fix or customize your own Quartz site:

Check `quartz.config.yaml`: Inspect the configurations for third-party plugins and line-break parsing settings.

Explore `/content` Structure: See how frontmatter parameters (tags, aliases, dates, language metadata) are structured for multi-language navigation.

## 🧩 Essential Plugins & Architectural Workarounds

If you have tried customizing **Quartz 5** using traditional guides or tutorials written for earlier versions, you may have noticed that many `quartz.layout.ts` tweaks simply **do not work**. 

### ⚠️ The Quartz 5 `quartz.layout.ts` Limitation

In the current version of Quartz 5, there is a known upstream issue where most direct modifications to `quartz.layout.ts` become completely ineffective. After tracing the core codebase, I confirmed this behavior and reported [the findings](https://github.com/jackyzha0/quartz/issues/2382#issuecomment-5985489119) back to the Quartz 5 repository. However, the upstream issue was closed without a native fix, leaving only a rather clunky [workaround](https://github.com/jackyzha0/quartz/issues/2382#issuecomment-5622495613). 

Because of this, standard community tricks for modifying default layouts (like customizing the built-in Explorer or Footer) are currently broken or extremely fragile out of the box unless you write custom plugins.

---

### 🔌 Ecosystem Solutions Used in `cyberGarden`

To completely bypass these limitations—and to achieve full multilingual capabilities—**cyberGarden** integrates three crucial third-party plugins from [boxi-os](https://github.com/boxi-os):

#### 1. [`quartz-multilanguage`](https://github.com/boxi-os/quartz-multilanguage)
* **Purpose:** Core multilingual routing, page metadata processing, and content switching.
* **Why it's essential:** Enables seamless management and display of multilingual essays (e.g., English, Chinese) without hacky folder redirects.

#### 2. [`quartz-navigations`](https://github.com/boxi-os/quartz-navigations)
* **Purpose:** Replaces the stock Quartz Explorer component.
* **Why it's essential:** Customizing the default Quartz Explorer to respect language contexts triggers the layout reactivity bug mentioned above. This plugin works around the issue out of the box, offering a highly versatile, powerful, and language-aware navigation sidebar that "just works."

#### 3. [`quartz-layout-box`](https://github.com/boxi-os/quartz-layout-box)
* **Purpose:** Replaces the rigid stock footer component.
* **Why it's essential:** The default community footer contains hardcoded elements that are difficult to adapt. `quartz-layout-box` provides a flexible layout wrapper, allowing full control over footer components, links, and custom styling without breaking Quartz 5 builds.

---

💡 **Takeaway for Builders:** If you are struggling with layout customizations in Quartz 5, avoid fighting `quartz.layout.ts` directly. Review how these three plugins are hooked into `cyberGarden`'s configuration files as a blueprint for your own site.

## 🤝 Contributing & Feedback
Feel free to open an issue or pull request if you find bugs, have questions about the Quartz setup, or want to suggest improvements to the multilingual routing.

## 📄 License
This repository is dual-licensed / open for exploration:

- **Code / Configurations (/quartz, configs):** Released under the MIT License.

- **Personal Writings / Essays (/content):** All rights reserved by the author.