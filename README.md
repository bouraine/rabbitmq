# Rabbitmq

# Run with Docker

```
docker run -d --hostname local-rabbit --name local-rabbit -e RABBITMQ_DEFAULT_USER=user -e RABBITMQ_DEFAULT_PASS=password rabbitmq:3-management
```

## .Net connection and end sample
```
 public static void Main(string[] args)
  {
      var factory = new ConnectionFactory()
      {
          HostName = "IP-ADDRESS",
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

# Azure 

Choose : RabbitMQ Cluster by Bitnami
Open 15672 and 5672 port

## Download rabbitmqadmin

http://{IP-ADDRESS}:15672/cli/rabbitmqadmin

## Add User

Here is how to create a user called agent with password agent, set it to be administrator and give it read and write access to all queues in the vhost /

``` 
rabbitmqctl add_user agent agent
rabbitmqctl set_user_tags agent administrator
rabbitmqctl set_permissions -p / agent ".*" ".*" ".*"
```

## Enable plugins

rabbitmq-plugins list
rabbitmq-plugins enable PLUGIN_NAME 

## Connecting from console admin
   
https://docs.bitnami.com/oci/infrastructure/rabbitmq/administration/use-admin-console/
https://www.rabbitmq.com/management-cli.html

## Access to web console

 http://{IP-ADDRESS}:15672/
