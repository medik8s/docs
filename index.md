---
layout: default
title: Home
nav_order: 1
---

<img src="images/medik8s-logo.png" alt="medik8s-logo" width="300" style="margin-left:auto; margin-right:auto; display:block"/>

# Medik8s - Kubernetes Node Remediation
{: .fs-8 }

Medik8s is a project consists of several kubernetes operators that provide automatic node remediation and high availability for singleton workloads
{: .fs-6 .fw-300 }


[Get Started Now](/GettingStarted){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[Watch a Demo](https://www.youtube.com/watch?v=8pSXAsioK8s){: .btn .btn-green .fs-5 .mb-4 .mb-md-0 .mr-2 }

Hardware is imperfect, and software contains bugs. When node level failures such
as kernel hangs or dead NICs occur, the work required from the cluster does not
decrease - workloads from affected nodes need to be restarted somewhere.

However some workloads, such as RWO volumes and StatefulSets, may require
at-most-one semantics.  Failures affecting these kind of workloads risk data
loss and/or corruption if nodes (and the workloads running on them) are assumed
to be dead whenever we stop hearing from them.  For this reason it is important
to know that the node has reached a safe state before initiating recovery of the
workload.

Unfortunately it is not always practical to require admin intervention in order
to confirm the node's true status. In order to automate the recovery of exclusive
workloads, Medik8s presents a collection of projects that can be installed on any
kubernetes-based cluster to automate:
* the [detection of failures](failure_detection),
* putting [nodes into a safe state](/remediation/remediation),
* allowing the scheduler to [recover affected workloads](recover_affected_workloads)
* attempting to [restore cluster capacity]()

## Community
Join [our google group](https://groups.google.com/g/medik8s) to get more info, participate in discussions and get notified
for new releases

<script type="text/javascript">
function openRemediationMenu(){
  document.getElementsByClassName("nav-list-item")[3].classList.add("active")
 }
document.body.addEventListener("load", openRemediationMenu(), false);
</script>

<style>
  /* Common styles for logos */
  .logo-link {
    display: block;
    text-align: center;
  }

  /* Style for the section title */
  .section-title {
    text-align: center;
    margin-top: 120px; /* Increased space above the title */
    margin-bottom: 60px; /* Increased space below the title */
  }

  /* Style for the container of logo pairs */
  .logos-container {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap; /* Allow logos to wrap to the next line */
    margin-bottom: 30px; /* Reduced space between blocks of logos */
  }

  .logos-container .logo-link {
    margin: 0; /* Reset margin to zero */
    flex: 1 1 auto; /* Distribute logos with equal space */
    max-width: calc(50% - 5px); /* Maximum width of each logo container with reduced gap */
  }

  /* Center-align the last single logo */
  .center-logo:last-child {
    justify-content: center;
  }
</style>

<div class="section-title">
  <h2>End Users</h2>
</div>

<div class="logos-container">
  <!-- First Pair of Logos -->
  <div class="logo-link">
    <a href="https://www.redhat.com/en/technologies/cloud-computing/openshift">
      <img src="../images/openshift-logo.png" alt="OpenShift" width="250" />
    </a>
  </div>
  <div class="logo-link">
    <a href="https://github.com/dana-team">
      <img src="../images/idf-logo.png" alt="IDF" width="150" />
    </a>
  </div>
</div>

<!-- Add more sections with logos here, create a new "logos-container" block for that -->
<div class="logos-container center-logo">
  <!-- Second Pair of Logos -->
  <div class="logo-link">
    <a href="https://www.nec.com/">
      <img src="../images/nec-logo.png" alt="NEC" width="150" />
    </a>
  </div>
  <!-- Add more logos here if needed -->
</div>
 