---
layout: page
title: Jupyter Notebooks from Lambda Servers
slim: true
---

1. Log-in into a Lmabda server using your credentials via ssh.
1. Once in the Lambda server execute the following command:
   
   ```jupyter notebook --no-browser --port=8080```
   - This will open the lambda server and will provide a token.
1. On your local systems type:
   ```ssh -L 8080:localhost:8080 <your account>@<lambda server>```
   
   - This command is basically forwarding port 8080 on the lambda server to your local system.
1. On your system browser go to: https://localhost:8080 and that will access the jupyter notebook interface from the lambda server.

Troubleshooting:
- Port Usage:
    If there are other person using that port (e.g. 8080) the step 2 will fail.  You need to select another port.  If this happens, the new port must be used on step 4.
