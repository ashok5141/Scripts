### GitHub Secret Retrieval Script 
- Trying to retrieve the secret keys and password where the GitHub PAT key has the overly push permission. [secrets_retrive.yml](https://raw.githubusercontent.com/ashok5141/Scripts/refs/heads/main/git/secrets_retrive.yml)
```bash
gedit cicd.yml # add the necessary changes to retrieve the file
git add .
git commit -m "Added secrets" # Note commit name
git push # if it has the specific branch mention that `--set-upstream origin infinity-123ashok`
gh run list # list push
gh run view 20525446925 --log # it has the webhooks, secrets printing with base64, and run time retrieve the scripts
```
##### Mitigation
- Least privilege access, the Developer should not have the push permission. Some should review, then proceed
- **TruffleHog** can filter the plain text password but not in this case, because the here not in the plain text `{{ secrets.FLAG }}`, but not protected for **DNS Exfiltration** using [webhooks](https://webhook.site/)
- Policy as Code **(Checkov / OPA)** block the curl command something reading like The company's Firewall sees the runner trying to talk to an **unknown IP and kills the connection**.
- Some companies run security agents inside the Ubuntu Runner Runtime Security **(Falco / Tetragon)**
