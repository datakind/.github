## Description

## Deployment Readiness\*

### Testing

Describe or check:

- [ ] Created or updated unit, feature, and/or integration tests  
- [ ] Typical manual testing in the local env browser, dev pipeline, etc.

### Deployment Notes

Describe or check:

- [ ]  No special deployment steps required

### Rollback Plan

Describe or check:

- [ ]  Standard revert is sufficient (`git revert`)

## Reviewer Guidance / Questions\*

## Screenshots / Testing Evidence\*

## SOC2 Change Management Checklist

- [ ] **None of the below are true in this code**  
- [ ] New roles/permissions are introduced without review and approval by the product manager  
- [ ] Hardcoded credentials, secrets, or API keys are present in this code  
- [ ] Secrets are being managed outside of the approved secrets management process (e.g., GitHub Secrets, environment variables)  
- [ ] PII or sensitive data handling is introduced or changed without being reviewed against our data classification policy  
- [ ] Sensitive data is written to logs  
- [ ] Input validation and sanitization is missing  
- [ ] An unnecessary attack surface has been introduced (e.g., unused endpoints, open ports, debug modes left enabled)  
- [ ] Common vulnerabilities have been introduced in the code (inc. any dependencies added or updated)  
- [ ] No review for common vulnerabilities has been conducted   
- [ ] Not tested in a non-production environment  
- [ ] Breaking changes to existing APIs or integrations with downstream consumers being notified  
- [ ] Performance impact has not been considered or acceptable  
- [ ] Appropriate audit logging is missing for any security-relevant actions introduced by this change  
- [ ] Log entries contain sensitive or PII data  
- [ ] All existing tests do not pass locally (`./vendor/bin/pest`)

Provide justification if you are submitting a PR with any boxes checked other than the first.

---

Reminder for Reviewers: By approving this PR you are confirming that you have reviewed the code for correctness, security, and compliance with our engineering and SOC 2 standards. Do not approve PRs where SOC 2 checklist items are checked without documented justification.

\*Optional