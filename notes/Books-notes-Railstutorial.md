# When should test
* 与应用代码相比，如果测试代码特别简短，倾向于先编写测试；
* 如果对想实现的功能不是特别清楚，倾向于先编写应用代码，然后再编写测试，并改进实现方式；
* 安全是头等大事，保险起见，要为安全相关的功能先编写测试；
* 只要发现一个问题，就编写一个测试重现这种问题，避免回归，然后再编写应用代码修正问题；
* 尽量不为以后可能修改的代码（例如 HTML 结构的细节）编写测试；
* 重构之前要编写测试，集中测试容易出错的代码。

# Linux process
* `sudo lsof -i:$PORTNO`: look a port
* `ps aux | grep $name`: look a process
* `pkill -15 -f $name`: kill a process by name
* `kill -15 $pid`: kill a process by pid
