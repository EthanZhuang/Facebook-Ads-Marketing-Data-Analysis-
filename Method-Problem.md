###### tags: `工作日誌`

# 行銷數據分析相關報告(Facebook Business Manager)
[Facebook Business Manager](https://business.facebook.com/adsmanager/manage/campaigns?act=132799196821088&business_id=743007782446785)

## Obejctive:
需要將**FB marketing Ads** 上面的資料爬取下來，放入不僅是**Google Sheets**內，還有**SQL和Tableau**上。

### 要求資料格式:
欄位名稱：(依序)
。時間分段(Time Period)：周一到周日
> 1.行銷活動名稱(campaign_name)
2.廣告組合名稱(adset_name)
3.花費金額(spend)
4.成果類型(objective)
5.成果(APP是下載次數、直播或其他網站是打賞金額) (results)
6.行動應用程式安裝次數(APP install)
7.訂閱轉換價值(不確定 - Convension Rate Ranking)
8.購買轉換價值(不確定 - Convension Rate Ranking)
9.分析報告開始(date_start)
10.分析報告結束(date_stop)
>

## 20201023 
### 1. 了解Facebook Marketing API 運用
[Facebook for Developer - Marketing API Setup 101](https://developers.facebook.com/ads/blog/post/v2/2018/11/01/marketing-api-setup-101/)

[Github - Facebook-python-business-sdk](https://github.com/facebook/facebook-python-business-sdk?fbclid=IwAR1IF-dAmqaYunRjw8EgQLXQlbezsrWzzpPTMZXGTkoCFtja0YbP11r4Av4)

前置需要的資料:
> 1. Account_Id
> 2. API Access Approvals
> 3. System User ID
> 4. Access Token
> 5. Ad Accounts, Pages

```python=
access_token = 'EAAJqMzKi2IsBAJp9LxmjKZBfEG5P5WXqzUO8f4eXoUYRr9beYIxSRXKFuXMUTVZCMaJnwewurtWpq93qiyB7X8wfDotZCQZC5M1B9YZAgIuiTEY5cHgOZAhmxGpOin6DM0HZAPcAmzs8YDBnAs4YzS9D1D5jZCLWLUkdhGVhbmddkAZDZD'
ad_account_id = 'act_132799196821088'
#app_secret = 'b3700e4944af0e889dc572179bd6800d'
#app_id = '679718078830731'

```

### 2. Set_up & Get to know the Facebook API

調整fields = {paras}， 可以獲取marketing sheets欄位內的資料
```python=
http://graph.facebook.com/v8.0/679718078830731?fields = asset_feed_spec, call_to_action_type, object_stroy_spec & access_token = EAAJqMzKi2IsBAJp9LxmjKZBfEG5P5WXqzUO8f4eXoUYRr9beYIxSRXKFuXMUTVZCMaJnwewurtWpq93qiyB7X8wfDotZCQZC5M1B9YZAgIuiTEY5cHgOZAhmxGpOin6DM0HZAPcAmzs8YDBnAs4YzS9D1D5jZCLWLUkdhGVhbmddkAZDZD
```
放在Google Url上面，FB Ads回傳的資料:
```json=
{
   "category": "Business",
   "link": "https://www.facebook.com/games/?app_id=679718078830731",
   "name": "\u7c4c\u78bcK\u7dda",
   "namespace": "cmoneychipk",
   "id": "679718078830731"
}
```

[Virtual Environment in python](https://ithelp.ithome.com.tw/articles/10199980)

**Brief introduction**: This will let you know the basic information of the FB-Marketing-API。
[【VIDEO】01 - Intro to the Facebook Marketing API](https://www.youtube.com/watch?v=to4uTxSNo6Q&ab_channel=kitchn_io)

[【VIDEO】Scrape Facebook & Instagram Ads Insight Data API for Marketing & Performance Metrics (2020)](https://www.youtube.com/watch?v=c10IPpfh0e0&ab_channel=StevesieData)

[Python Facebook Ads Api简介](https://linpingta.github.io/blog/2015/03/07/python-facebook-ads-api-introduction/)

[Facebook Marketing API - 获取洞察力的Python - 达到用户请求限制](https://xbuba.com/questions/47834523)


## Facing Problems
1. 沒有Token的權限(非使用者)無法抓資料
![](https://i.imgur.com/lvIfZle.png)


## Ads Account Insights
[Ads Account Ingihts Reference](https://developers.facebook.com/docs/marketing-api/reference/ad-account/insights/)

2. 現在跳過權限，直接用網頁方式看可不可以取資料:
![](https://i.imgur.com/5zExLNY.png)

```
Access_token = 

EAAJqMzKi2IsBAJp9LxmjKZBfEG5P5WXqzUO8f4eXoUYRr9beYIxSRXKFuXMUTVZCMaJnwewurtWpq93qiyB7X8wfDotZCQZC5M1B9YZAgIuiTEY5cHgOZAhmxGpOin6DM0HZAPcAmzs8YDBnAs4YzS9D1D5jZCLWLUkdhGVhbmddkAZDZD
```

```python=
graph.facebook.com/v8.0/act_132799196821088/insights?date_preset = last_30d&fields = campaign_namee&access_token = EAAJqMzKi2IsBAJp9LxmjKZBfEG5P5WXqzUO8f4eXoUYRr9beYIxSRXKFuXMUTVZCMaJnwewurtWpq93qiyB7X8wfDotZCQZC5M1B9YZAgIuiTEY5cHgOZAhmxGpOin6DM0HZAPcAmzs8YDBnAs4YzS9D1D5jZCLWLUkdhGVhbmddkAZDZD
```

下面這個已經不能使用了
```python=
graph.facebook.com/v8.0/679718078830731/insights?date_preset = last_30d&fields = campaign_name EAAJqMzKi2IsBAJp9LxmjKZBfEG5P5WXqzUO8f4eXoUYRr9beYIxSRXKFuXMUTVZCMaJnwewurtWpq93qiyB7X8wfDotZCQZC5M1B9YZAgIuiTEY5cHgOZAhmxGpOin6DM0HZAPcAmzs8YDBnAs4YzS9D1D5jZCLWLUkdhGVhbmddkAZDZD
```

# 20201026 