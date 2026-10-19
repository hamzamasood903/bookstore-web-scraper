# Bookstore Intelligence Mission: Web Scraper

A reusable web scraper built with `requests`, `BeautifulSoup` and `pandas` that turns the practice site [books.toscrape.com](https://books.toscrape.com/) into a clean business dataset, then uses it to answer pricing, rating and stock questions.

## How it works
1. **Inspect**: each book is an `article.product_pod`. Title is in the `title` attribute of `h3 > a`, price in `p.price_color`, rating in the second class of `p.star-rating`, availability in `p.instock.availability`.
2. **Scrape one page**: `scrape_page(url)` returns a list of records. Rating words (One to Five) are converted to 1-5 and the product URL is captured.
3. **Scale up**: `scrape_catalogue(n_pages)` loops through `page-1.html`, `page-2.html`, ... and stops when a page returns no books. Set `n_pages=None` to scrape the whole catalogue.
4. **Save**: all records go into a DataFrame and are written to `competitor_books.csv`.
5. **Analyse**: pandas answers the seven intelligence questions, and a knapsack dynamic-programming routine solves the £100 CEO challenge exactly.

## Files
- `scraper.py`: the full script
- `bookstore_scraper.ipynb`: the same work as a notebook
- `competitor_books.csv`: dataset produced by the scraper
- `rating_counts.png`: bar chart of books per star rating

## Run it
```bash
pip install requests beautifulsoup4 pandas matplotlib numpy
python scraper.py
```

## Results
*(Fill in from your own output.)*

| Question | Answer |
|---|---|
| 1. Most expensive book |'The Death of Humanity: and the Case for Life' |
| 2. Cheapest book |'Patience' |
| 3. Average price | £34.56 |
| 4. Number of 5-star books |19 |
| 5. % in stock | 100.0% |
| 6. Top 5 highest-rated |81	Princess Between Worlds (Wide-Awake Princess #5)	5	13.34
80	Princess Jellyfish 2-in-1 Omnibus, Vol. 01 (Princess Jellyfish 2-in-1 Omnibus #1)	5	13.61
34	Sophie's World	5	15.94
54	Thirst	5	17.27
12	Set Me Free	5	17.46 |
| 7. Cheapest 5-star book |Princess Between Worlds (Wide-Awake Princess #5) |

**CEO £100 challenge:** selected titles, individual prices, total cost £__, total rating score __.
                                                                              Title  Price  Rating
Mama Tried: Traditional Italian Cooking for the Screwed, Crude, Vegan, and Tattooed  14.02       4
                                                                           Patience  10.16       3
                                   Princess Between Worlds (Wide-Awake Princess #5)  13.34       5
  Princess Jellyfish 2-in-1 Omnibus, Vol. 01 (Princess Jellyfish 2-in-1 Omnibus #1)  13.61       5
                                            Untitled Collection: Sabbath Poems 2014  14.27       4
                                                                     Sophie's World  15.94       5
                                                                        Set Me Free  17.46       5
Total cost: £98.80 | Total rating score: 31 | Books: 7
**Business recommendation:** *(2-3 sentences supported by the data above.)*
I would prioritize 4-5 star books priced below the average of £34.56, because they make up a healthy share of the catalogue and pair strong customer satisfaction with low cost. Since 100% of books are in stock, availability is not a differentiator, so we should compete on price and rating.
## Notes
Built for educational purposes on a sandbox website designed for scraping practice.
