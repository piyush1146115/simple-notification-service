# simple-notification-service

Ref: https://www.freecodecamp.org/news/build-a-real-time-notification-system-with-go-and-kafka/

Let's Test the Real-Time Notification System👨‍🔬🖥️👩‍🔬
Now that the producer and consumer are ready, it’s time to see the system in action.

1. **Start the producer:**
   Open up a terminal, move into the `simple-notification-service` directory, and run the producer with the following command:

```bash
go run cmd/producer/producer.go
```
2. **Start the consumer:**
   Open up a second terminal window, navigate to the `simple-notification-service` directory, and start the consumer by running:
```bash
go run cmd/consumer/consumer.go
```

3. **Sending notifications:**
   With both producer and consumer running, you can simulate sending notifications. Open up a third terminal and use the below curl commands to send notifications:

User 1 (Emma) receives a notification from User 2 (Bruno):
```bash
curl -X POST http://localhost:8080/send -d "fromID=2&toID=1&message=Bruno started following you."
```

User 2 (Bruno) receives a notification from User 1 (Emma):
```bash
curl -X POST http://localhost:8080/send -d "fromID=1&toID=2&message=Emma mentioned you in a comment: 'Great seeing you yesterday, @Bruno\!'"
```

User 1 (Emma) receives a notification from User 4 (Lena):
```bash
curl -X POST http://localhost:8080/send -d "fromID=4&toID=1&message=Lena liked your post: 'My weekend getaway\!'"
```

4. **Retrieving notifications:**
   Finally, you can fetch the notifications of a specific user. You can use the below curl commands to fetch notifications:

Retrieving notifications for User 1 (Emma):
```bash
curl http://localhost:8081/notifications/1
```

Output:
```json
{"notifications": [{"from": {"id": 2, "name": "Bruno"}, "to": {"id": 1, "name": "Emma"}, "message": "Bruno started following you."}]}
{"notifications": [{"from": {"id": 4, "name": "Lena"}, "to": {"id": 1, "name": "Emma"}, "message": "Lena liked your post: 'My weekend getaway!'"}]}
```

In the above output, you see a JSON response listing all the notifications for Emma. As you send more notifications, they accumulate, and you can fetch them using the consumer’s API.