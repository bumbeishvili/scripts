# scripts

[StackExchangeDataExplorer](https://data.stackexchange.com/stackoverflow/query/new)

#### StackOverFlow Top Users By Location Per Tag 
```sql 
SELECT --TOP 20 
    rank() over (partition by TagName order by count(*) desc) ranking,
    TagName,
    Users.Id [User Link],
    DisplayName,
    COUNT(*) AS UpVotes ,
    Users.Location
FROM Tags
    INNER JOIN PostTags ON PostTags.TagId = Tags.id
    INNER JOIN Posts ON Posts.ParentId = PostTags.PostId
    INNER JOIN Votes ON Votes.PostId = Posts.Id and VoteTypeId = 2
    INNER JOIN Users ON Posts.OwnerUserId = Users.Id
WHERE 
    LOWER(Location) LIKE LOWER('%##CountryName##%') 
GROUP BY TagName, Users.Id,DisplayName , Users.Location
ORDER BY TagName,ranking
```
