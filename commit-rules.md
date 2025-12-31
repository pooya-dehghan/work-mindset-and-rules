# Senior Go Developer: Task Completion & Delivery Cookbook

> **Note:** Use this checklist for every Jira ticket or Pull Request to ensure "Senior-level" output and maintainable code.

---

## 🏗️ Phase 1: Pre-Code Discovery
- [ ] **Jira Alignment:** Have I met every single "Acceptance Criteria" (AC) listed in the task?
- [ ] **Context Gathering:** Do I know why this is being built? (Understanding the business concern).
- [ ] **Bottleneck Analysis:** - **Load:** How does this scale? Is it $O(n)$ or $O(n^2)$?
    - **I/O:** Am I making unnecessary database calls or API requests in a loop?
- [ ] **Edge Case Audit:** What happens if the input is `nil`, `empty`, or the database returns `ErrNoRows`?

---

## 💻 Phase 2: Implementation (The Go Way)
- [ ] **Compilation:** Does the code build without warnings? (`go build ./...`)
- [ ] **Idiomatic Go:**
    - [ ] No "Magic Numbers" (use constants).
    - [ ] Small, focused functions.
    - [ ] Correct use of `internal/` vs `pkg/` folders.
- [ ] **Error Handling:** - [ ] Errors are wrapped with context: `fmt.Errorf("context: %w", err)`.
    - [ ] No ignored errors (no `_ = function()`).
- [ ] **Concurrency Safety:** - [ ] If using Goroutines, did I run the race detector? (`go test -race ./...`)
    - [ ] Are all channels closed or managed by a `context.Context`?

---

## 🧪 Phase 3: Verification & Testing
- [ ] **Unit Tests:** - [ ] High-priority logic is covered via **Table-Driven Tests**.
    - [ ] Mocks are used for external dependencies.
- [ ] **Integration Tests:** - [ ] Happy path is tested against a real DB (e.g., via Docker/Testcontainers).
- [ ] **Performance:** - [ ] For hot-paths, did I run `go test -bench=.`?
- [ ] **Linter Check:** Does it pass the company `golangci-lint`?

---

## 📊 Phase 4: Observability & Documentation
- [ ] **Logging:** Are logs structured? (e.g., `slog.Info("msg", "user_id", id)`).
- [ ] **Metrics:** Did I add a Prometheus counter or histogram for this new feature?
- [ ] **Documentation:** - [ ] Public functions have comments.
    - [ ] README is updated if env vars or setup changed.
    - [ ] Swagger/OpenAPI spec is updated for API changes.

---

## 🚀 Phase 5: The Merge Request (Self-Review)
- [ ] **The "Dirty Diff" Check:** Have I removed all `fmt.Println`, commented-out code, and "TODO" comments?
- [ ] **PR Description:** Does the description explain **WHY** the change was made, not just **WHAT** changed?
- [ ] **Small PRs:** If this is over 500 lines, can I split it into smaller, more reviewable chunks?
- [ ] **Testing Evidence:** Did I paste a log snippet or a screenshot proving it works in the PR comment?

---

## 🛠️ Phase 6: Post-Deployment
- [ ] **Monitoring:** Did I check the logs/Grafana dashboards immediately after it hit staging/production?
- [ ] **Stakeholder Update:** Did I move the Jira ticket and notify the requester?