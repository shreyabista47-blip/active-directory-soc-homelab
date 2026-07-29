# Group Policy Configuration

## Objective

The objective of this phase was to configure Group Policy Objects (GPOs) in the Active Directory environment to apply centralized security settings to domain-connected systems.

Group Policy allows administrators to manage security configurations, user settings, and computer policies across an enterprise environment.

---

## Group Policy Objects Created

The following policies were configured:

- Default Domain Policy
- Workstation Security Baseline

These policies were applied to the `cyberlab.local` domain environment.

---

## Security Policies Configured

The lab included configuration of security-related policies such as:

- Password Policy
- Account Lockout Policy
- Security Baseline Settings

These settings help simulate enterprise security controls commonly used in Windows domain environments.

---

## Client Policy Application

The Windows 11 client was configured to receive policies from the Domain Controller.

Policy updates were tested using:

```cmd
gpupdate /force
```

Successful update message:

```
Computer Policy update has completed successfully.
User Policy update has completed successfully.
```

---

## Group Policy Verification

The applied policies can be verified using:

```cmd
gpresult /r
```

A screenshot showing the applied Group Policy Objects will be added after final verification.

<!-- Add image here later:
![Applied Group Policy](../images/client01-gpresult.png)
-->

---

## Result

The Active Directory environment successfully demonstrated centralized policy management.

Completed:

- ✅ Created Group Policy Objects
- ✅ Configured security policies
- ✅ Applied policies to domain clients
- ✅ Tested policy updates using gpupdate
- ⏳ Final gpresult evidence pending
