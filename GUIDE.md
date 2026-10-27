# DevOps Capstone – Copy-Paste Guide

Replace `YOUR_GITHUB_USERNAME` everywhere (including README.md) with your GitHub username.
Repo name used below: `devops-capstone-project`.

---

## LAB 1 — Planning (Tasks 1–6)

### 1. Create the repo
1. Open https://github.com/ibm-developer-skills-network/aolwx-devops-capstone-template
2. **Use this template → Create a new repository** → name `devops-capstone-project` → **Public** → Create.

### 2. Add the user story template (Task 2)
In GitHub: **Add file → Create new file** → name: `.github/ISSUE_TEMPLATE/user-story.md` → paste contents of `.github/ISSUE_TEMPLATE/user-story.md` from this zip → Commit.

URL to submit:
`https://github.com/YOUR_GITHUB_USERNAME/devops-capstone-project/blob/main/.github/ISSUE_TEMPLATE/user-story.md`

### 3. Create the Kanban board
Repo → **Projects → Link a project → New project → Board** → name `devops-capstone-project`.
Rename/add columns so you have exactly:
`New Issues` · `Icebox` · `Product Backlog` · `Sprint Backlog` · `In Progress` · `Review/QA` · `Done`
(Board ⋯ → Workflows: set "Item added to project" → status **New Issues**.)

### 4. Create the user stories (Issues → New issue → User Story → add to project)

Create ALL of these now. Use the exact titles.

**1. Set up the development environment**
```
**As a** developer
**I need** to set up the development environment
**So that** I can develop and test the account service

### Details and Assumptions
    * The template repo has a working Create function and a test suite
    * Need PostgreSQL running in Docker

### Acceptance Criteria
Given the development environment is set up
When I run make tests
Then all tests pass with good coverage
```

**2. Read an account from the service**
```
**As a** customer
**I need** to read my account from the service
**So that** I can see my account details

### Details and Assumptions
    * Read by account id using GET /accounts/{id}

### Acceptance Criteria
Given an account exists
When I send GET /accounts/{id}
Then I receive the account with 200 OK
```

**3. List all accounts in the service**
```
**As a** service administrator
**I need** to list all accounts in the service
**So that** I can see every customer account

### Details and Assumptions
    * GET /accounts returns a JSON list (empty list is OK)

### Acceptance Criteria
Given accounts exist
When I send GET /accounts
Then I receive a list of all accounts with 200 OK
```

**4. Update an account in the service**
```
**As a** customer
**I need** to update my account in the service
**So that** my details stay current

### Details and Assumptions
    * PUT /accounts/{id} with a JSON body

### Acceptance Criteria
Given an account exists
When I send PUT /accounts/{id} with new data
Then the account is updated and returned with 200 OK
```

**5. Delete an account from the service**
```
**As a** customer
**I need** to delete my account from the service
**So that** my data is removed when I leave

### Details and Assumptions
    * DELETE /accounts/{id} returns 204 even if not found

### Acceptance Criteria
Given an account exists
When I send DELETE /accounts/{id}
Then I receive 204 NO CONTENT and the account is gone
```

**6. Need the ability to automate continuous integration checks**
```
**As a** developer
**I need** CI checks to run automatically
**So that** every push and pull request is linted and tested

### Details and Assumptions
    * Use GitHub Actions with flake8 and nosetests

### Acceptance Criteria
Given code is pushed to main
When the CI workflow runs
Then linting and tests run and the build badge shows passing
```

**7. Need to add security headers and CORS policies**
```
**As a** service provider
**I need** security headers and CORS policies
**So that** the service is protected from common web attacks

### Details and Assumptions
    * Use Flask-Talisman and Flask-Cors

### Acceptance Criteria
Given the service is running
When a request is made
Then security headers and CORS headers are returned
```

**8. Containerize your microservice using Docker**
```
**As a** developer
**I need** to containerize the microservice using Docker
**So that** it can be deployed anywhere

### Details and Assumptions
    * Python 3.9-slim base, gunicorn on port 8080, non-root user

### Acceptance Criteria
Given a Dockerfile
When I build and run the image
Then the service responds on port 8080
```

**9. Deploy your Docker image to Kubernetes**
```
**As a** service provider
**I need** to deploy the Docker image to Kubernetes
**So that** the service is scalable and highly available

### Details and Assumptions
    * Use deployment and service manifests in /deploy

### Acceptance Criteria
Given the image is in the registry
When I apply the manifests
Then the pods are running and the service is reachable
```

**10. Create a CD pipeline to automate deployment to Kubernetes**
```
**As a** developer
**I need** a CD pipeline to automate deployment to Kubernetes
**So that** changes are deployed automatically

### Details and Assumptions
    * Use Tekton: clone, lint, test, build, deploy

### Acceptance Criteria
Given code is pushed
When the pipeline runs
Then the new image is built and deployed to OpenShift
```

📸 **Task 3:** all 10 stories in **New Issues** → `planning-userstories-done.png`

### 5. Triage
- Move stories 6–10 → **Icebox**. 📸 **Task 4:** `planning-productbacklog-done.png`
- Move stories 1–5 → **Product Backlog**.
- Labels: story 1 → `technical debt` (create the label if it doesn't exist). Stories 2–5 → `enhancement`.
- 📸 **Task 5:** Product Backlog with labels → `planning-labels-done.png`

### 6. Sprint 1
- Project settings → **+ New field**:
  - `Estimate` (Number)
  - `Iteration` (Iteration, 2 weeks)
- Set estimates: 1 → 3, 2 → 3, 3 → 3, 4 → 5, 5 → 3
- Set Iteration 1 on stories 1–5.
- Move them to **Sprint Backlog**.
- 📸 **Task 6:** `planning-kanban-done.png` (make sure Estimate and Iteration are visible on the cards or in table view)

---

## LAB 2 — REST API (Tasks 7–18)

Open the Skills Network **Cloud IDE** → Terminal → New Terminal:

```bash
git clone https://github.com/YOUR_GITHUB_USERNAME/devops-capstone-project.git
cd devops-capstone-project
bash ./bin/setup.sh
exit
```

Open a NEW terminal:
```bash
cd devops-capstone-project
make install
make db
make tests
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

Move story 1 to **In Progress**. Then:
- Replace `service/routes.py`, `service/__init__.py`, `tests/test_routes.py`, `requirements.txt` with the files from this zip.
- Copy `setup.cfg` as-is.

```bash
pip install -r requirements.txt
make lint
make tests        # all green, coverage ≥ 95%
git add -A
git commit -m "Implement list, read, update, delete + security headers"
git push          # username = GitHub user, password = Personal Access Token
```

URL for **Task 7**:
`https://github.com/YOUR_GITHUB_USERNAME/devops-capstone-project/blob/main/setup.cfg`

📸 Move stories to Done one at a time and screenshot each:

| Task | Story | Screenshot |
|------|-------|------------|
| 8 | 1 (Set up dev env) | `rest-techdebt-done.png` |
| 9 | 2 (Read) | `read-accounts.png` |
| 10 | 3 (List) | `list-accounts.png` |
| 11 | 4 (Update) | `update-accounts.png` |
| 12 | 5 (Delete) | `delete-accounts.png` |

### cURL outputs (Tasks 13–17)

Terminal 1:
```bash
make run
```

Terminal 2 — run each command, then copy the command AND its output into the named file:

```bash
# rest-create-done
curl -i -X POST http://127.0.0.1:5000/accounts \
  -H "Content-Type: application/json" \
  -d '{"name":"John Doe","email":"john@doe.com","address":"123 Main St.","phone_number":"555-1212"}'

# rest-list-done
curl -i -X GET http://127.0.0.1:5000/accounts

# rest-read-done   (use the id returned by create, usually 1)
curl -i -X GET http://127.0.0.1:5000/accounts/1

# rest-update-done
curl -i -X PUT http://127.0.0.1:5000/accounts/1 \
  -H "Content-Type: application/json" \
  -d '{"name":"John Doe","email":"john@doe.com","address":"456 New St.","phone_number":"555-1111"}'

# rest-delete-done
curl -i -X DELETE http://127.0.0.1:5000/accounts/1
```

Shortcut — this saves the command + output straight into each file:
```bash
{ echo '$ curl -i -X GET http://127.0.0.1:5000/accounts'; curl -i -X GET http://127.0.0.1:5000/accounts; } > rest-list-done
```

**Sprint 2:**
- Move stories 6 and 7 → **Sprint Backlog**, Iteration 2, estimates 5 and 3.
- 📸 **Task 18:** `sprint2-plan.png`

---

## LAB 3 — CI (Tasks 1, 19–21)

1. Add `.github/workflows/ci-build.yaml` from the zip.
2. Put the README.md from the zip in the repo (edit your username in the badge line).
3. Push:
   ```bash
   git add -A
   git commit -m "Add CI workflow and badge"
   git push
   ```
4. GitHub → **Actions** → open the green run → **build** job → expand every step. Copy all the log text into `ci-workflow-done` (**Task 19**).
   Alternative with GitHub CLI: `gh run view --log > ci-workflow-done`
5. URLs:
   - **Task 21:** `https://github.com/YOUR_GITHUB_USERNAME/devops-capstone-project/blob/main/.github/workflows/ci-build.yaml`
   - **Task 1:** `https://github.com/YOUR_GITHUB_USERNAME/devops-capstone-project/blob/main/README.md` (badge must show **passing**)
6. 📸 Story 6 → Done → `ci-kanban-done.png` (**Task 20**)

---

## LAB 4 — Security (Tasks 22–25)

The `__init__.py` from the zip already has Talisman + CORS, and the tests already cover them.

```bash
make tests 2>&1 | tee security-headers-done
```
That file is **Task 23**.

- **Task 22:** `https://github.com/YOUR_GITHUB_USERNAME/devops-capstone-project/blob/main/service/__init__.py`
- 📸 Story 7 → Done → `security-kanban-done.png` (**Task 24**)
- Move stories 8, 9, 10 → **Sprint Backlog**, Iteration 3, estimates 3/5/8.
- 📸 `sprint3-plan.png` (**Task 25**)

---

## LAB 5 — Docker + Kubernetes/OpenShift (Tasks 26–31)

Copy `Dockerfile`, `deploy/deployment.yaml`, and `deploy/service.yaml` from the zip, then push.

Run in the lab's OpenShift terminal (inside the repo):

```bash
# Postgres in the cluster
oc create -f postgresql-ephemeral-template.json
oc new-app postgresql-ephemeral
oc get pods          # wait until postgresql is Running

# Build and push the image
docker build -t accounts:1 .
docker tag accounts:1 us.icr.io/$SN_ICR_NAMESPACE/accounts:1
docker push us.icr.io/$SN_ICR_NAMESPACE/accounts:1

# Task 30
docker images > kube-images
```

`kube-images` must show the REPOSITORY, TAG, IMAGE ID, CREATED, and SIZE columns.

```bash
# Deploy (fills the image name into the manifest)
sed -i "s|IMAGE_NAME_HERE|us.icr.io/$SN_ICR_NAMESPACE/accounts:1|g" deploy/deployment.yaml
kubectl apply -f deploy/
kubectl get all -l app=accounts > kube-deploy-accounts      # Task 31
cat kube-deploy-accounts    # must show deployment, pods, replicaset, service

# Restore the placeholder for Lab 6 before committing
sed -i "s|us.icr.io/$SN_ICR_NAMESPACE/accounts:1|IMAGE_NAME_HERE|g" deploy/deployment.yaml
```

**Task 26 – app output on 8080:**
```bash
oc create route edge accounts --service=accounts
oc get routes
```
Open the route URL (or Skills Network Toolbox → Launch Application → port 8080). Copy the JSON into `kube-app-output`. It looks like:
```json
{"name":"Account REST API Service","paths":"http://.../accounts","version":"1.0"}
```

- **Task 29:** `https://github.com/YOUR_GITHUB_USERNAME/devops-capstone-project/blob/main/Dockerfile`
- 📸 Story 8 → Done → `kube-docker-done.png` (**Task 27**)
- 📸 Story 9 → Done → `kube-kubernetes-done.png` (**Task 28**)

---

## LAB 6 — Tekton CD Pipeline (Tasks 32–33)

Copy the `tekton/` folder from the zip and push it. Then:

```bash
# Catalog tasks
tkn hub install task git-clone
tkn hub install task flake8

# Your tasks, pvc and pipeline
kubectl apply -f tekton/pvc.yaml
kubectl apply -f tekton/tasks.yaml
kubectl apply -f tekton/pipeline.yaml
tkn task ls
tkn clustertask ls      # buildah and openshift-client should be listed
```

If `git-clone` is listed as a ClusterTask, keep `kind: ClusterTask` in `pipeline.yaml`. If you installed it with `tkn hub` instead, delete the `kind: ClusterTask` line under the clone task.

Run it:
```bash
tkn pipeline start cd-pipeline \
    -p repo-url="https://github.com/YOUR_GITHUB_USERNAME/devops-capstone-project.git" \
    -p branch=main \
    -p build-image=image-registry.openshift-image-registry.svc:5000/$SN_ICR_NAMESPACE/accounts:1 \
    -w name=pipeline-workspace,claimName=pipelinerun-pvc \
    -s pipeline \
    --showlog
```

Then save the logs and check every task succeeded:
```bash
tkn pipelinerun logs --last > pipelinerun.txt     # Task 32
tkn pipelinerun ls                                 # STATUS must be Succeeded
```

📸 Story 10 → Done → `cd-pipeline-done.png` (**Task 33**)

---

## Submission cheat-sheet

| Task | What to submit |
|------|----------------|
| 1 | `.../blob/main/README.md` |
| 2 | `.../blob/main/.github/ISSUE_TEMPLATE/user-story.md` |
| 7 | `.../blob/main/setup.cfg` |
| 21 | `.../blob/main/.github/workflows/ci-build.yaml` |
| 22 | `.../blob/main/service/__init__.py` |
| 29 | `.../blob/main/Dockerfile` |
| 13–17, 19, 23, 26, 30–32 | paste the contents of the matching text file |
| everything else | the matching screenshot |
