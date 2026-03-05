## Features to add

1. Auto-scroll to bottom when new messages arrive

```python
But since the SSE is on a child element, the simpler approach is to add a small script. Add this attribute to your #messages div:
Copied!

hx_on__htmx_after_swap="this.scrollTop = this.scrollHeight"


```


1. Switch the Embedding Model
1. Automatic install of the ColGrep when codebase changed and nbdev_prepare and export!
1. Reindex when deploy to github!
1. store BYOK securly in browswer cookies
1. citatinos
1. make the delete working
1. add history feature based on lisette
1. total cost,show the model name and provider under the footer of the icon 


### Colgrep_parser Features

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
