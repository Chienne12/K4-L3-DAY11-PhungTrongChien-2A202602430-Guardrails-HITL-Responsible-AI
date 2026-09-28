# Checklist Lab Day 11 — Guardrails, HITL, Responsible AI

## Luồng tổng thể

`User → Rate Limiter → Input Guardrails → LLM → Output Guardrails → Egress`

Song song: `Audit Log + Monitoring`

## Checkpoint 1 — Setup

- [x] Python 3.10+ hoạt động.
- [x] Đã tạo và kích hoạt `.venv`.
- [x] Đã cài `requirements.txt`.
- [x] `.env` có `OPENROUTER_API_KEY`.
- [x] `.env` có `RED_TEAM_PROVIDER=openai` hoặc `gemini` và API key tương ứng.
- [x] Không commit `.env`.
- [p ] Chạy `pytest tests/smoke -q` và tất cả test pass.

## Checkpoint 2 — Blue Guardrails

- [x] `detect_injection()` có ít nhất 5 pattern và xử lý Unicode ẩn.
- [x] `topic_filter()` chặn topic cấm và câu ngoài ngân hàng.
- [ ] `InputGuardrailPlugin` chặn trước khi gọi LLM.
- [ ] `content_filter()` che số điện thoại, email, CCCD, API key và password.
- [ ] `OutputGuardrailPlugin` thay dữ liệu nhạy cảm bằng `[REDACTED]`.
- [ ] Chạy `python src/main.py --part 2`.
- [ ] Injection bị chặn, câu ngân hàng được cho qua, secret bị che.

## Checkpoint 3 — Pipeline

- [ ] `RateLimitPlugin` dùng sliding window theo `user_id`.
- [ ] `AuditLogPlugin` ghi input, output, layer chặn và latency.
- [ ] `MonitoringAlert` tính metrics và sinh cảnh báo.
- [ ] Plugin đúng thứ tự: rate limit → input guardrail → output guardrail.
- [ ] Egress chỉ cho HTTPS thuộc `api.vinbank.example` và payload không có dữ liệu nhạy cảm.
- [ ] `run_assignment_suite()` chạy đủ 4 nhóm test.
- [ ] Chạy `python src/main.py --part 3`.
- [ ] Có `outputs/results.json`.
- [ ] Có `outputs/audit_log.json`.
- [ ] Có `outputs/metrics.json`.
- [ ] Chạy `pytest tests/public/test_results_contract.py -q` và test pass.

## Checkpoint 4 — Red Team

- [ ] Đã thay 5 prompt `TODO` trong `src/attacks/attacks.py`.
- [ ] Mỗi prompt dùng một kỹ thuật tấn công khác nhau.
- [ ] Chạy `python src/main.py --part 4`.
- [ ] Có `outputs/attack_results.json`.
- [ ] Có `outputs/unsafe_attack_result.json`.
- [ ] Có `outputs/guards_attack_result.json`.
- [ ] Red làm lộ ít nhất một secret theo yêu cầu bài.

## Checkpoint 5 — Kiểm tra và nộp

- [ ] Chạy `pytest tests/smoke -q`.
- [ ] Chạy `pytest tests/public -q`.
- [ ] Chạy `python scripts/grade.py --submission-dir . --out outputs/grade_report.json`.
- [ ] `outputs/results.json` đúng schema.
- [ ] `outputs/attack_results.json` chứa kết quả Red và Red Advance.
- [ ] Không có API key thật trong Git.
- [ ] Repo đúng tên quy định.
- [ ] Đã push GitHub và nộp link đúng hạn.

