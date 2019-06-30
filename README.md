# rabbitmq
rabbitmq ressources


Here is how to create a user called agent with password agent, set it to be administrator and give it read and write access to all queues in the vhost /

``` 
rabbitmqctl add_user agent agent
rabbitmqctl set_user_tags agent administrator
rabbitmqctl set_permissions -p / agent ".*" ".*" ".*"
```
