---
title: "Fix the Plots"
output: 
  html_document:
    keep_md: true
    theme: paper
---

<!---The following chunk allows errors when knitting--->



<br>

## Question 1
Why is this not running?

```r
coronavirus %>%  
  filter(type == "confirmed") %>% 
  group_by(date) %>% 
  summarize(total_cases = sum(cases)) %>% 
  ggplot(mapping = aes(x = date, y = total_cases)) %>%
  geom_line()
```

<br>

## Question 2

What is the problem here?

```r
top10_countries <- coronavirus %>% 
  filter(type == "confirmed") %>%
  group_by(Country.Region) %>%
  summarize(total_cases = sum(cases)) %>%
  arrange(-total_cases) %>% 
  head(10) %>% 
  .$Country.Region

coronavirus %>%  
  filter(type = confirmed, Country.Region %in% top10_countries) %>% 
  group_by(Country.Region, date) %>% 
  summarize(total_cases = sum(cases)) %>% 
  ggplot(mapping = aes(x = date, y = total_cases, color = Country.Region)) +
  geom_line()
```

<br>

## Question 3
What is the difference between the two code chunks below (look in the `ggplot()` line)? Which would you use and why?

```r
coronavirus %>%  
  filter(type == "confirmed", Country.Region %in% top10_countries) %>% 
  group_by(Country.Region, date) %>% 
  summarize(total_cases = sum(cases)) %>% 
  ggplot(mapping = aes(x = date, y = total_cases, color = Country.Region)) +
  geom_line()
```
