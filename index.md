## Intro

I am doing the real numbers game as found [here](https://wwwf.imperial.ac.uk/~buzzard/xena/rng090720/). It turns out that there are a few versions floating around, so while this game isn't finalised this is the version I'll working on.

It's mid-July now, for reference.

## Set World

Level 1

```
rw subset_iff,
intros x inx,
use inx,
```

Level 2

```
--rw subset_iff,
intros x xin,
rw mem_union_iff,
use xin, 
```

I commented out the rewrite because as far as lean is concerned, a hidden definition is no different from an actual definition.
But while typing things out it's a friendly helper.

Level 3

```
intros x xin,
rw mem_inter_iff at xin,
use xin.left,
```

I personally find it much nicer to 'dig in' to those proofs that include \(\and, \leftrightarrow \) as opposed to splitting it and then dealing with it. The second way seems pretty clunky and childish.

Level 4

```
...
```

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/dkurganov/real_number_game/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
