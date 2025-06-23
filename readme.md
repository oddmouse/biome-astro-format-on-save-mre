# Biome Astro Format on Save MRE

Since upgrading Biome to version 2.0.0, formatting on save with `.astro` files completely removes all code that is not inside frontmatter.

When running `pnpm biome check --fix src/test.astro` in the terminal, everything runs as expected.

The only thing I could find related to this is an issue with the Zed extension where I am also experiencing the issue. https://github.com/biomejs/biome-zed/issues/60


## Steps to Reproduce

1. Clone the MRE repo
2. Open `src/test.astro` in VS Code with the biome extension installed
3. Save the file
4. Save the file and watch it format and strip out all code except for the frontmatter

From this:

```astro
---
const useSortedKeys = {
	2: "two",
	3: "three",
	1: "one",
	4: "four",
};

let useConst = "Astro Test";
---

<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>{useConst}</title>
  </head>
  <body>
    <h1>{useConst}</h1>
    <ol>
      {Object.values(useSortedKeys).map((val) => <li>{val}</li>)}
    </ol>
  </body>
</html>
```

To this:

```
const useSortedKeys = {
	1: "one",
	2: "two",
	3: "three",
	4: "four",
};

const useConst = "Astro Test";
```