## Features to add

1. Auto-scroll to bottom when new messages arrive

```python
But since the SSE is on a child element, the simpler approach is to add a small script. Add this attribute to your #messages div:
Copied!

hx_on__htmx_after_swap="this.scrollTop = this.scrollHeight"


```

- [] Switch the Embedding Model
- [] Automatic install of the ColGrep when codebase changed and nbdev_prepare and export!
- [] Reindex when deploy to github!
- [] store BYOK securly in browswer cookies
- [] citatinos
- [] make the delete working
- [x] add history feature based on lisette
- [x] total cost,show the model name and provider under the footer of the icon
- [] add sources(cites )
- [] Control the Personality of the Bot (Name, Icon,model..etc)


1. The merge=True option could be handy for getting a single summary per file, or you can keep individual code units for finer-grained retrieval
2. The CodeUnit metadata (signatures, docstrings, calls, parameters) gives you rich context to pass alongside chunks to Lisette for better citations

### ColGrep Limitations

1. Weak with nbdev codebases — `# %%` cell markers create tons of tiny `RawCode` units that flood the index
2. `.ipynb` files treated as JSON documents (one blob), not parsed as code — no cell extraction
3. No `--include` filter on `colgrep init`, only on search

### ColGrep + nbdev Workflow

**Init from the package dir, not project root:**

```bash
cd /seo_rat/seo_rat
colgrep clear && colgrep init -y
```

**Search with regex pre-filter to skip rawcode noise:**

```bash
# Semantic — filter to real functions/classes only
colgrep -e "^def |^class " "your query" -k 5 -c

# Exact function name — pure regex, always reliable
colgrep -e "^def insert_article" -k 1 -c
```

**Improve semantic ranking — add richer docstrings in the notebook:**

- `"""Insert new article"""` → scores low
- `"""Insert a new article record into the database for a given website"""` → scores high

## Github Actions

For HyperRun, a GitHub Action could automate the Doc Author setup:

    On push → re-index the repo with colgrep init
    Deploy the HyperRun server (e.g. to Railway, Fly.io, or a VPS)
    Build docs with the embed snippet already included

So the doc author's experience becomes: clone repo → add a .github/workflows/hyperrun.yml → push → everything works automatically.
