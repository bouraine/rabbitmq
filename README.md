# Rabbitmq

## Add User

Here is how to create a user called agent with password agent, set it to be administrator and give it read and write access to all queues in the vhost /

``` 
rabbitmqctl add_user agent agent
rabbitmqctl set_user_tags agent administrator
rabbitmqctl set_permissions -p / agent ".*" ".*" ".*"
```

## .Net connection and sample
```
 public static void Main(string[] args)
  {
      var factory = new ConnectionFactory()
      {
          HostName = "52.143.153.165",
          Port = 5672,
          UserName ="agent",
          Password = "agent"
      };
      using(var connection = factory.CreateConnection())
      using(var channel = connection.CreateModel())
      {
          channel.QueueDeclare(queue: "hello",
              durable: false,
              exclusive: false,
              autoDelete: false,
              arguments: null);

          string message = "Hello World!" + DateTime.UtcNow.Ticks;
          var body = Encoding.UTF8.GetBytes(message);

          channel.BasicPublish(exchange: "",
              routingKey: "hello",
              basicProperties: null,
              body: body);
          Console.WriteLine(" [x] Sent {0}", message);
      }

      Console.WriteLine(" Press [enter] to exit.");
      Console.ReadLine();
  }
   ```
