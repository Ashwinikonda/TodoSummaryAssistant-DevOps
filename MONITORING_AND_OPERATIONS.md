# Monitoring and Operations

## 1. Metrics to Monitor

I would monitor the following metrics to understand the health of the application:

- CPU and memory usage of the Kubernetes pods.
- CPU and memory usage of the Kubernetes nodes.
- Number of running, pending and failed pods.
- Application response time.
- HTTP error rate, especially 4xx and 5xx errors.
- Number of requests received by the application.
- Pod restarts and container restart count.
- Database availability and connection problems.
- Disk usage on the nodes.

These metrics help to identify resource problems and application issues before they become bigger problems.



## 2. Important Logs

The main logs I would check are:

- Backend application logs.
- Frontend or web server logs.
- Kubernetes pod logs.
- Database logs.
- Jenkins build logs.
- Deployment and container startup logs.

For the backend, I would especially check logs related to database connection errors, API failures, application exceptions and failed requests.

Jenkins logs are also useful when a build or Docker image creation fails.



## 3. Alerts That Matter

Some alerts that would be useful are:

- Application pod is down.
- Pod keeps restarting.
- High CPU or memory usage.
- High number of HTTP 5xx errors.
- Application response time becomes too high.
- Database connection failure.
- Kubernetes node becomes unavailable.
- Disk space becomes critically low.
- Deployment or health checks fail.

These alerts can help the team react before the users are seriously affected.

### Alerts That Should Not Be Created

Not every small event needs an alert.

For example:

- A single temporary increase in CPU usage.
- One failed request.
- A pod restarting once during a normal deployment.
- Normal application logs.
- Small and temporary changes in response time.

These can create unnecessary alerts and make it harder to notice real problems.



## 4. Detecting Problems Early

Operational problems can be detected early by continuously checking application and infrastructure metrics.

Health checks such as readiness and liveness probes can detect unhealthy application pods.

Logs can help identify errors and exceptions.

Monitoring CPU, memory, response time, error rate and pod restarts can show abnormal behavior before it becomes a major issue.

When an important threshold is crossed, an alert can be sent to the operations team so that they can investigate the problem.