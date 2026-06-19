# Introduction to EDR (Endpoint Detection & Response)

## Overview

EDR is a security solution that monitors endpoint activity, detects suspicious behaviour, and enables analysts to investigate and respond to threats from a central console.

Unlike traditional antivirus solutions that primarily rely on signatures, EDR focuses on visibility, behavioural detection, and response capabilities.

## Core EDR Components

### Endpoint Agent (Sensor)

Installed on endpoints to:

* Collect telemetry
* Monitor activity
* Detect suspicious behaviour
* Send data to the EDR platform

### EDR Console

Used to:

* Correlate endpoint data
* Generate detections
* Investigate alerts
* Perform response actions

## Key Telemetry Collected

* Process creation and termination
* Parent-child process relationships
* Command-line activity
* Network connections
* File and folder modifications
* Registry changes

This telemetry helps analysts reconstruct attack timelines and identify malicious activity.

## Detection Methods

* Signature-based detection
* Behavioural analysis
* Anomaly detection
* Threat Intelligence (IOC matching)
* MITRE ATT&CK mapping
* Machine learning

These techniques allow EDR solutions to detect advanced threats that may evade traditional antivirus products.

## Response Capabilities

Common response actions include:

* Host isolation
* Process termination
* File quarantine
* Remote endpoint access
* Forensic artefact collection

## Key Takeaways

* EDR provides deep visibility into endpoint activity.
* Endpoint agents collect telemetry and send it to a central console.
* Detection relies heavily on behaviour analysis, not just signatures.
* Analysts can investigate and respond to threats directly from the EDR platform.
* EDR is a core tool used by SOC teams for endpoint monitoring, investigation, and incident response.
