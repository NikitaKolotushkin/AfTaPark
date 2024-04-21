# Aftapark

## Проект для хакатона от VK&HSE

### Первичный анализ:
+ Проанализировали закономерности в таблицах geo и users
+ Провели статистический анализ данных
+ Исключили "битые" данные, не подходящие для дальнейшей обработки (или мешающие ей)
+ Выдвинули ряд теорий о закономерности распределения искомых данных

![Зависимость кол-ва запросов от возраста](/src/img/ages_requests_graph.png)
![Зависимость кол-ва запросов от возраста](/src/img/correct_ages_requests.png)
![Зависимость кол-ва пользователей от региона](/src/img/distribution_users_by_region.jpeg)

```python
import pandas as pd
import matplotlib.pyplot as plt

parquet_data = pd.read_parquet("C:\Alex\hachoton\part_2.parquet")
parquet_data.to_csv()

df2 = pd.read_csv("C:\Alex\hachoton\geo_dataframe.csv")

merged_df = pd.merge(parquet_data, df2, on='geo_id')
merged_df.to_csv('merged_file.csv', index=False)

region_counts = merged_df['region_id'].value_counts()

plt.figure(figsize=(10, 6))
plt.bar(region_counts.index, region_counts.values)
plt.xlabel('Region')
plt.ylabel('Number of Users')
plt.title('Distribution of Users by Region')
plt.xticks(rotation=45)
plt.show()
```

Пример кода отрисовки гистограммы на основе полученных статистических данных

### Сведение таблиц данных
+ 