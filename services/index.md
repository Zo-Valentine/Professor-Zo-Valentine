---
layout: default
title: Services
---
# Services

## Service Architecture
Caphè services are organized around bottlenecks rather than software categories.

### Diagnose
Find the information, data, workflow, or decision bottleneck.

### Build
Design and implement the smallest useful system that resolves it.

### Operate
Monitor, measure, improve, and expand the system.

## Service Families

**Data:** Data Audit · Data Integration · Data Pipeline · Data Modeling · Data Warehouse · Data API · Data Enrichment

**Workflow:** Workflow Audit · Process Mapping · Workflow Redesign · Automation · Appointment Systems · Follow-Up Systems

**Intelligence:** Job Intelligence · Recruiting Intelligence · Property Intelligence · Threat Intelligence · Operational Intelligence

**Architecture:** Business Systems Architecture · Data Architecture · Integration Architecture · Human-in-the-Loop Architecture · Operating Model

**Learning:** LMS Architecture · Curriculum Systems · Corporate Training · Information Systems Education

## Property & Real Estate Operations

The same Diagnose → Build → Operate architecture applied to property operators, disposition/
REO teams, and small-to-growing property-management companies — see the
[Property Operations Intelligence Platform]({{ '/systems/property-operations-intelligence-platform/' | relative_url }})
system page. The entry ladder is scoped to operator size rather than a single fixed offer:

**Diagnose** → Property Operations Snapshot (a single property/workflow diagnostic)
**Build** → Workflow Audit → Operations Sprint (implement one specific improvement)
**Operate** → Automation Sprint → ongoing Intelligence/Operations Layer (ongoing monitoring, reporting, optimization)

Initial focus is owner-operators and small-to-growing property-management companies rather
than institutional multifamily, which is already well served by enterprise PMS/BI vendors.

## Entry Path
`PROBLEM → DIAGNOSE → ARCHITECT → BUILD → MEASURE → OPERATE`

### Introducing CurbIQ — the pilot service

CurbIQ is the first live entry point into this architecture: a physical property sign becomes
a measurable digital interaction, a structured request, a human response, and audit evidence —
built for real estate disposition and leasing teams. It's the pilot service this path is
currently proven against; see the
[Property Operations Intelligence Platform]({{ '/systems/property-operations-intelligence-platform/' | relative_url }})
system page for the real, running evidence.

<div class="shell">
<form class="lead-form" id="start-project-form">
<h3>Start a project</h3>
<label for="lf-name">Name</label>
<input type="text" id="lf-name" name="name" required>
<label for="lf-email">Email</label>
<input type="email" id="lf-email" name="email" required>
<label for="lf-org">Organization (optional)</label>
<input type="text" id="lf-org" name="organization">
<label for="lf-interest">What are you interested in?</label>
<select id="lf-interest" name="service_interest">
<option value="curbiq_pilot">CurbIQ Pilot</option>
<option value="data_engineering">Data Engineering</option>
<option value="workflow_automation">Workflow / Automation</option>
<option value="intelligence_reporting">Intelligence / Reporting</option>
<option value="other">Other</option>
</select>
<label for="lf-message">What problem are you trying to solve?</label>
<textarea id="lf-message" name="message" required></textarea>
<button type="submit" class="button primary">Send</button>
<p class="form-status" id="lf-status"></p>
</form>
<div class="lead-form-divider"><span>or</span></div>
<a class="button calendly-cta" href="https://calendly.com/zovalentinen/techincal-risk-consulting-career-learning-systems" target="_blank" rel="noopener">Book time directly →</a>
</div>

<script>
(function () {
  var API_BASE = "http://localhost:8010"; // local dev only — replace with the deployed
                                           // lead-capture-api's public URL before this site
                                           // goes live on GitHub Pages.
  var form = document.getElementById("start-project-form");
  var status = document.getElementById("lf-status");
  form.addEventListener("submit", function (e) {
    e.preventDefault();
    status.textContent = "Sending...";
    status.className = "form-status";
    fetch(API_BASE + "/v1/leads", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        name: document.getElementById("lf-name").value,
        email: document.getElementById("lf-email").value,
        organization: document.getElementById("lf-org").value || null,
        service_interest: document.getElementById("lf-interest").value,
        message: document.getElementById("lf-message").value,
        source_page: window.location.pathname,
      }),
    })
      .then(function (res) {
        if (!res.ok) throw new Error("request failed");
        return res.json();
      })
      .then(function () {
        status.textContent = "Thanks — this has been received, a human will follow up.";
        status.className = "form-status ok";
        form.reset();
      })
      .catch(function () {
        status.textContent = "Something went wrong sending this. Please try again.";
        status.className = "form-status err";
      });
  });
})();
</script>
