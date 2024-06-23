Postmortem: Web Stack Debugging Project Outage

Issue Summary
Duration of the Outage:
Start Time: June 20, 2024, 16:30 SAST
End Time: June 20, 2024, 18:00 SAST

Impact:
The primary web application was inaccessible, resulting in a total service outage for all users. Approximately 100% of our user base experienced downtime and were unable to access the service.

Root Cause:
The root cause was a misconfigured load balancer that led to a cascading failure of the web server cluster, ultimately causing the entire application to become unavailable.

Timeline
16:30 SAST: Issue detected by automated monitoring system alerting of HTTP 500 errors.
16:32 SAST: On-call engineer confirms the issue and begins initial investigation.
16:35 SAST: Engineers suspect database overload due to increased traffic, begin database performance checks.
16:45 SAST: Misleading path: Team investigates potential DDoS attack but finds no supporting evidence.
17:00 SAST: Escalated to senior engineering team due to lack of progress.
17:15 SAST: Senior engineer identifies high load on the web servers, points to load balancer configuration.
17:30 SAST: Misleading path: Attempts to restart web servers individually, issue persists.
17:45 SAST: Discovery of misconfigured load balancer sending excessive requests to a single web server.
17:50 SAST: Load balancer configuration corrected, gradual recovery of web services begins.
18:00 SAST: Full service restored and normal traffic resumed.
Root Cause and Resolution
Root Cause:
The primary issue was a misconfiguration in the load balancer setup. A recent update to the load balancer software introduced a bug that caused it to incorrectly route all traffic to a single web server instead of distributing it evenly across the server cluster. This caused the overloaded server to fail, triggering a cascade effect that took down the entire application.

Resolution:
The engineering team identified the misconfigured load balancer by analyzing traffic patterns and server load. The load balancer configuration was corrected to ensure even distribution of incoming traffic across all web servers. Once the configuration was fixed, the web servers were able to recover, and normal service was restored.

Corrective and Preventative Measures
Improvements/Fixes:

Load Balancer Configuration Management: Implement a more rigorous configuration management process for load balancer settings.
Automated Testing: Introduce automated testing for load balancer configurations to catch errors before deployment.
Enhanced Monitoring: Set up more granular monitoring to detect uneven traffic distribution early.
Incident Response Training: Conduct regular training sessions for the engineering team on handling load balancer-related issues.
Tasks to Address the Issue:

Patch Load Balancer Software: Apply the latest patches to fix the known bug.
Add Monitoring on Load Balancer Traffic: Implement detailed monitoring to track traffic distribution in real-time.
Review Load Balancer Configuration: Conduct a comprehensive review of the current load balancer setup.
Automate Configuration Deployment: Use infrastructure-as-code tools to manage and deploy load balancer configurations.
Conduct Load Balancer Failure Drills: Simulate load balancer failures and practice response procedures regularly.
By addressing these specific areas, we aim to prevent similar incidents in the future and ensure a more robust and resilient web application service.
