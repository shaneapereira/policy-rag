# Notes

## Environment setup (day 1)

Built on GitHub Codespaces, driven from an iPad. No local machine, so the
dev environment had to be remote and reproducible.

**Pinned Python to 3.12.** The default image was on 3.14, which is new
enough that several AI libraries don't yet ship pre-built wheels. Added a
`.devcontainer/devcontainer.json` so the version is fixed for anyone who
clones the repo, rather than depending on whatever the host provides.

**Hit `externally-managed-environment` (PEP 668).** The container turned out
to be Alpine-based, not the Debian image I'd specified, and its system Python
refuses direct `pip install` to protect packages the OS manages. Rather than
override with `--break-system-packages`, used a virtual environment: project
dependencies now live in `.venv`, isolated from the system Python. The right
fix rather than the fast one — the same reasoning as not installing libraries
into a shared runtime on a server.

**Git LFS hooks blocked the first push.** The repo had LFS hooks configured
but `git-lfs` wasn't on the path, so the pre-push hook aborted. Removed the
orphaned hooks. Also caught `get-pip.py` in the first commit and removed it
with `git rm --cached` plus a `.gitignore` entry.

**Open item:** the container is Alpine rather than the image the devcontainer
file requests, so the rebuild isn't fully applying. Not blocking yet. May
matter when adding Postgres via Docker-in-Docker.git add -A
git commit -m "Add setup notes"
git push
