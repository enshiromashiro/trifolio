```toml
# article metadata

title = "an example article"

description = """
this is an example article for trifolio static site generator system.
"""

tags = [
  "article",
  "example",
]
```

# about this article

this article is an example for the trifolio static site generator.

# the article structure

each articles are composed by two parts; a metadata and a body.

one article has one metadata block as **a toml code block** placed at the head of it. that is parsed as a toml document and is used as article infomation in other pages like article list page.

another part is a content of the article itself called a body. the body of the article are written in CommonMark or GitHub Flavored Markdown.

# foo

**bar**

and ~~buzz~~
