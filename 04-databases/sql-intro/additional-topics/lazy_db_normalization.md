# Lazy Normalization

1. Each table should map to only 1 model e.g. _products_ table maps to your _Product_ model
2. Each table row should map to only 1 instance of the model
3. Columns should not store collections, this includes duplicating columns with similar column names e.g. _\|\| Phone Nos \|\|_ and _\|\| Phone No 1 \| Phone No 2 \| phone No 3 \|\|_ are both bad.
4. Rows should avoid duplicate value data and should instead store references to other tables e.g. a _category_ column on a _books_ table should store foreign keys for entries on the _categories_ table rather than a category name
5. Don’t store stuff you can work out easily from other object data

## Most Important Rule

You can break any of these rules, as long as it is done consciously and with good reason e.g. don’t make tables for the sake of making them. Don’t spend too much time design ERDs and lose focus of the product, especially when it is in the infancy stage - YAGNI.

