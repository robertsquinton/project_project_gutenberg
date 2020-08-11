Figure A
================

This column plot explores the prevalence of bookshelf inclusion. A book can belong to one or (counter-intuitively) several bookshelves, but the most common case is the book being absent from any bookshelf.

``` r
bookshelf_multiplicity_summary <- gutenberg_metadata %>%
  filter(language == 'en', rights == "Public domain in the USA.", has_text) %>%
  mutate(bookshelves = str_count(gutenberg_bookshelf, pattern = "/") + 1) %>%
  mutate(bookshelves = replace_na(bookshelves, 0)) %>%
  group_by(bookshelves) %>%
  summarise(count = n()) %>%
  mutate(bookshelves = as.character(bookshelves))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

``` r
ggplot(bookshelf_multiplicity_summary, aes(x = bookshelves, y = count, fill = bookshelves)) +
  geom_col() +
  scale_fill_viridis_d(direction = -1, begin = 0.1) +
  labs(x = NULL, y = "Number of eBooks", fill = "Number of assigned bookshelves")
```

![](md1_files/figure-markdown_github/display%20plot-1.png)
