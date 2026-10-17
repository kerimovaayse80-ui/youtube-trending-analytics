# YouTube Trending Videos: Methodology and Content Strategy Insights

## 1. Project Overview

This project explores engagement patterns and performance indicators in YouTube trending videos using the US YouTube Trending dataset. The analysis investigates relationships between video metrics, differences across content categories, publication weekday patterns, and the relationship between popularity and audience engagement.

The main objective is to transform raw data into meaningful insights that can help explain how trending videos perform and inform content strategy decisions.

## 2. Dataset Description

The project uses two files:

- `USvideos.csv` — contains video information, including views, likes, dislikes, comments, tags, publication time, trending date, and category ID.
- `US_category_id.json` — contains category information used to map category IDs to readable category names.

The original dataset contained **40,949 rows and 16 columns**. After mapping category names, it contained 17 columns.

Initial data quality checks identified:
- 570 missing values in video descriptions.
- 48 exact duplicate rows.
- 6,351 unique video IDs.

## 3. Methodology

### 3.1 Data Cleaning and Preparation

The dataset was loaded using pandas, and category IDs were mapped to category names using the JSON file. Missing values, duplicate rows, and unique video IDs were examined to understand the dataset's quality.

The date columns were converted into datetime format to support time-based analysis. The data was sorted by trending date, and duplicate video IDs were removed while keeping the first occurrence. This created a video-level dataset with one retained record per video.

### 3.2 Feature Engineering

Several metrics were created to evaluate video performance:

- **Engagement Rate:** The percentage of views associated with likes, dislikes, and comments.
- **Like Rate:** The percentage of views associated with likes.
- **Dislike Rate:** The percentage of views associated with dislikes.
- **Days to Trend:** The number of calendar days between publication and the recorded trending date.
- **Tag Count:** The number of tags associated with each video.

The engagement rate was calculated as:

`(likes + dislikes + comment_count) / views * 100`

The like rate was calculated as:

`likes / views * 100`

The dislike rate was calculated as:

`dislikes / views * 100`

Videos with zero or fewer views were excluded before calculating rate metrics.

### 3.3 Correlation Analysis

Pearson correlation was used to investigate linear relationships between numerical variables, including views, likes, dislikes, comments, engagement rate, and tag count.

The main observed results were:

| Relationship | Correlation |
|---|---:|
| Views and likes | 0.76 |
| Comments and dislikes | 0.68 |
| Tag count and views | 0.04 |

Correlation analysis helps identify relationships between variables, but it does not prove that one variable causes another.

### 3.4 Category Performance Analysis

Videos were grouped by category to calculate:

- Average views.
- Average engagement rate.
- Average like rate.
- Number of videos.

This analysis helped compare categories in terms of popularity and audience interaction.

### 3.5 Publication Weekday Analysis

The publication weekday was extracted from the publication timestamp. Average views, median views, video counts, and engagement statistics were compared across weekdays.

Both mean and median values were considered because a small number of highly popular videos can significantly influence average performance.

### 3.6 Top Video Analysis

The ten videos with the highest view counts were examined alongside their engagement rates and other performance metrics.

Additional comparisons identified videos with relatively high views but low engagement and videos with relatively low views but high engagement. This helped demonstrate the difference between reaching a large audience and generating interactions.

### 3.7 Data Visualization

The project included several visualizations:

- Pearson correlation heatmap.
- Average views by category.
- Average engagement rate by category.
- Video views by publication weekday.
- Log-scale comparison of views by weekday.
- Scatter plot of views versus engagement rate by category.

These visualizations made it easier to identify patterns, compare groups, and communicate the findings.

## 4. Five Key Insights

### Insight 1: Views and Likes Have a Strong Positive Correlation

The correlation between views and likes was **0.76**, indicating a strong positive linear relationship. Videos with more views generally tended to receive more likes.

This suggests that views and likes are closely associated indicators of video performance, although the relationship does not establish causation.

### Insight 2: Music Leads in Average Views and Engagement

The Music category recorded the highest average views, approximately **1.39 million**, and the highest average engagement rate at **8.23%**.

This indicates that Music performed strongly in both reach and audience interaction among the categories in the analyzed dataset.

Howto & Style also demonstrated relatively high engagement, with an average engagement rate of **5.97%**.

### Insight 3: High View Counts Do Not Always Mean High Engagement

The most-viewed video in the analyzed records, *Maluma – El Préstamo (Official Video)*, received approximately **48.43 million views**, but its engagement rate was only about **1.43%**.

This demonstrates that popularity and engagement measure different aspects of performance. A video may reach a large audience without generating a similarly high proportion of interactions.

### Insight 4: Engagement Rates Differ Across Publication Weekdays

Friday had the highest average engagement rate at **5.24%**, while Sunday had the lowest at **4.32%**. Saturday recorded the highest median engagement rate at **4.13%**.

These results suggest that publication weekday is worth investigating when studying engagement. However, the analysis does not prove that the publication day itself causes these differences.

### Insight 5: Tag Count Has Almost No Linear Relationship with Views

The correlation between tag count and views was **0.04**, indicating almost no linear relationship in this dataset.

This suggests that simply increasing the number of tags was not associated with higher view counts in the analyzed records. However, tag relevance and quality were not measured by tag count alone, so the result does not mean that tags are unimportant.

## 5. Content Strategy Insights

The following recommendations are based on the observed patterns. They should be treated as hypotheses to test rather than guaranteed strategies.

### 5.1 Measure Both Reach and Engagement

Views indicate the size of a video's audience, while engagement rate measures interactions relative to views.

**Recommendation:** Evaluate videos using multiple metrics, including views, engagement rate, like rate, and comments. Avoid judging performance solely by view count.

### 5.2 Study Successful Content Categories

Music performed strongly in both average views and engagement, while Howto & Style also achieved a relatively high engagement rate.

**Recommendation:** Examine successful videos to identify useful patterns in topics, formats, titles, thumbnails, presentation, and audience preferences. Apply relevant lessons to the target channel rather than assuming that results will be identical across categories.

### 5.3 Test Different Publication Weekdays

Friday had the highest average engagement rate in this dataset, but other factors may influence the result, including video topic, channel size, audience habits, and category distribution.

**Recommendation:** Test comparable videos across different weekdays over a sustained period. Use channel-specific analytics to determine whether the observed weekday pattern applies to a particular audience.

### 5.4 Focus on Relevant Metadata Rather Than Tag Quantity

The near-zero correlation between tag count and views suggests that using more tags alone was not associated with higher view counts in this analysis.

**Recommendation:** Prioritize accurate and relevant tags, clear titles, and informative descriptions. Evaluate performance using actual channel analytics rather than assuming that more tags automatically produce more views.

### 5.5 Define the Goal of Each Video

A video designed to maximize reach may perform differently from one designed to encourage discussion or build a community.

**Recommendation:** Define the objective before evaluating performance. Use views to assess reach and engagement-related metrics to understand audience interaction. Compare videos with similar goals and formats wherever possible.

### 5.6 Consider Sample Size and Outliers

Some videos receive exceptionally high view counts, which can influence averages. In addition, certain categories contain relatively few records. For example, Shows has only 4 videos, while Nonprofits & Activism has 14 in the category summary.

**Recommendation:** Consider median values and sample sizes alongside averages. Avoid drawing strong conclusions from categories with very small samples.

## 6. Limitations

Several limitations should be considered when interpreting the findings:

- The analysis covers videos in the available US trending dataset, not every video uploaded to YouTube.
- The video-level analysis retains one record per video, so it does not represent the complete daily history of trending appearances.
- Correlation does not establish causation.
- Outliers and skewed distributions can influence averages and Pearson correlation values.
- Category averages based on small samples may be less reliable.
- Tag count does not measure tag relevance or metadata quality.
- Publication weekday alone cannot explain differences in engagement.
- The calculated engagement rate includes likes, dislikes, and comments relative to views. It does not measure watch time, retention, shares, or overall audience sentiment.

## 7. Future Improvements

The project could be extended through the following steps:

1. Analyze the complete daily trending history instead of retaining only one record per video.
2. Compare median views and engagement rates across categories and channels.
3. Investigate additional features, such as video duration, title length, and metadata characteristics.
4. Explore log transformations or robust statistical methods to reduce the influence of extreme values.
5. Test weekday patterns while accounting for differences in category and channel.
6. Build a predictive model to estimate video performance if suitable features and evaluation data are available.

## 8. Conclusion

This project applied data cleaning, feature engineering, exploratory data analysis, correlation analysis, grouping, and visualization to investigate YouTube trending-video performance.

The findings show that views and likes are strongly associated, category performance varies, and high popularity does not necessarily correspond to high engagement. The analysis also identified differences in engagement across publication weekdays and found almost no linear relationship between tag count and views.

From a content strategy perspective, the results highlight the importance of evaluating multiple performance metrics, understanding category differences, and testing recommendations with real channel data.

Overall, this project demonstrates how data analytics can transform raw data into meaningful observations that support more informed decisions about digital content performance.
