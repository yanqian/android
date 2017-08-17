## How to release your APK with github api

1. Apply an API token of your repo
Check the github [auth](https://github.com/blog/1509-personal-api-tokens) document and [personal api key](https://github.com/blog/1509-personal-api-tokens).

2. Go the check the [relase api](https://developer.github.com/v3/repos/releases/) page

3. Add new tag with `git tag v0.1 && git push --tag` and you also can use api to create new tag

4. creata a new release with `POST /repos/:owner/:repo/releases`
eg:
> curl  -H "Content-Type:application/json" -X POST -u username:YOUR-PERSONAL-API-TOKEN --data '{"tag_name": "v0.1", "name": "v0.1", "body":"release with apk", "draft":false, "prelease":false}'  https<span></span>://github.douban.com/api/v3/repos/yanqian/android/releases/ 


5. Find the `GET /repos/:owner/:repo/releases` to get release id and upload url from response
eg: 
> curl -u username:YOUR-PERSONAL-API-TOKEN https<span></span>://github.douban.com/api/v3/repos/yanqian/android/releases

6. Upload your assets with `POST https://<upload_url>/repos/:owner/:repo/releases/:id/assets?name=foo.zip`
eg:
> curl  -H "Content-Type:application/vnd.android.package-archive" -X POST -u username:YOUR-PERSONAL-API-TOKEN --data-binary @app-release.apk https<span></span>://github.douban.com/api/uploads/repos/yanqian/android/releases/323/assets?name=app-release.apk

## other ways
- with command of `github-release` from [github-release](https://github.com/aktau/github-release)
- GUI to upload. check with [github-help](https://github.com/waylau/github-help/blob/master/Creating%20Releases%20%E5%88%9B%E5%BB%BA%E5%8F%91%E5%B8%83%E5%8C%85.md)