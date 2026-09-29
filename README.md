# usefulHQ Used Price Index

A daily index of secondhand prices, built from the cheapest genuine eBay US listing for about
2,100 specific product models across 88 categories. Licensed [CC BY 4.0](LICENSE): free to use, including commercially,
with credit to "usefulHQ Used Price Index".

- Live page, with the current reading and the method: https://usefulhq.com/used-price-index/
- Data: [`used-price-index.csv`](used-price-index.csv), one row per day per scope
  (`all` plus one row per category), updated daily.
- Monthly readings, one fixed page per completed month, revised only when the method itself is
  corrected, which the page says at the top: https://usefulhq.com/used-price-index/2026-08/
  (August 2026; later months follow the same pattern)

## What is in the CSV

| column | meaning |
|---|---|
| `date` | the day the prices were recorded |
| `scope` | `all` for the whole index, otherwise the category slug, which is also its page on usefulhq.com |
| `index_level` | 100.0 at the start date, chained daily |
| `models` | how many models carried a price that day |

## How it is built

Each day is measured against the day before, not against a fixed baseline. Every model priced on
both days contributes one ratio, and the day's move is the trimmed geometric mean of those ratios
with the top and bottom 10% removed. Most models do not move on a given day, so the median would
sit at exactly 1.0000 forever.

**A one-day move on a single model of more than 25% up, or 20% down, is discarded rather than
counted.** Those are the same size of move: a 20% fall is exactly undone by a 25% rise. A jump that
size is almost always the collector matching a different listing. This rule exists because the
first version, chained from a fixed August baseline, reported acoustic guitars down 32%: our own
filters had improved on 12 August and stopped pricing guitars from listings that were never
guitars. An index that cannot tell its own corrections from the market is worse than no index.

Prices are the cheapest Buy It Now listing per model, in US dollars, with parts, accessories,
broken units and bundles filtered out as far as the filters can tell. One model, one vote: there
is no way to weight by sales volume from listing data, and inventing a weighting would be false
precision.

## Revisions

**30 September 2026: method corrected, whole history recomputed.** Two faults in the chaining were
fixed together. The discard rule was one-sided: it removed any one-day move over 25% either way,
which kept a 24% fall but threw away the 33% rise that undid it, so a price bouncing between two
listings was pushed down one bounce at a time. And the day's ratios were averaged arithmetically,
which drifts upward when prices bounce. The two partly cancelled, so the whole index barely moved
(read on 29 September, since 7 August: whole market -0.4% as first published, -0.3% recomputed;
graphics cards +6.6% and +6.3%), but some categories changed a lot (Samsung Galaxy phones -25.0% to -6.1%, Google Pixel phones +0.3% to +11.4%, GoPros
-16.7% to -5.8%). Every row in the CSV was recomputed, and the commit history keeps the earlier numbers.
The August monthly page was recomputed too and says so at the top.

**From 1 October 2026, published days are not recomputed.** Until then the whole CSV was rebuilt every night, so when a wrong listing was found and a model's history was corrected, days already published could change. From 1 October each day's figures stay as first published; a correction counts from the day it is made, and any future change to the method will be listed here as a revision, with the commit history keeping the earlier numbers.

## What it does not tell you

It tracks the floor of the market (cheapest listing), not what a typical buyer pays. Categories
are equally weighted by model, so a category with eight models counts as much as one with fifty.
History starts in August 2026, so a six-week move is a hint, not a trend.

## Where it sits next to the CPI

The US Consumer Price Index has long priced used cars and trucks, and until recently little else
bought secondhand. Secondhand clothing joined it in early 2025, and the Bureau of Labor Statistics
says it is researching others, naming electronics, books and furniture
([Monthly Labor Review, May 2026](https://www.bls.gov/opub/mlr/2026/article/turning-thrifty-incorporating-secondhand-apparel-into-the-consumer-price-index.htm)).
This index is no substitute for that work: it prices the cheapest listing rather than what people
pay, and it weights models equally rather than by what households spend. What it offers is a daily
reading of the goods that research is looking at, most of them electronics, while the official
series does not yet cover them.

## Citing it

Please link https://usefulhq.com/used-price-index/ and include the date, since the numbers change
daily. Questions, corrections or a category you want pulled: hello@usefulhq.com
