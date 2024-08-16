# Electorid Marines Playbook 

Document generation status: [![example workflow](https://github.com/electroid2024/playbook/actions/workflows/ci.yml/badge.svg)](https://github.com/electroid2024/playbook/actions)

## About this repo

This repo is to host the "playbook" documentation website for our FLL team's robot game. 

## Where is our "playbook" website ?

- [https://electroid2024.github.io/playbook/](https://electroid2024.github.io/playbook/)

## How to use this repo locally

https://squidfunk.github.io/mkdocs-material/getting-started/

### MkDocs: Initial setup

```bash
sudo apt install -y docker.io
sudo docker pull squidfunk/mkdocs-material
```

### Mkdocs: Start development server on http://localhost:8000

```bash
docker run --rm -it -p 8000:8000 -v ${PWD}:/docs squidfunk/mkdocs-material
```