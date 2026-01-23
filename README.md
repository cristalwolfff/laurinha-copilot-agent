# 🤖 Laurinha: AI Marketing Compliance & Content Assistant

**Status:** 🚀 Deployed & Homologated (Microsoft Teams Integration)  
**Role:** AI Engineer / Power Platform Developer  
**Tech Stack:** Microsoft Copilot Studio, Power Fx, Power Automate, Microsoft Teams, Generative AI.

---

## 📖 Overview

**Laurinha** is a custom AI agent developed to solve a critical operational bottleneck in the CRM department. Before this project, the creation of communication schedules (SMS, Push, Email, WhatsApp) was a manual, week-long process prone to human error.

This project was the company's first fully operational agent built on **Microsoft Copilot Studio**, integrated natively into **Microsoft Teams**. It bridges the gap between creative freedom and strict technical compliance, empowering non-technical staff to generate valid marketing assets instantly.

---

## 🛑 The Challenge (Business Pain Points)

* **Operational Bottleneck:** Planning campaigns for multiple channels took weeks due to the high volume of repetitive copywriting tasks.
* **High Cognitive Load:** Analysts had to manually memorize and check technical rules for every message (e.g., *Is this SMS under 160 chars?*, *Does this WhatsApp message have bold formatting?*, *Are there forbidden special characters?*).
* **Compliance Risks:** Frequent human errors led to failed message deliveries or non-compliant formatting (e.g., using non-GSM-7 characters in SMS).

---

## 💡 The Solution

I architected a solution that uses **Generative AI** for creativity but constrains it with **Hard-Coded Logic (Power Fx)** for compliance. The bot acts as a "guardrail" system—it drafts the content and immediately validates it against platform rules before the user even sees it.

### Key Features
1.  **Generative AI Content Creation:** Generates diverse copy variations for SMS, Push, and Email based on raw offer data.
2.  **Real-time Validation (Power Fx):** Prevents the AI from "hallucinating" invalid formats. The bot mathematically verifies character counts and encoding sets.
3.  **Microsoft Teams Integration:** Zero-friction adoption; the bot lives where the team communicates.

---

## ⚙️ Engineering & Architecture

### 1. Hard-Coding Logic with Power Fx
Unlike simple GPT wrappers, **Laurinha** uses deterministic logic to police the AI's output. Below is a conceptual example of the validation logic used to ensure SMS compliance (GSM-7 standard and length):

```powerfx
// ---------------------------------------------------------
// SMS Validation Logic (Conceptual Snippet)
// Ensures content is < 160 chars and contains no invalid symbols
// ---------------------------------------------------------

If(
    Len(Topic.GeneratedSMS) > 160,
    // Error Path: Retry generation with stricter prompt
    Set(VarValidationStatus, "Error: Length exceeded");
    RedirectTo(Step_RegenerateShortCopy),

    // Else: Check for non-GSM-7 characters (Simplified Regex check)
    IsMatch(Topic.GeneratedSMS, "^[A-Za-z0-9@£$¥èéùìòÇ\n\r\s]*$"),
    
    // Success Path: Output valid content
    Set(VarValidationStatus, "Valid");
    Return(Topic.GeneratedSMS),

    // Error Path: Found invalid characters
    Set(VarValidationStatus, "Error: Invalid Characters Detected");
    RedirectTo(Step_CleanSpecialChars)
)

```

### 2. Workflow Orchestration

* **Trigger:** User invokes bot in Teams via `@Laurinha`.
* **Input:** User provides offer details (e.g., "50% off Sneakers").
* **Process:**
1. Copilot generates 5 variations using GenAI.
2. Power Fx loops through variations to validate constraints.
3. Invalid options are discarded or auto-corrected.


* **Output:** Returns a structured Adaptive Card with "Ready-to-Send" copy.

---

## 🏆 Impact & Results

* **SLA Reduction:** Campaign planning time reduced from **weeks to minutes**.
* **Strategic Focus:** Shifted team focus from "formatting checks" to "marketing strategy."
* **100% Compliance:** Eliminated technical errors in outgoing SMS and Push notifications by standardizing the output format.

---

## 📬 Contact

If you are looking for similar solutions involving **Copilot Studio**, **Power Automate**, or **AI Agents**, feel free to reach out.

**[Upwork](https://www.upwork.com/freelancers/~01e86eb238637e8561?mp_source=share)**

```

```
