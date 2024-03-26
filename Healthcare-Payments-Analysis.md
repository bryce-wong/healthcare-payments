Healthcare Payments Analysis
================
Bryce Wong
2024-03-25

## Importing data

``` r
research_payments = read_csv(file = "./data/PGYR22_P011824/OP_DTL_RSRCH_PGYR2022_P01182024.csv")
research_payments = janitor::clean_names(research_payments)

ownership_payments = read_csv(file = "./data/PGYR22_P011824/OP_DTL_OWNRSHP_PGYR2022_P01182024.csv")
ownership_payments = janitor::clean_names(ownership_payments)

deleted_payments = read_csv(file = "./data/PGYR22_P011824/OP_REMOVED_DELETED_PGYR2022_P01182024.csv")
deleted_payments = janitor::clean_names(deleted_payments)
```

``` r
general_payments = 
  GET("https://openpaymentsdata.cms.gov/api/1/datastore/query/df01c2f8-dc1f-4e79-96cb-8208beaf143c/0?offset=0&count=true&results=true&schema=true&keys=true&format=csv&rowIds=false") |> 
  content("parsed")
```

``` r
general_payments %>% 
  ggplot(aes(x = total_amount_of_payment_usdollars)) +
  geom_histogram()

research_payments %>% 
  filter(total_amount_of_payment_us_dollars < 10000) %>% 
  ggplot(aes(x = total_amount_of_payment_us_dollars)) +
  geom_histogram(bins = 15)

ownership_payments %>% 
  filter(total_amount_invested_us_dollars < 100000) %>% 
  ggplot(aes(x = total_amount_invested_us_dollars)) +
  geom_histogram(bins = 15)
```
