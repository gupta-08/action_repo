# action‑repo 🚦

A tiny GitHub repository whose *only* purpose is to generate real‑world
webhook events (Push • Pull Request • Merge) for my companion project
[`webhook-repo`](https://github.com/gupta-08/webhook-repo).

> **Why a separate repo?**  
> The assignment asks for one repo that *emits* webhooks (`action-repo`)
> and another that *receives* + displays them (`webhook-repo`).  
> Keeping them independent mirrors a real production setup.

---

## 🔗 1. Webhook Configuration

1. Go to **Settings ▸ Webhooks ▸ “Add webhook”**  
2. **Payload URL**   `https://<your-tunnel>.loca.lt/webhook`  
3. **Content type**  `application/json`  
4. **Events to send** select:  
   - Push  
   - Pull request  
   - (Optionally) “Let me select individual events” ➜ “Pull request” & “Merge request”  
5. Click **Add webhook**.  
   You should see a green ✓ “Webhook created”.

> **Note:** While developing locally I expose my Flask app on port 5000
> and tunnel it via **localtunnel** / **ngrok**.

---

## 🏎️ 2. How to Trigger Each Event

| Action                            | What to do in this repo                                  | Webhook Fires |
|----------------------------------|----------------------------------------------------------|---------------|
| **Push**                         | `git commit` ➜ `git push origin main`                    | `push`        |
| **Pull Request (opened)**        | Create a branch, push, open PR to `main`                 | `pull_request` (`"action":"opened"`) |
| **Merge (closed + merged)**      | Merge the PR via GitHub UI (or `gh pr merge`)            | `pull_request` (`"action":"closed", "merged":true`) + auto‑`push` |


