# Go Web App - Complete CI/CD Project 🚀

A simple Go web application with **fully automated** deployment using modern DevOps practices.

## What Does This Project Do?

This is a **Go web application** that automatically builds, tests, and deploys itself to Kubernetes whenever you push code to GitHub. No manual work needed!

## How It Works (Simple Explanation)

1. **You write code** and push it to GitHub
2. **GitHub Actions** automatically:
   - Tests your code
   - Builds a Docker container
   - Uploads it to DockerHub with a unique version number
3. **ArgoCD** sees the new version and automatically deploys it to Kubernetes
4. **Your app is live!** Users can access it

**That's it!** You just push code, and everything else happens automatically.

## The Tech Stack (What We Use)

- **Go** - Programming language for the web app
- **Docker** - Packages the app in a container
- **Kubernetes (Minikube)** - Runs the app
- **GitHub Actions** - Automatically builds and tests code
- **ArgoCD** - Automatically deploys to Kubernetes
- **Helm** - Manages Kubernetes configuration

## Quick Start

### 1. Access the Application

Once deployed, you can access the app at:
- **URL:** `http://go-web-app.com` (add to `/etc/hosts` first)
- **Or via NodePort:** `http://<your-ip>:30080`

### 2. Make Changes

1. Edit the code in `go-web-app/` folder
2. Push to GitHub:
   ```bash
   git add .
   git commit -m "Your changes"
   git push
   ```
3. Wait 2-3 minutes
4. Your changes are automatically live!

## Project Structure

```
go-web-app-deploy/
├── go-web-app/              # The actual Go application
│   ├── main.go              # Main application code
│   ├── Dockerfile           # How to package the app
│   └── static/              # Web pages (HTML)
│
├── .github/workflows/       # Automation rules
│   └── Ci.yaml              # CI/CD pipeline definition
│
├── Helm/                    # Kubernetes deployment config
│   └── go-web-app-chart/    # Helm chart for deployment
│
└── k8s/                     # Alternative Kubernetes configs
```

## What Happens Behind the Scenes?

### When You Push Code:

1. **GitHub Actions CI Pipeline Runs** (2-3 minutes)
   - Compiles your Go code
   - Runs tests to make sure nothing is broken
   - Builds a Docker image
   - Uploads image to DockerHub with a unique tag (e.g., `18933966846`)
   - Updates the Helm chart with the new tag
   - Commits the change back to GitHub

2. **ArgoCD Detects the Change** (30 seconds)
   - Sees the updated Helm chart in GitHub
   - Pulls the new Docker image from DockerHub
   - Updates your Kubernetes deployment
   - Your app restarts with the new version

3. **Result:** Your changes are live!

## Key Concepts Explained

### What is CI/CD?
**CI/CD** = Continuous Integration / Continuous Deployment
- **CI:** Automatically test and build your code when you push changes
- **CD:** Automatically deploy the tested code to production

### What is GitOps?
Your **Git repository is the source of truth**. Whatever is in Git gets deployed to production. Change Git = Change production.

### Why Docker?
Docker packages your app with everything it needs to run. Same container works on your laptop, test server, and production.

### Why Kubernetes?
Kubernetes automatically manages your app:
- Restarts it if it crashes
- Scales it when traffic increases
- Routes traffic to healthy instances

### Why Helm?
Helm is like a package manager for Kubernetes. It makes deploying complex apps simple.

## Viewing Your Pipeline

### GitHub Actions:
- Go to your GitHub repo
- Click "Actions" tab
- See all builds and their status

### ArgoCD Dashboard:
- URL: `http://<your-ip>:31706`
- Username: `admin`
- Password: (check installation notes)

### Kubernetes Status:
```bash
# See running pods
kubectl get pods

# See services
kubectl get svc

# See deployments
kubectl get deployments
```

## Troubleshooting

### Pipeline Fails?
- Check the "Actions" tab in GitHub
- Read the error logs
- Fix the code and push again

### App Not Accessible?
```bash
# Check if pods are running
kubectl get pods

# Check pod logs
kubectl logs <pod-name>

# Check service
kubectl get svc go-web-app-service
```

### ArgoCD Not Syncing?
- Login to ArgoCD dashboard
- Click "Refresh" or "Sync"
- Check for any error messages

## Important Files

- **main.go** - Your application code
- **Ci.yaml** - Defines the CI/CD pipeline
- **values.yaml** - Kubernetes deployment configuration
- **Dockerfile** - Instructions to build Docker image

## Security Notes

### Secrets Used:
- `DOCKERHUB_USERNAME` - Your DockerHub username
- `DOCKERHUB_TOKEN` - DockerHub access token
- `TOKEN` - GitHub personal access token

These are stored securely in GitHub Secrets (Settings → Secrets).

## Benefits of This Setup

✅ **No manual deployments** - Push code and it deploys automatically  
✅ **Always tested** - Code is tested before deployment  
✅ **Version control** - Every version has a unique tag  
✅ **Easy rollback** - Can go back to any previous version  
✅ **Visible history** - See all changes in Git  
✅ **Professional workflow** - Industry-standard practices  

## Learning Resources

- **GitHub Actions:** https://docs.github.com/en/actions
- **ArgoCD:** https://argo-cd.readthedocs.io/
- **Kubernetes:** https://kubernetes.io/docs/
- **Docker:** https://docs.docker.com/
- **Helm:** https://helm.sh/docs/

## Support

If something doesn't work:
1. Check the logs (GitHub Actions, kubectl logs)
2. Review the error messages
3. Google the error (you're not the first to see it!)
4. Check if all secrets are configured correctly

---

**Remember:** The beauty of this setup is that you only need to focus on writing code. The pipeline handles everything else! 🎉
