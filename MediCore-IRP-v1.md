MediCore Health Systems — Incident Response Plan

Version: 1.0
Date: June 2026
Owner: Lead Cloud Security Architect

2. Roles and Responsibilities
Role	Title	Channel	SLA
Incident Lead	Cloud Security Architect	Teams	15 min
DPO	External DPO	Direct phone	2 hours
CTO	Chief Technology Officer	Teams	2 hours
ICO	Information Commissioner's Office	report.ico.org.uk	72 hours
NHS Trust	Per contract	Secure email	4 hours
3. Detection Triggers (Phase 2)
Alert	Who Notified	SLA	Phase
CPU > 80% for 3+ min	Incident Lead	15 min	Phase 2
3+ failed SSH attempts in 5 min	Incident Lead + CTO	5 min	Phase 2
Database access not from web tier	DPO	Immediate	Phase 2
Patient data access outside 22:00–06:00	DPO + CTO	Immediate	Phase 2
Storage access from outside VNet	Incident Lead	10 min	Phase 2
4. Containment (Phase 3) — Risk R01: Unauthorised SSH Access

Preserve logs first:

aws logs export-task

or

az monitor log query

Isolate the VM:

az network nsg rule update --name AllowSSH --access Deny

Revoke compromised credentials:

aws iam delete-access-key --access-key-id [key]
Notify CTO and DPO via Teams (not email due to response-time requirements).
5. Eradication (Phase 4)
Identify the entry vector from auth.log.
Patch SSH configuration:
MaxAuthTries 3
AllowUsers sysadmin
Rebuild the VM from a clean snapshot.
Run a Trivy vulnerability scan on the rebuilt image before reconnecting.
Verify that audit logging is operational.
6. GDPR Breach Notification (Article 33)
Time	Action
T+0	Breach identified — 72-hour notification clock starts
T+2h	Notify CTO and DPO via Teams/phone
T+8h	DPO completes risk assessment (High / Medium / Low)
T+24h	Draft ICO notification via report.ico.org.uk
T+72h	Submit ICO notification, even if investigation remains ongoing
T+72h+	Assess Article 34 requirement to notify affected patients if risk is high

Required ICO statement:

Investigation ongoing — further update will be provided within 5 working days.

Git Commands
git add compliance/MediCore-IRP-v1.md \
        screenshots/23-irp-document.png \
        screenshots/24-notification-chain.png

git commit -m "Week 4: IRP v1.0 + ICO notification chain (Art.32 + Art.33 evidence)"

git push
