# Daikibo Web Activity Incident Report

## 1. Overview

This report summarizes the analysis of Daikibo’s web activity logs related to a suspected data leak from the internal manufacturing status dashboard.

## 2. Scope

- Time window: 2021-06-25 to 2021-06-29
- Data source: `web_requests.log` (sample subset in `web_requests_sample.log`)
- Focus: Identifying suspicious user activity and assessing external access risk.

## 3. External Access Assessment

- All observed IP addresses are in the `192.168.x.x` private range.
- The dashboard is hosted on Daikibo’s intranet.
- No public IP addresses or external scanning activity were observed.

**Conclusion:** The dashboard cannot be accessed directly from the internet; any attacker would need VPN or internal access.

## 4. User Activity Summary

Most users (e.g., `3ZBu4TumfETr3ruTL4A7ZM`, `obbi5BSPBt2K66ZGP8cyTJ`, `dBFjPM7T4dW7zMu7pqn8wn`, `8CVNc7CPYFWSjbi7MHbTHB`) exhibit normal, human-like browsing patterns:
- Standard login flows.
- Occasional API calls.
- Irregular timing consistent with manual interaction.

## 5. Suspicious Activity

**User ID:** `1FtyZHWX9c8JJTZiYqq4Bs`  
**IP Address:** `192.168.0.73`

### Indicators:

- Multiple API calls to `/api/factory/status` and `/api/factory/machine/status`.
- Systematic enumeration of machines in multiple factories (`meiyo`, `berlin`).
- Short intervals between requests, suggesting scripted automation.
- No corresponding dashboard refreshes between API calls.

**Assessment:** This activity is consistent with automated data extraction using a valid authenticated session.

## 6. Likely Cause

The most likely cause of the data leak is the misuse or compromise of the account associated with user ID `1FtyZHWX9c8JJTZiYqq4Bs`, used to systematically query machine status data via the API from an internal IP address.

## 7. Recommendations

- Investigate the user account `1FtyZHWX9c8JJTZiYqq4Bs` (owner, role, recent behavior).
- Review endpoint rate limiting and API access controls.
- Implement anomaly detection for automated API usage patterns.
- Enforce stronger monitoring on internal accounts accessing sensitive telemetry data.
