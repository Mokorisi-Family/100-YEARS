# Mokorosi 100th Birthday — Guestbook + WhatsApp setup

The website now has a live guestbook UI. It stores messages in Supabase and can notify the family via WhatsApp Cloud API.

## 1. Create the Supabase database
1. Create a Supabase project.
2. Open SQL Editor.
3. Run supabase/schema.sql.
4. Ensure the birthday_messages table is exposed through the Data API.
5. Copy the project URL and publishable/anon key into js/supabase-config.js.

## 2. Deploy WhatsApp notification
Deploy supabase/functions/send-whatsapp/index.ts as the send-whatsapp Edge Function.
Set these server-side secrets: WHATSAPP_ACCESS_TOKEN, WHATSAPP_PHONE_NUMBER_ID, WHATSAPP_NOTIFICATION_NUMBER, META_GRAPH_VERSION.
Never put the access token in GitHub or browser code.

## 3. Public flow
Visitor → submits message → message is immediately stored → message appears on the website → WhatsApp notification can be sent to the family number.
The page also offers an optional WhatsApp share after posting. No manual approval is required.

## 4. WhatsApp
The server-side Cloud API function keeps the access token private. Meta's WhatsApp business messaging rules determine when business-initiated messages require approved templates or opt-in.