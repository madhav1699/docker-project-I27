gcloud compute firewall-rules create allow-all-gke-test \
  --network=default \
  --direction=INGRESS \
  --priority=1000 \
  --action=ALLOW \
  --rules=tcp:0-65535,udp:0-65535,icmp \
  --source-ranges=0.0.0.0/0 \
  --target-tags=gke-my-cluster-342cf3f5-node



  Steps to create a firewall rule in Google Cloud Console
Set up Ruby on Rails baseline testing | Arm Learning Paths
1. Open Firewall rules

Go to the 
Google Cloud Firewall rules page .

Make sure your project is selected: project-8d1b0e22-0c3c-4bb4-81a.

Set up Ruby on Rails baseline testing | Arm Learning Paths
2. Click Create firewall rule

Enter a name such as allow-all-gke-test.

Network: default

Direction: Ingress

Action on match: Allow

Targets: Specified target tags

Target tags: gke-my-cluster-342cf3f5-node

Connect to Google Cloud VMs via SSH on Mac/Linux: A CKAD Guide
3. Configure source and ports

Source IPv4 ranges: preferably your trusted public IP followed by /32

Protocols and ports: Select Allow all if available, or choose Specified protocols and ports and configure TCP and UDP with all ports.

If you need ICMP too, select the applicable option.

Bind ip wrong in redis config - Stack Overflow
4. Create the rule

Click Create and wait for the rule to appear in the firewall rules list.

Alternative: Create the rule using Cloud Shell
To allow all TCP and UDP ports, plus ICMP, to your GKE nodes from any IPv4 address, run:

bash
gcloud compute firewall-rules create allow-all-gke-test \
  --network=default \
  --direction=INGRESS \
  --priority=1000 \
  --action=ALLOW \
  --rules=tcp:0-65535,udp:0-65535,icmp \
  --source-ranges=0.0.0.0/0 \
  --target-tags=gke-my-cluster-342cf3f5-node
This rule is very permissive. Use it only if you understand the exposure and genuinely need public access. It also doesn't automatically enable every IP protocol, such as ESP or AH.

Verify the rule
bash
gcloud compute firewall-rules describe allow-all-gke-test
Then retry your NGINX NodePort:

bash
curl -v --connect-timeout 10 http://34.171.0.94:31242
If it still times out, check the node tags, effective firewall policies, and GKE networking configuration.

Recommendation: For your NGINX test, allowing just TCP port 31242 from your trusted source IP is safer than opening all ports.