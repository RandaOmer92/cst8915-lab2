# CST8915 Lab 2: 12-Factor Algonquin Pet Store on Four Azure VMs

**Student Name**: Randa Omer

**Student ID**: 041079985

**Course**: CST8915 Full-stack Cloud-native Development

**Semester**: Fall 2026

---

## Demo Video

🎥 [Watch Demo Video](https://youtu.be/nf0JVFIjlOs)

---

## Service Repositories

- Order Service: https://github.com/RandaOmer92/order-service
- Product Service: https://github.com/RandaOmer92/product-service
- Store Front: https://github.com/RandaOmer92/store-front

---

## Deployment

| Component | VM | Region | Port |
|---|---|---|---|
| RabbitMQ | rabbitmq-vm | Mexico Central | 5672 |
| Product Service (Rust) | product-vm | Mexico Central | 3030 |
| Order Service (Node.js) | order-vm | Mexico Central | 3000 |
| Store Front (Vue.js) | store-vm | Canada Central | 8080 |

---

## Reflection Questions

### 1. What changes did you make to the `order-service` and `product-service` to comply with the **Configurations** and **Backing Services** factors of the 12-Factor App methodology?

I took the settings out of the code and put them in a `.env` file. In the order-service, the RabbitMQ address and the port are now in `.env`. In the product-service, the port is in `.env`. I added `dotenv` to both services so they can read the `.env` file. I also added `.env` to `.gitignore` so it does not go to GitHub. RabbitMQ runs on its own VM, and the order-service connects to it using the address in `.env`. If I want a different RabbitMQ, I just change the address.

### 2. Why is it important to use environment variables instead of hard-coding configurations in your application?

With environment variables, I can change settings without changing the code. When I put each service on a different VM, I only changed the IPs in `.env`. I did not edit the code. It also keeps my RabbitMQ password safe because `.env` is not uploaded to GitHub.

### 3. Why is it important to have **separate repositories** for each microservice? How does this help maintain independence and scalability of each service?

Each service has its own repository, so each one is separate. I can change one service without affecting the others. Each service can also use a different language, like Rust, Node.js, and Vue.js in this lab. If one service gets busy, like the order-service, I can add more copies of just that one.

---

## Challenges and Learnings

- B2s and B1ms sizes were not available on my Azure for Students account, so I used Standard_B2als_v2 for all 4 VMs.
- My account only allowed 3 public IPs and 6 vCPUs in Mexico Central, so I created store-vm in Canada Central. This did not affect the app because all services talk to each other using public IPs.
- I learned that the RabbitMQ `guest` account only works on the same machine, which is why the lab uses a separate `orderapp` account for the order-service to connect from another VM.
- My laptop IP changed when I worked from a different place, so I had to update the NSG rules to allow my new IP.
