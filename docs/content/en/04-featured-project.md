---
section: featured-project
locale: en
order: 4
status: approved
updatedAt: 2026-09-19
title: Road Inspection IoT Platform
context: Freelance project for a road infrastructure agency.
period: 2025-12 – 2026-03
role: Full Stack Development and Platform Architecture
problem: Road inspections relied on manual routes without reliable connectivity, with detection data scattered across separate systems and no data isolation between clients.
solution: I designed and built a multitenant platform with an Android app that runs on-device computer vision for inspections without connectivity, a geospatial pipeline that consolidates results by state, and a web panel to review detections and export official reports.
outcomes:
  - Scaled the road geospatial catalog from 3 to 31 states, reaching 100% national coverage.
  - Enabled inspections without connectivity through on-device computer vision.
  - Ensured data isolation between clients with a multitenant microservices architecture and automated onboarding of new clients.
  - Stabilized capture during long field routes by diagnosing and fixing critical defects found in testing.
stack:
  - NestJS
  - Android (Kotlin)
  - TensorFlow Lite
  - YOLO
  - Python
  - Angular
media:
  - id: A04
    kind: cover
    src: images/featured-project/cover.svg
    alt: 'Synthetic composition representing a road-inspection platform: a road map and a detection dashboard.'
  - id: A05
    kind: screenshot-mobile
    src: images/featured-project/screenshot-mobile.webp
    alt: Synthetic screenshot of the inspection mobile app, inside a phone frame.
  - id: A06
    kind: screenshot-web
    src: images/featured-project/screenshot-web.webp
    alt: Synthetic screenshot of the web operations panel, inside a browser frame.
---
