# ICD-10 Lookup Tool — User Manual for Healthcare Personnel

A free, AI-powered ICD-10 code lookup tool that lets you search **178,000+ ICD-10-CM diagnosis and ICD-10-PCS procedure codes** directly inside Claude AI. No login, no subscription, no forms to fill out.

**Server:** `https://icd10mcpserver.zapperedge.com/sse`  
**Data Source:** CMS ICD-10-CM and ICD-10-PCS (updated annually, FY2026)  
**Last Verified:** March 2026

---

## Table of Contents

- [What You Can Do](#what-you-can-do)
- [Step 1 — Set Up Claude (5 minutes)](#step-1--set-up-claude-5-minutes)
- [Step 2 — Set Up Other MCP Clients](#step-2--set-up-other-mcp-clients)
- [Step 3 — Verify It's Working](#step-3--verify-its-working)
- [How to Search — With Examples](#how-to-search--with-examples)
- [Test Cases for Medical Coders and RCM](#test-cases-for-medical-coders-and-rcm)
- [ICD-10-CM Chapter Reference](#icd-10-cm-chapter-reference)
- [Tips and Tricks](#tips-and-tricks)
- [FAQ](#faq)

---

## What You Can Do

| Task | Example |
|------|---------|
| Look up a specific code | *"Look up ICD-10 code J18.9"* |
| Validate a code before billing | *"Is E11.65 a valid billable code?"* |
| Search by condition or keyword | *"Find codes for pneumonia"* |
| Search for billable codes only | *"Find billable codes for type 2 diabetes"* |
| Browse an entire code category | *"Show me all codes in category E11"* |
| Search by chapter | *"What codes are in the respiratory chapter?"* |
| Find ICD-10-PCS procedure codes | *"Search for appendectomy procedure codes"* |
| Get ICD-9 to ICD-10 migration hints | *"I have ICD-9 code 250.00, what is the ICD-10 equivalent?"* |
| Check database status | *"Check the ICD-10 database status"* |

---

## Step 1 — Set Up Claude (5 minutes)

Claude is the easiest MCP client to get started with. You just need a free Claude account.

### 1.1 — Create a Claude Account

Go to **[claude.ai](https://claude.ai)** and sign up for a free account if you don't have one.

> **Note:** MCP connectors work on all Claude plans including the free tier.

---

### 1.2 — Add the ICD-10 MCP Server

1. Log in to **[claude.ai](https://claude.ai)**
2. Click your **profile icon** (top right corner)
3. Click **Settings**
4. In the left sidebar, click **Connectors**
5. Click the **"+ Add connector"** or **"Add MCP Server"** button
6. Fill in the form:

   | Field | Value |
   |-------|-------|
   | **Name** | `ICD-10` *(or any name you like)* |
   | **SSE URL** | `https://icd10mcpserver.zapperedge.com/sse` |

7. Click **Save** or **Connect**

---

### 1.3 — Start a New Conversation

> **Important:** You must start a **new conversation** after adding the connector. It will not appear in existing chats.

1. Click **New Chat** (or the pencil icon)
2. Type:
   ```
   Check the ICD-10 database status
   ```
3. Claude should respond with something like:
   > *"The ICD-10 database is ready with 178,215 codes (98,186 CM + 79,969 PCS), FY2026, last updated March 6, 2026..."*

**You are connected!** You can now search the full ICD-10 code set by just talking to Claude.

---

## Step 2 — Set Up Other MCP Clients

### Option B — Cursor (AI Code Editor)

If you use **[Cursor](https://cursor.sh)**:

1. Open Cursor
2. Press `Cmd+Shift+P` (Mac) or `Ctrl+Shift+P` (Windows)
3. Search for **"Open MCP Settings"** or go to **Settings → MCP**
4. Add the following to your `mcp.json` config file:

```json
{
  "mcpServers": {
    "icd10": {
      "url": "https://icd10mcpserver.zapperedge.com/sse",
      "transport": "sse"
    }
  }
}
```

5. Save the file and restart Cursor
6. Open the AI chat panel and type: `Check the ICD-10 database status`

---

### Option C — Windsurf (Codeium)

If you use **[Windsurf](https://codeium.com/windsurf)**:

1. Open Windsurf
2. Go to **Settings → AI → MCP Servers**
3. Click **Add Server**
4. Enter:

```json
{
  "name": "ICD-10",
  "url": "https://icd10mcpserver.zapperedge.com/sse",
  "transport": "sse"
}
```

5. Save and restart
6. Test by typing: `Check the ICD-10 database status`

---

### Option D — Continue.dev (VS Code Extension)

If you use **[Continue](https://continue.dev)** in VS Code:

1. Open VS Code
2. Go to the Continue extension settings
3. Edit your `~/.continue/config.json` and add:

```json
{
  "experimental": {
    "modelContextProtocolServers": [
      {
        "transport": {
          "type": "sse",
          "url": "https://icd10mcpserver.zapperedge.com/sse"
        }
      }
    ]
  }
}
```

4. Reload VS Code
5. Test in the Continue chat: `Check the ICD-10 database status`

---

### Option E — Any MCP-Compatible Client

For any other MCP client that supports SSE transport, use:

- **SSE Endpoint:** `https://icd10mcpserver.zapperedge.com/sse`
- **Transport:** `SSE`
- **Auth:** None required

---

## Step 3 — Verify It's Working

Once connected in any client, run this quick 3-step check:

**Check 1 — Database is live:**
```
Check the ICD-10 database status
```
Expected: 178,215 codes, FY2026, status "ready"

**Check 2 — Lookup works:**
```
Look up ICD-10 code J18.9
```
Expected: Returns "Pneumonia, unspecified organism" — billable, Diseases of the respiratory system

**Check 3 — Search works:**
```
Find billable codes for type 2 diabetes with kidney complications
```
Expected: Returns a list of billable E11.2x codes with descriptions

If all 3 pass — you are good to go.

---

## How to Search — With Examples

Just talk to Claude naturally. Here are the most useful patterns for medical coders and RCM staff:

### Look Up a Specific Code
```
Look up ICD-10 code E11.65
```
```
What is the description for code J18.9?
```
```
Look up PCS code 0BH17EZ
```

---

### Validate a Code for Billing
```
Is E11.65 a valid billable code?
```
```
Validate ICD-10 code Z99.999
```
```
Is code J18 billable?
```
> Useful for catching non-billable header codes before submitting claims. Header codes (e.g. E11, J18) are not billable — only their fully specified child codes are accepted on claims.

---

### Search by Condition or Keyword
```
Find codes for pneumonia
```
```
Search for fracture of femur codes
```
```
What are the ICD-10 codes for sepsis?
```
```
Find codes related to heart failure
```

---

### Search for Billable Codes Only
```
Find billable codes for hypertension
```
```
Search for billable codes for major depressive disorder
```
> Adding "billable only" filters out header/category codes and returns only codes acceptable on claims.

---

### Browse an Entire Code Category
```
Show me all codes in category E11
```
```
What codes are under category I50?
```
```
List all codes in category J18
```
> Returns every code within a 3-character category — useful for reviewing specificity options before selecting a final code.

---

### Search by Chapter
```
What codes are in the circulatory system chapter?
```
```
Find codes in the mental and behavioral disorders chapter
```
```
What chapter does code F32.1 belong to?
```

---

### Search ICD-10-PCS Procedure Codes
```
Search for appendectomy procedure codes in ICD-10-PCS
```
```
Find PCS codes for knee replacement
```
```
Look up PCS code 0BH17EZ
```

---

### ICD-9 to ICD-10 Migration Hints
```
I have ICD-9 code 250.00 — what ICD-10 codes should I consider?
```
```
What ICD-10 code maps to ICD-9 410.9?
```
> Note: This tool provides keyword-based suggestions as a starting point. For official claim submission, always confirm using CMS GEMs (General Equivalence Mappings) at cms.gov.

---

### Pagination — Get More Results
```
Find codes for diabetes mellitus, show me the first 10
```
Then:
```
Show me the next 10
```

---

## Test Cases for Medical Coders and RCM

Use these to verify the tool works correctly for coding and billing scenarios.

---

### Test 1 — Validate a Known Billable Code
**Prompt:**
```
Validate ICD-10 code E11.65
```
**Expected result:** Valid — billable — "Type 2 diabetes mellitus with hyperglycemia"

---

### Test 2 — Validate a Non-Billable Header Code
**Prompt:**
```
Validate ICD-10 code J18
```
**Expected result:** Code exists but is NOT billable — it is a category header. Use a more specific code such as J18.9.

---

### Test 3 — Validate a Code That Does Not Exist
**Prompt:**
```
Validate ICD-10 code Z99.999
```
**Expected result:** Invalid — format is correct but code is not found in the ICD-10 database.

---

### Test 4 — Look Up a Specific Diagnosis Code
**Prompt:**
```
Look up ICD-10 code J18.9
```
**Expected result:**
- Code: J18.9
- Description: Pneumonia, unspecified organism
- Type: ICD-10-CM (diagnosis)
- Billable: Yes
- Chapter: Diseases of the respiratory system
- Fiscal Year: FY2026

---

### Test 5 — Look Up a PCS Procedure Code
**Prompt:**
```
Look up ICD-10-PCS code 0BH17EZ
```
**Expected result:** Returns full description of the procedure code, billable status, and fiscal year.

---

### Test 6 — Search by Condition Keyword
**Prompt:**
```
Find ICD-10 codes for pneumonia
```
**Expected result:** List of pneumonia codes including J18.0, J18.1, J18.9 and related codes with descriptions and billable status.

---

### Test 7 — Search for Billable Codes Only
**Prompt:**
```
Find billable codes for type 2 diabetes with kidney complications
```
**Expected result:** Only billable codes from the E11.2x category — such as E11.21, E11.22, E11.29 — are returned. Non-billable header codes like E11.2 are excluded.

---

### Test 8 — Browse a Full Code Category
**Prompt:**
```
Show me all codes in category E11
```
**Expected result:** Complete listing of all 117 codes under Type 2 diabetes mellitus (E11), including both header codes and 87 billable codes, with descriptions.

---

### Test 9 — Identify Chapter for a Code
**Prompt:**
```
What chapter does code F32.1 belong to?
```
**Expected result:** Chapter 5 — Mental, Behavioral and Neurodevelopmental disorders (F01–F99)

---

### Test 10 — Search PCS Procedure Codes
**Prompt:**
```
Search for appendectomy ICD-10-PCS codes
```
**Expected result:** List of PCS codes related to appendix removal procedures with full descriptions.

---

### Test 11 — ICD-9 Migration Hint
**Prompt:**
```
I have ICD-9 code 250.00 — what ICD-10 codes should I look at?
```
**Expected result:** Suggested ICD-10-CM codes in the E11 diabetes mellitus category, along with a reminder to confirm with CMS GEMs for official crosswalk.

---

### Test 12 — Pagination Test
**Prompt:**
```
Find codes for diabetes mellitus, show 5 results
```
Then:
```
Show the next 5
```
**Expected result:** Two distinct pages of results with no duplicate codes.

---

### Quick Pass Checklist

| # | Test | Pass if... |
|---|------|------------|
| 1 | Validate good billable code | Returns "valid" and "billable" |
| 2 | Validate header code | Returns "exists but not billable" |
| 3 | Validate non-existent code | Returns "not found" |
| 4 | Lookup CM diagnosis code | Returns full description and chapter |
| 5 | Lookup PCS procedure code | Returns procedure description |
| 6 | Keyword search | Returns list of matching codes |
| 7 | Billable-only search | Returns no header codes |
| 8 | Category browse | Returns all codes in category |
| 9 | Chapter lookup | Returns correct chapter name |
| 10 | PCS search | Returns procedure codes |
| 11 | ICD-9 migration hint | Returns ICD-10 suggestions |
| 12 | Pagination | Page 2 has different results than page 1 |

All 12 passing = Tool is fully working for medical coding and RCM use.

---

## ICD-10-CM Chapter Reference

Use these chapter names when searching by clinical area:

| Chapter | Code Range | Clinical Area |
|---------|------------|---------------|
| 1 | A00–B99 | Infectious and parasitic diseases |
| 2 | C00–D49 | Neoplasms |
| 3 | D50–D89 | Blood and blood-forming organ diseases |
| 4 | E00–E89 | Endocrine, nutritional and metabolic diseases |
| 5 | F01–F99 | Mental, behavioral and neurodevelopmental disorders |
| 6 | G00–G99 | Diseases of the nervous system |
| 7 | H00–H59 | Diseases of the eye and adnexa |
| 8 | H60–H95 | Diseases of the ear and mastoid process |
| 9 | I00–I99 | Diseases of the circulatory system |
| 10 | J00–J99 | Diseases of the respiratory system |
| 11 | K00–K95 | Diseases of the digestive system |
| 12 | L00–L99 | Diseases of the skin and subcutaneous tissue |
| 13 | M00–M99 | Diseases of the musculoskeletal system and connective tissue |
| 14 | N00–N99 | Diseases of the genitourinary system |
| 15 | O00–O9A | Pregnancy, childbirth and the puerperium |
| 16 | P00–P96 | Certain conditions originating in the perinatal period |
| 17 | Q00–Q99 | Congenital malformations and chromosomal abnormalities |
| 18 | R00–R99 | Symptoms, signs and abnormal clinical findings |
| 19 | S00–T88 | Injury, poisoning and external causes |
| 20 | V00–Y99 | External causes of morbidity |
| 21 | Z00–Z99 | Factors influencing health status and contact with health services |
| 22 | U00–U85 | Codes for special purposes (COVID-19 and emerging conditions) |

---

## FAQ

**Q: What code sets are included?**
A: Both ICD-10-CM (diagnosis codes, 98,186 codes) and ICD-10-PCS (inpatient procedure codes, 79,969 codes) are included. The current fiscal year is FY2026.

**Q: How current is the data?**
A: The database is updated annually to match CMS ICD-10 fiscal year releases. You can ask *"Check the ICD-10 database status"* to see the exact version and last update date. The current database reflects FY2026 codes effective October 1, 2025.

**Q: Is this data official?**
A: Yes. Data comes directly from CMS ICD-10-CM and ICD-10-PCS code files — the same source used by payers, clearinghouses, and coding software.

**Q: Is it free to use?**
A: Yes, completely free. Claude has a free tier at claude.ai.

**Q: What is the difference between a billable and a non-billable code?**
A: Billable codes (also called "valid for submission" or "leaf codes") are the most specific level of a code and can be used on claims. Non-billable codes are header or category codes that group related conditions but are not accepted by payers. For example, E11 (Type 2 diabetes mellitus) is a non-billable header; E11.9 (Type 2 diabetes mellitus without complications) is billable.

**Q: Can I use this for ICD-10-PCS inpatient procedure coding?**
A: Yes. Specify "PCS" in your query to search procedure codes. For example: *"Find PCS codes for laparoscopic cholecystectomy"*

**Q: Does this replace official coding software or encoder tools?**
A: This tool is designed for quick lookups, validation, and research during the coding and billing workflow. For official claim submission, always confirm codes in your encoder or against the official CMS code files. This tool does not replace AHA Coding Clinic guidance or official payer policies.

**Q: Can it help with ICD-9 to ICD-10 crosswalks?**
A: The tool provides keyword-based suggestions to help identify candidate ICD-10 codes when given an ICD-9 code or condition description. For official mappings, use the CMS General Equivalence Mappings (GEMs) at cms.gov/medicare/coding-billing/icd-10-codes/icd-10-cm-icd-10-pcs-gems.

**Q: What if I get no results?**
A: Try broadening your search — use a shorter keyword or remove modifiers. For example, instead of "community-acquired bacterial pneumonia" try "pneumonia." Also confirm you are spelling the condition correctly.

**Q: My MCP client is not listed. Will it work?**
A: Any MCP client that supports SSE transport should work. Use the SSE URL: `https://icd10mcpserver.zapperedge.com/sse`

---

## Support

If the server is down or returning errors:
- Ask Claude: *"Check the ICD-10 database status"*

For issues or feature requests: feature-request@zapperedge.com

---

*Data provided by the Centers for Medicare and Medicaid Services (CMS) — US Department of Health and Human Services. ICD-10-CM and ICD-10-PCS codes updated annually each fiscal year.*
