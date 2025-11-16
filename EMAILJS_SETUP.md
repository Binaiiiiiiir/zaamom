# EmailJS Setup Guide for Store Forms

## Step-by-Step Instructions

### Step 1: Get Your EmailJS Public Key
1. Go to https://www.emailjs.com/
2. Log in to your account
3. Go to **Account** → **General**
4. Copy your **Public Key** (it looks like: `abc123xyz456`)
5. Open `store.html`
6. Find line 17: `emailjs.init("YOUR_PUBLIC_KEY");`
7. Replace `YOUR_PUBLIC_KEY` with your actual Public Key

### Step 2: Create Email Template in EmailJS
1. Go to **Email Templates** in your EmailJS dashboard
2. Click **Create New Template**
3. Name it: `Store Order Form`
4. Copy the template content below into the template editor

### Step 3: Get Your Template ID
1. After creating the template, you'll see a **Template ID** (it looks like: `template_abc123`)
2. Open `store.html`
3. Find line 375: `emailjs.send("service_3lv5cqe", "YOUR_TEMPLATE_ID", templateParams)`
4. Replace `YOUR_TEMPLATE_ID` with your actual Template ID

### Step 4: Configure Email Service
1. Make sure your service ID `service_3lv5cqe` is connected to your email account
2. In EmailJS dashboard, go to **Email Services**
3. Verify that `service_3lv5cqe` is active and connected

---

## EmailJS Template Content

### Option 1: Advanced Template (with conditional blocks)

If your EmailJS plan supports Handlebars conditionals, use this:

```
Subject: New Store Order - {{category}}

Hello,

You have received a new order from your store:

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ORDER DETAILS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Category: {{category}}

Customer Information:
• Name: {{customer_name}}
• Email: {{customer_email}}
• Phone: {{customer_phone}}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ORDER SPECIFICATIONS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

{{#if board_type}}
Board Type: {{board_type}}
Board Size: {{board_size}}
{{/if}}

{{#if outfit_type}}
Outfit Type: {{outfit_type}}
Outfit Size: {{outfit_size}}
{{/if}}

{{#if canvas_size}}
Canvas Size: {{canvas_size}}
{{/if}}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
MESSAGE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

{{message}}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

This email was sent from your Zaamom Store website.

Best regards,
Zaamom Store
```

### Option 2: Simple Template (works on all plans)

If you don't have Handlebars support, use this simpler version:

```
Subject: New Store Order - {{category}}

Hello,

You have received a new order from your store:

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ORDER DETAILS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Category: {{category}}

Customer Information:
• Name: {{customer_name}}
• Email: {{customer_email}}
• Phone: {{customer_phone}}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ORDER SPECIFICATIONS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Board Type: {{board_type}}
Board Size: {{board_size}}
Outfit Type: {{outfit_type}}
Outfit Size: {{outfit_size}}
Canvas Size: {{canvas_size}}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
MESSAGE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

{{message}}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

This email was sent from your Zaamom Store website.

Best regards,
Zaamom Store
```

**Note:** With Option 2, empty fields will show as blank. Only the relevant fields will have values based on the category selected.

---

## Template Variables Reference

The following variables are available in your template:

| Variable | Description | Example |
|----------|-------------|---------|
| `{{category}}` | Order category | "Boards", "Outfit & Accessories", or "Canvas" |
| `{{customer_name}}` | Customer's name | "John Doe" |
| `{{customer_email}}` | Customer's email | "john@example.com" |
| `{{customer_phone}}` | Customer's phone | "+1234567890" |
| `{{board_type}}` | Board type (if Boards category) | "surf", "body board", or "skateboard" |
| `{{board_size}}` | Board size (if Boards category) | "6'0\"", "38\"", etc. |
| `{{outfit_type}}` | Outfit type (if Outfit category) | "tshirt", "hoodies", "bag", or "shoes" |
| `{{outfit_size}}` | Outfit size (if Outfit category) | "M", "L", "42", etc. |
| `{{canvas_size}}` | Canvas size (if Canvas category) | "50x70 cm", "60x80 cm", etc. |
| `{{message}}` | Customer's message | Any text from the textarea |

---

## Testing

1. After completing all steps, test the form:
   - Click on any polaroid (Boards, Outfit & Accessories, or Canvas)
   - Fill out the form
   - Submit
   - Check your email inbox for the order

2. If you don't receive emails:
   - Check EmailJS dashboard for error logs
   - Verify your Public Key and Template ID are correct
   - Make sure your email service is properly connected

---

## Notes

- The template uses conditional blocks (`{{#if}}`) to show only relevant fields
- Empty fields will show as blank (not "undefined")
- All three order types use the same template but show different fields based on category

