# CMPE 273 – Week 1 Lab 1: Your First Distributed System (Starter)

This starter provides two implementation tracks:
- `python-http/` (Flask + requests)
- `go-http/` (net/http)

Pick **one** track for Week 1.

## Lab Goal
Build **two services** that communicate over the network:
- **Service A** (port 8080): `/health`, `/echo?msg=...`
- **Service B** (port 8081): `/health`, `/call-echo?msg=...` calls Service A

Minimum requirements:
- Two independent processes
- HTTP (or gRPC if you choose stretch)
- Basic logging per request (service name, endpoint, status, latency)
- Timeout handling in Service B
- Demonstrate independent failure (stop A; B returns 503 and logs error)

## Deliverables
1. Repo link
2. README updates:
   - how to run locally
   - success + failure proof (curl output or screenshot)
   - 1 short paragraph: “What makes this distributed?”

### Running Locally

Open two terminal windows:

**Terminal 1 - Start Service A:**
```bash
go run service-a/main.go
```

**Terminal 2 - Start Service B:**
```bash
go run service-b/main.go
```

<img width="1361" height="240" alt="Screenshot 2026-02-04 at 5 22 30 PM" src="https://github.com/user-attachments/assets/d954a34a-6426-4a56-b81b-31ea218f6cca" />


## Testing

## Sample Output

### Success Output
With both services running:
```
$ curl "http://127.0.0.1:8081/call-echo?msg=hello"

```
<img width="1361" height="240" alt="Screenshot 2026-02-04 at 5 27 04 PM" src="https://github.com/user-attachments/assets/dae947b2-d3d8-48c3-bda5-8a3e48f0301c" />


### Failure Output (Service A Down)
1. Stop Service A (Ctrl+C)
2. Call Service B:
```
$ curl "http://127.0.0.1:8081/call-echo?msg=hello"
```

<img width="1361" height="240" alt="Screenshot 2026-02-04 at 5 27 30 PM" src="https://github.com/user-attachments/assets/f6ed912f-a34e-486f-b8dc-f555488ce1d7" />



## What Makes This Distributed?

This system is considered **distributed** because it consists of two independent processes (Service A and Service B) that communicate over a network using HTTP. Each service runs in its own address space, has its own lifecycle, and can fail independently of the other. Service B depends on Service A but gracefully handles Service A's unavailability by returning a 503 error and logging the failure. This demonstrates key distributed systems concepts: **network communication**, **independent failure modes**, **timeout handling**, and **fault tolerance**. In a real-world scenario, these services could run on different machines or containers, making the distributed nature explicit.


