## Intro

I am doing the real numbers game as found [here](https://wwwf.imperial.ac.uk/~buzzard/xena/rng090720/). A few versions of the game are floating around, so your version may not correspond nicely with mine.

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

I show my first (pretty pathetic) attempt
```
split,

intro ab,
rw ext_iff,
intro x,
rw mem_union_iff,

split,
intro xin,
right,
use xin,

intro, 
cases a with a b,
rw subset_iff at ab,
apply ab, use a,

use b,

intro ab,
rw subset_iff,
intros x xin,
rw ext_iff at ab,
rw ab, 
use xin,
```

So this one is a tiny bit better, here we 'factorised' out the proof of x early on, and also used the nice `tauto` tactic for proving logic-based goals.

```
rw subset_iff,
rw ext_iff,

apply forall_congr, -- thank you Mario
intro x,

split,
intro it,
rw mem_union_iff,
tauto, -- pleasently overpowered

intro iff,
rw iff, 
rw mem_union_iff,
tauto,
```

It turns out we can use `tauto` a bit more, it's logic based and figures out the \(\leftrightarrow\) quite well on its own.

```
rw subset_iff,
rw ext_iff,

apply forall_congr,
intro x,

rw mem_union_iff,
tauto,
```

Level 5

Using what we've learnt

```
rw ext_iff,
apply forall_congr,
intro x,

rw mem_inter_iff,
tauto, 
```

Level 6

```
rw ext_iff,
intro x,
rw mem_sdiff_iff, 
rw ←mem_neg_iff, 
rw mem_inter_iff, 
```

Alternatively,

```
rw ext_iff,
intro x,
refl,
```

Level 7

```
rw subset_iff,
intro x,
tauto, -- I am liking this tactic
```

I'm not sure why it's overly verbose here, maybe I was meant to focus by doing this? But it's all logicky so I'm still slightly unsure why my approach wasn't put forward.

```
rw subset_iff,
intro x,
rw mem_empty_iff,
intro false,
cases false,
```

Level 8


```
norm_num
```

Although to get the most out of the 'pro tips'

```
split;
norm_num,
```

I didn't bother doing a split at first because `norm_num` supports simplification over \(\and\).

Level 9

```
use -2, 
norm_num,

use 0,
norm_num,
```

I do wonder if there's a way to expedite this, it looks slightly repetetive.

Level 10

```
intros x y le,

have h : ∃ n : ℕ, 0 < n ∧ (1/n : ℝ) < (y - x), 
apply archimedean_R, 
linarith,

cases h with n ar,

have h : ∃ m : ℤ, ((m - 1) : ℝ) ≤ (n*x) ∧ (n*x : ℝ) < (m : ℝ), 
apply has_ceiling (n*x), 

cases h with m hc,

have h : 0 < n → (1/n : ℝ) * (m : ℝ) = (m/n : ℝ),
apply inv_prod_other m n, 

use [m/n, m/n], 
simp, 

have g : x < (m/n : ℝ) ↔ (↑n*x) < (↑m),
apply lt_div_iff' _, norm_num [h],
simp * at *,

split,
rw g, apply hc.2, 

-- use m <= nx + 1 < n(y - 1/n) + 1 = ny, then solve it
```

I need to go now so will complete it later. This is also my first attempt, I'm definitely planning to make it nicer, at the moment my ideas are to use backwards reasoning instead of forward.

That is the end of set world.
### TBC


This down here is for me, so I don't forget markdown things.

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
