Documentation for my self-hosted homelab: hardware, network topology, and the Docker services running on top of it.

📖 Live site: https://avdo06-maker.github.io/Vladi-homelab/

Structure
docs/
├── index.md              # homepage
├── hardware/index.md      # server specs, drives
├── network/index.md       # topology diagrams, IP mapping
└── services/               # one page per Docker service
    ├── index.md
    ├── immich.md
    ├── seafile.md
    ├── mealie.md
    ├── stirling-pdf.md
    └── dockhand.md
Local preview
bash
pip install mkdocs-material
mkdocs serve

Then open http://localhost:8000.

Deployment

Pushing to main triggers .github/workflows/deploy.yml, which builds the site with MkDocs and publishes it to the gh-pages branch automatically.
