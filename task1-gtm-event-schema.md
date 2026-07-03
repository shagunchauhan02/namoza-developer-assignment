# Task 1 – GTM Event Schema

## GTM Event Tracking Schema

| Event Name | Trigger Type | Key Parameters | GA4 Report / Audience |
|------------|--------------|----------------|------------------------|
| booking_step_complete | Custom Event (dataLayer) | step_number, step_name, clinic_location, specialty | Funnel Exploration |
| booking_confirmed | Form Submission Success | booking_id, clinic_location, specialty | Conversions |
| call_now_click | Click Trigger | page_location, clinic_location, button_text | Engagement Report |
| whatsapp_click | Click Trigger | page_location, destination_url, button_location | Engagement Report |
| patient_guide_download | Form Submit + File Download | guide_name, phone_number, page_location | Lead Generation |
| clinic_page_view | Page View | clinic_location, page_title, page_url | Pages & Screens |
| blog_scroll_50 | Scroll Trigger (50%) | article_title, scroll_percentage, page_url | Engagement |
| blog_scroll_90 | Scroll Trigger (90%) | article_title, scroll_percentage, page_url | Engaged Audience |

---

# Booking Form Funnel Tracking

The booking form contains three steps. Google Tag Manager cannot automatically understand multi-step form progress. Therefore, the front-end developer must push custom `dataLayer` events whenever a user completes a step.

Each completed step sends a custom event to the `dataLayer`. GTM listens for these events and forwards them to Google Analytics 4.

This enables Funnel Exploration in GA4 to measure user drop-off between each booking step.

---

## Step 1 JSON

```json
{
  "event": "booking_step_complete",
  "step_number": 1,
  "step_name": "location_specialty_selected",
  "clinic_location": "{{clinic name}}",
  "specialty": "{{specialty selected}}"
}
```

---

## Step 2 JSON

```json
{
  "event": "booking_step_complete",
  "step_number": 2,
  "step_name": "patient_details_entered",
  "patient_name": "{{name}}",
  "phone_number": "{{phone}}",
  "preferred_date": "{{preferred date}}"
}
```

---

## Step 3 JSON

```json
{
  "event": "booking_step_complete",
  "step_number": 3,
  "step_name": "booking_confirmed",
  "booking_status": "confirmed",
  "clinic_location": "{{clinic name}}"
}
```

---

# Funnel Analysis in GA4

Create a Funnel Exploration with the following steps:

1. Step 1 – Location & Specialty Selected
2. Step 2 – Patient Details Entered
3. Step 3 – Booking Confirmed

This allows marketing teams to identify where users abandon the booking process and optimize the highest drop-off stage.

---

# Google Ads Conversion

**Recommended Conversion:**

`booking_confirmed`

### Why?

Confirmed consultation bookings directly represent business value. Optimizing Google Ads for confirmed bookings improves lead quality and enables Smart Bidding to maximize actual appointments instead of intermediate actions like button clicks or page views.