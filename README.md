# git-adsecurity-assessment-report-for-cti-junior.com
CTI califonia training  institution
# Security Assessment Report: cti-junior.com

**Assessment Date:** 2025-06-25  
**Tester:** kayon-assefa  
**Scope:** http://cti-junior.com

---

## 1. Reconnaissance & Information Gathering

- **WHOIS:** Domain information collected; no sensitive data or misconfigurations observed.
- **DNS/NSLookup:** Domain resolves correctly; no subdomains were discovered.
- **Port Scan:** Only standard web ports (80, 443) are open. No unusual or unexpected services detected.
- **Technology Stack:** Website powered by Next.js (modern JavaScript framework).
- **SSL/TLS:**  
  - Chrome browser: Reports site as "Secure".
  - Firefox browser: Reports site as "Not Secure" (potential certificate or mixed content issue).
  - SSL checked; no major vulnerabilities detected, but browser inconsistency should be addressed.

---

## 2. Application Assessment

### A. Authentication

- **Login Page:**  
  - Located at `/admin`.  
  - Requires email and password.  
  - No “forgot password” functionality.
  - Error message is generic (“email or password invalid”), which is good practice.
  - No user enumeration possible.
  - Login form uses HTTP 200 OK for all responses.

- **Brute-force & Rate Limiting:**  
  - No visible brute-force protection mechanism (e.g., CAPTCHA, account lockout) detected from limited testing.
  - No evidence of rate limiting after multiple failed logins.

### B. Input Validation

- **XSS:**  
  - Input fields tested, but reflected and stored XSS not detected.
- **Open Redirects:**  
  - Common patterns tested; no vulnerable endpoints found.

### C. Directory and File Discovery

- **Directory/File Bruteforce:**  
  - No sensitive or hidden files/directories found (`.env`, `.git`, backups, source maps, etc.).
  - No accessible admin panels or dev/test endpoints beyond `/admin`.

### D. Security Headers

- Most standard security headers present.
- Need to confirm presence of:
  - `Content-Security-Policy`
  - `X-Frame-Options`
  - `Strict-Transport-Security`
  - `X-Content-Type-Options`

### E. SSL/TLS

- **Mixed Content or Certificate Issue:**  
  - Chrome and Firefox have different security status indicators.
  - May be due to missing intermediate certificate or mixed content (HTTP assets on HTTPS site).
  - Requires further investigation and remediation.

---

## 3. Notable Gaps and Potential Weaknesses

1. **Inconsistent SSL/TLS Security**
   - Firefox reports site as "Not Secure" while Chrome reports "Secure".
   - Possible causes: missing intermediate cert, mixed content, or browser-specific TLS settings.
   - **Recommendation:** Use [SSL Labs](https://www.ssllabs.com/ssltest/analyze.html) to diagnose and fix.

2. **No Brute-Force or Rate-Limit Protection**
   - Login form does not implement visible brute-force prevention.
   - **Recommendation:** Add rate limiting, CAPTCHA, or account lockout on failed login attempts.

3. **No Password Recovery**
   - No “Forgot Password” option available.
   - **Recommendation:** Add secure password recovery to improve usability.

4. **No User Enumeration**
   - This is a positive finding (no usernames/emails can be enumerated via login errors).

5. **Security Headers**
   - Most headers present, but ensure all recommended security headers are consistently set.

6. **No Sensitive Files/Endpoints Found**
   - Positive outcome; no dev files, backups, or config files exposed.

---

## 4. Additional Recommendations

- Ensure all browser security indicators are green (“Secure”) and resolve inconsistencies.
- Regularly test with multiple browsers and SSL tools.
- Periodically review and update security headers.
- Consider regular automated scans with OWASP ZAP or similar tools.

---

## 5. Conclusion

The website demonstrates good security hygiene in several areas (no user enumeration, hidden files, or obvious XSS/open redirects).  
However, attention is needed for SSL/TLS consistency and brute-force protection on login forms.  
No critical vulnerabilities detected at this time.

**Attachments:**  
- Screenshots of browser security indicators  
- Sample curl/headers output (if required)  

---

**Prepared by:**  
kayon-assefa  
2025-06-25
