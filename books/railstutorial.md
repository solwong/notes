## When should test

* 与应用代码相比，如果测试代码特别简短，倾向于先编写测试；
* 如果对想实现的功能不是特别清楚，倾向于先编写应用代码，然后再编写测试，并改进实现方式；
* 安全是头等大事，保险起见，要为安全相关的功能先编写测试；
* 只要发现一个问题，就编写一个测试重现这种问题，避免回归，然后再编写应用代码修正问题；
* 尽量不为以后可能修改的代码（例如 HTML 结构的细节）编写测试；
* 重构之前要编写测试，集中测试容易出错的代码。

## Linux process

* `sudo lsof -i:$PORTNO`: look up a port status
* `ps aux | grep $name`: look up a process status
* `pkill -15 -f $name`: kill a process by name
* `kill -15 $pid`: kill a process by pid

## Gems related

`guard`: auto test
`spring`: speed the test
`bootstrap-sass`: beauty the app

## Troubleshooting

- `error for some template cannot be found`: ensure your server is restart after bundle install
- db:seed数据总是不能用，试试关闭服务器后，执行db数据

## Works flow

1. `git checkout -b $branch`
2. do sth.
3. `git commit`
4. `git checkout master`
5. `git merge`
6. `git push github master`
7. `git push heroku master`
8. `git run db:migrate`

## Debug

### Console

```ruby
def show
  debugger
end
```

### Web pages

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
  <%= debug(params) if Rails.env.development? %>
  </body>
</html>
```

## Security

### Got your cookie

1. 使用包嗅探工具截获不安全网络中传输的 cookie；
2. 获取包含记忆令牌的数据库；
3. 使用跨站脚本（Cross-Site Scripting，简称 XSS）攻击；
4. 获取已登录用户的设备访问权。

## Test

如果某个功能暂时没有覆盖测试，可以先用`raise`代替，当测试覆盖时，此处一定抛出异常。

## 功能方法封装原则

- 数据库操作放置到Model，逻辑操作可以在help中封装，最后controller执行help的封装
