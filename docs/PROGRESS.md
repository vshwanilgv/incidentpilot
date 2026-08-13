# IncidentPilot — Phase 2A Progress

Tracking against the 25-step method (Phase 2A spec, section 38) and the
completion checklist (section 37). Update this file at the end of every
task so a new session can pick up without re-deriving context.

## Method sequence (spec section 38)

- [x] 1. Inspect existing repository — N/A, fresh scaffold
- [x] 2. Understand Phase 1 deployment — captured from spec doc (Prometheus/Loki/Tempo/Grafana on k3s, verified working)
- [ ] 3. Identify Prometheus/Loki/Tempo endpoints — pending (need URLs/ports from your k3s cluster)
- [x] 4. Define data models — **DONE this task**
- [ ] 5. Implement Prometheus adapter
- [ ] 6. Test Prometheus adapter
- [ ] 7. Implement Loki adapter
- [ ] 8. Test Loki adapter
- [ ] 9. Implement Tempo adapter
- [ ] 10. Test Tempo adapter
- [ ] 11. Implement Kubernetes adapter
- [ ] 12. Test Kubernetes adapter
- [ ] 13. Implement Alertmanager webhook
- [ ] 14. Implement normalization
- [ ] 15. Implement PostgreSQL persistence
- [ ] 16. Implement incident correlation
- [ ] 17. Implement context builder
- [ ] 18. Implement topology
- [ ] 19. Implement deployment context
- [ ] 20. Implement security context
- [ ] 21. Implement API
- [ ] 22. Deploy to k3s
- [ ] 23. Run controlled failure
- [ ] 24. Verify complete incident lifecycle
- [ ] 25. Document architecture

## Task log

### Task 1 — Repo scaffold + canonical models (DONE)

- Created `incidentpilot/` repo skeleton (services/observation-gateway,
  shared, infrastructure, docs).
- Implemented canonical `Observation`, `Incident`, `Evidence` Pydantic
  models in `shared/models/` per spec sections 11, 18, 21-22.
- 13 unit tests in `shared/tests/test_models.py`, all passing (validated
  in sandbox with Python 3.12 / pydantic 2.9.2 / pytest 8.3.3).
- **Design decision needing your confirmation**: the spec lists both
  `status` and `current_phase` as Incident fields without fully
  separating their meaning. Implemented as two independent axes:
  `status` (open/resolved/closed) and `current_phase` (the Phase 2A
  DETECTED → ... → READY_FOR_INVESTIGATION state machine). Flag if you
  intended something else.
- Not yet decided: exact Postgres schema / ORM (SQLAlchemy vs raw SQL)
  — deferred to the persistence task (step 15).

### Task 2 — TBD

Next candidate per the method sequence: identify your actual
Prometheus/Loki/Tempo endpoints and k3s access details (step 3), then
implement + test the Prometheus adapter (steps 5-6).
