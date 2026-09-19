# usefulHQ Used Price Index

A daily index of secondhand prices, built from the cheapest genuine eBay US listing for about
2,100 specific product models across 88 categories. Free to use with attribution.

- Live page, with the current reading and the method: https://usefulhq.com/used-price-index/
- Data: [`used-price-index.csv`](used-price-index.csv), one row per day per scope
  (`all` plus one row per category), updated daily.

## What is in the CSV

| column | meaning |
|---|---|
| `date` | the day the prices were recorded |
| `scope` | `all` for the whole index, otherwise the category slug, which is also its page on usefulhq.com |
| `index_level` | 100.0 at the start date, chained daily |
| `models` | how many models carried a price that day |

## How it is built

Each day is measured against the day before, not against a fixed baseline. Every model priced on
both days contributes one ratio, and the day's move is the trimmed mean of those ratios with the
top and bottom 10% removed, because most models do not move on a given day and the median would
sit at exactly 1.0000 forever.

**A one-day move of more than 25% on a single model is discarded rather than counted.** A jump
that size is almost always the collector matching a different listing. This rule exists because
the first version, chained from a fixed August baseline, reported acoustic guitars down 32%: our
own filters had improved on 12 August and stopped pricing guitars from listings that were never
guitars. An index that cannot tell its own corrections from the market is worse than no index.

Prices are the cheapest Buy It Now listing per model, in US dollars, with parts, accessories,
broken units and bundles filtered out as far as the filters can tell. One model, one vote: there
is no way to weight by sales volume from listing data, and inventing a weighting would be false
precision.

## What it does not tell you

It tracks the floor of the market (cheapest listing), not what a typical buyer pays. Categories
are equally weighted by model, so a category with eight models counts as much as one with fifty.
History starts in August 2026, so a six-week move is a hint, not a trend.

## Citing it

Please link https://usefulhq.com/used-price-index/ and include the date, since the numbers change
daily. Questions, corrections or a category you want pulled: hello@usefulhq.com
