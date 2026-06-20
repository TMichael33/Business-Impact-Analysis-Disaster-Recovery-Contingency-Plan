# Project 7: Business Impact Analysis & Disaster Recovery Contingency Plan

## Executive Summary
A mature compliance posture recognizes that security controls must align directly with operational survival and asset protection. This project demonstrates the execution of an enterprise-wide **Business Impact Analysis (BIA)** and the development of a **Disaster Recovery (DR) Contingency Plan** mapped to the **NIST SP 800-34 Rev. 1** framework for a mock FinTech enterprise ("Nexus FinTech").

The objective of this project was to systematically evaluate corporate business units, calculate financial and operational impacts during systemic outages, define precise recovery objectives, and outline an actionable recovery roadmap for high-availability IT assets.

---

## Operational Definitions & BIA Core Metrics
To establish a rigorous, numbers-driven approach to downtime, the BIA evaluates enterprise systems using four core industry metrics:
*   **Maximum Tolerable Downtime (MTD):** The total time executive leadership can tolerate the complete disruption of a business function before irreversible financial or existential ruin occurs.
*   **Recovery Time Objective (RTO):** The target time allocated for IT personnel to fully restore a system or application back to operational status following an outage. **(Rule: RTO must always be less than or equal to MTD).**
*   **Recovery Point Objective (RPO):** The maximum acceptable age of data that can be permanently lost during a major disruption (e.g., if backups run every 4 hours, the maximum RPO exposure is 4 hours of transaction data).
*   **Work Recovery Time (WRT):** The time required to verify data integrity, run consistency checks, and catch up on manual backlogs once a system is technically running, before the business unit goes live.

---

## Enterprise Business Impact Analysis (BIA) Matrix

Below is the formal asset prioritization matrix mapped out during the business risk evaluation phase.

<table width="100%">
  <thead>
    <tr>
      <th width="15%">System / Asset Name</th>
      <th width="15%">Impact Category</th>
      <th width="25%">Downstream Operational Impact</th>
      <th width="10%">MTD</th>
      <th width="10%">Target RTO</th>
      <th width="10%">Target RPO</th>
      <th width="15%">Estimated Downtime Cost</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>Core Payment Ledger API</b></td>
      <td> <b>Tier 1:<br>Mission-Critical</b></td>
      <td>Halts all client payment processing, transaction authorizations, and point-of-sale settlements globally. Immediate regulatory breach.</td>
      <td>2 Hours</td>
      <td><b>&le; 1 Hour</b></td>
      <td><b>&le; 15 Mins</b><br>(Near Real-Time)</td>
      <td><span style="color:red;"><b>$75,000 / Hour</b></span></td>
    </tr>
    <tr>
      <td><b>Customer ERP & CRM Databases</b></td>
      <td> <b>Tier 2:<br>High Priority</b></td>
      <td>Blocks customer support operations, limits account verification pipelines, and creates manual data log jams for account reps.</td>
      <td>12 Hours</td>
      <td><b>&le; 4 Hours</b></td>
      <td><b>&le; 1 Hour</b></td>
      <td><span style="color:orange;"><b>$12,000 / Hour</b></span></td>
    </tr>
    <tr>
      <td><b>Corporate HR & Payroll Platform</b></td>
      <td> <b>Tier 3:<br>Medium / Low</b></td>
      <td>Delays internal hiring operations, expense accounting processing, and non-essential administrative reporting. No external client impact.</td>
      <td>72 Hours</td>
      <td><b>&le; 24 Hours</b></td>
      <td><b>&le; 24 Hours</b><br>(Daily Backup)</td>
      <td><span style="color:green;"><b>$1,500 / Hour</b></span></td>
    </tr>
  </tbody>
</table>

---

## Disaster Recovery Contingency Strategy (NIST 800-34)

To guarantee that our **Tier 1 (Core Payment Ledger API)** maintains its strict 1-hour RTO and 15-minute RPO, the following disaster recovery architecture has been implemented:

### 1. High-Availability Cloud Failover
The payment API operates on a multi-region, cloud-native cluster architecture. Database transactions are continuously mirrored across live-active availability zones. If the primary cloud region undergoes a catastrophic regional failure, traffic automatically reroutes to the secondary node via automated health-check routing tables, maintaining a hot-standby state.

### 2. Immutable Transaction Logs
Database write-ahead logs are backed up every 15 minutes to air-gapped, immutable cloud storage buckets with object-locking enabled. This ensures that even during a widespread ransomware attack, financial data can be cleanly reconstructed up to the point of disruption within our defined RPO boundary.

### 3. Verification & Work Recovery Playbook
Once technical failover is confirmed by infrastructure teams, data engineers must execute an automated transaction reconciliation script. This checks for any orphaned API calls or out-of-sync balances against secondary clearinghouses before the system is formally cleared to accept public customer traffic.

---

## Key Insights & Business Alignment
1. **GRC Bridges Technology and Revenue:** A basic IT checklist looks at infrastructure as a list of servers. A business-aligned GRC analyst looks at infrastructure through the lens of revenue risk, compliance violations, and contractual commitments, enabling leadership to make data-driven budget decisions.
2. **Data-Driven Control Allocation:** Security budgets are finite. Running a comprehensive BIA ensures an organization doesn't overspend on protecting low-impact systems while leaving the true economic engines of the enterprise vulnerable. It changes security from an ambiguous expense to an architecture of risk optimization.
3. **Contingency Testing Stops Chaos:** An undocumented, untested DR plan is non-existent when a real emergency strikes. Aligning business units with formal metrics (RTO/RPO) ensures that when an outage occurs, technical teams have exact benchmarks and step-by-step playbooks to follow, protecting enterprise equity and maintaining continuity under extreme duress.
