# Task 3 – CRM & Google Ads Integration Design

## Q1. How would you architect this integration end-to-end?

When a patient submits the consultation form on the OrthoNow landing page, the form data is first sent to the backend server. The backend validates the submitted information and then sends the patient's details to HubSpot using the HubSpot Forms API.

If the phone number already exists, HubSpot updates the existing contact. Otherwise, it creates a new contact with the following details:

- Name
- Phone Number
- Clinic Preference
- Source = Google Ads – Consultation Landing Page
- Lead Status = New Enquiry

After HubSpot successfully responds, the backend sends a request to the Karix WhatsApp Business API to automatically send a confirmation message to the patient.

At the same time, the website pushes the `consultation_form_submitted` event to the dataLayer. Google Tag Manager captures this event and sends it to Google Analytics 4. The conversion is then imported into Google Ads so campaigns can optimize for consultation form submissions.

**Integration Flow**

Landing Page  
↓  
Backend Server  
↓  
HubSpot Forms API  
↓  
Karix WhatsApp Business API  
↓  
Google Tag Manager  
↓  
Google Analytics 4  
↓  
Google Ads

**Why HubSpot Forms API?**

I chose the HubSpot Forms API because it provides a direct, secure, and scalable integration without relying on third-party automation tools such as Zapier or Make. It offers better reliability, lower latency, and greater control over data handling.

---

## Q2. What is the biggest failure point and how would you build a fallback?

The biggest failure point is the HubSpot API. If HubSpot is temporarily unavailable, the patient's enquiry may fail to reach the CRM.

To prevent data loss, the backend should log failed requests, store them in a retry queue, and automatically retry after a short interval. Monitoring and alerting should notify the technical team if repeated failures occur so they can investigate immediately.

---

## Q3. The WhatsApp message must fire within 2 minutes. What could break this SLA and how would you monitor it?

The two-minute SLA could be affected by:

- HubSpot API downtime
- Karix API delays
- Network connectivity issues
- Backend server overload
- Invalid phone numbers

To monitor this SLA, the system should record timestamps for both the consultation form submission and the WhatsApp message delivery. Dashboards and automated alerts can identify any messages that exceed the two-minute target, allowing the team to take corrective action quickly.

---

## Recommended Technology Stack

- Frontend: HTML5, CSS3, JavaScript
- Backend: Node.js / Express
- CRM: HubSpot Forms API
- Messaging: Karix WhatsApp Business API
- Analytics: Google Tag Manager + Google Analytics 4
- Advertising: Google Ads Conversion Import