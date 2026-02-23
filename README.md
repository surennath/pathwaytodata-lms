# pathwaytodata-lms
pathwaytodata site hosting

# 🚀 PathwayToData — Deployment Guide
## Google Sites + GitHub Pages + Custom Domain (www.pathwaytodata.com)

---

## 📋 OVERVIEW

Google Sites does NOT host raw HTML files directly — it uses an iframe embed system.  
**The correct architecture:**

```
GitHub Pages (hosts your HTML file)
        ↕ iframe embed
Google Sites (your visual website)
        ↕ Custom Domain
www.pathwaytodata.com
```

---

## PHASE 1 — Host Your HTML on GitHub Pages (Free)

### Step 1: Create a GitHub Account
1. Go to https://github.com → Sign Up (free)
2. Use your email, create a username like `pathwaytodata`

### Step 2: Create a Repository
1. Click the **+** icon (top-right) → **New repository**
2. Repository name: `pathwaytodata-lms`
3. Set to **Public**
4. Check ✅ "Add a README file"
5. Click **Create repository**

### Step 3: Upload Your HTML File
1. In your new repo, click **Add file** → **Upload files**
2. Upload the `pathwaytodata-lms.html` file
3. **RENAME IT** to `index.html` (this is critical!)
4. Scroll down → Click **Commit changes**

### Step 4: Enable GitHub Pages
1. In your repo, click **Settings** (top menu)
2. Scroll to **Pages** (left sidebar under "Code and automation")
3. Under "Source" → select **Deploy from a branch**
4. Branch: **main** | Folder: **/ (root)**
5. Click **Save**
6. Wait 2–3 minutes → Your site will be live at:
   ```
   https://pathwaytodata.github.io/pathwaytodata-lms/
   ```
7. **Copy this URL** — you'll need it for Google Sites

---

## PHASE 2 — Set Up Google Sites

### Step 1: Open Google Sites
1. Go to https://sites.google.com (sign in with your Google account)
2. Click the **+** (Blank site) button

### Step 2: Name Your Site
1. Click "Untitled Site" at the top left → type `PathwayToData`
2. Click the page title area → type `Home`

### Step 3: Embed Your LMS (Full-Page Method)
1. In the right panel, click **Insert** tab
2. Scroll down to **Embed** → click it
3. In the dialog, click the **Embed code** tab
4. Paste this code (replace with YOUR GitHub Pages URL):
   ```html
   <iframe 
     src="https://pathwaytodata.github.io/pathwaytodata-lms/"
     width="100%" 
     height="100%"
     frameborder="0"
     style="border:none;"
     allow="payment"
   ></iframe>
   ```
5. Click **Next** → then **Insert**

### Step 4: Make it Full Screen
1. Click the embedded element
2. Drag resize handles to fill the entire page
3. Click on the element → click the **Full width** icon

### Step 5: Remove Google Sites Header (Optional)
1. Click the **Pages** icon (left panel)
2. Click ⋮ next to "Home" → **Page settings**
3. Toggle OFF "Show page title"

### Step 6: Publish Your Site
1. Click the blue **Publish** button (top right)
2. Choose a web address: `pathwaytodata` (you'll get `sites.google.com/view/pathwaytodata`)
3. Under "Who can view" → select **Anyone**
4. Click **Publish**

---

## PHASE 3 — Connect Your Custom Domain (www.pathwaytodata.com)

> You own this domain. Now point it to Google Sites.

### Step 1: Set Up Custom Domain in Google Sites
1. In your Google Site, click **Publish** → **Manage**
2. Click **Custom domain** → then **Start setup**
3. Type: `www.pathwaytodata.com`
4. Google will show you a **CNAME record** to add to your DNS
   - It will look like: `www → ghs.googlehosted.com`
5. **Copy the CNAME value** — don't close this window

### Step 2: Add DNS Records at Your Domain Registrar
*(Go to wherever you bought your domain — GoDaddy, Namecheap, BigRock, etc.)*

#### Option A — www.pathwaytodata.com (Subdomain CNAME)
| Type  | Name | Value                    | TTL  |
|-------|------|--------------------------|------|
| CNAME | www  | ghs.googlehosted.com     | 1hr  |

#### Option B — Also redirect root domain (pathwaytodata.com → www)
| Type | Name | Value              | TTL  |
|------|------|--------------------|------|
| A    | @    | 216.239.32.21      | 1hr  |
| A    | @    | 216.239.34.21      | 1hr  |
| A    | @    | 216.239.36.21      | 1hr  |
| A    | @    | 216.239.38.21      | 1hr  |

### Step 3: Verify Ownership
1. Back in Google Sites → it will ask you to verify ownership
2. Add a **TXT record** in your DNS:
   - Type: `TXT`
   - Name: `@`
   - Value: (the verification code Google gives you)
3. Wait 15–30 minutes for DNS to propagate
4. Click **Verify** in Google Sites

### Step 4: Done! 🎉
- After DNS propagates (up to 48 hours but usually 1–2 hrs):
  - `www.pathwaytodata.com` → Your LMS website

---

## PHASE 4 — Configure Razorpay (Payment Integration)

### Step 1: Create Razorpay Account
1. Go to https://razorpay.com → **Sign Up**
2. Complete KYC (business verification required for live payments)
3. For testing, go to **Dashboard** → **Settings** → **API Keys**
4. Click **Generate Test Key** → Copy your `Key ID`

### Step 2: Add Key to Your Website
1. Open `index.html` in any text editor (Notepad, VS Code)
2. Find this line:
   ```javascript
   key: 'YOUR_RAZORPAY_KEY_ID',
   ```
3. Replace with your actual key:
   ```javascript
   key: 'rzp_test_xxxxxxxxxxxx',  // Test mode
   // or
   key: 'rzp_live_xxxxxxxxxxxx',  // Live mode (after KYC)
   ```
4. Save the file → re-upload to GitHub (repeat Phase 1, Step 3)

### Step 3: Test Payment Flow
1. Open your site → click any course → "Enroll Now"
2. Use Razorpay test cards:
   - Card: `4111 1111 1111 1111`
   - Expiry: Any future date
   - CVV: Any 3 digits
   - OTP: `1234`

---

## PHASE 5 — Configure WhatsApp Integration

### Step 1: Get Your WhatsApp Business Number
1. Download **WhatsApp Business** app on your phone
2. Set up your business profile for PathwayToData

### Step 2: Update the Website
1. Open `index.html` → find:
   ```javascript
   const WA_NUMBER = '919800000000';
   ```
2. Replace with your number (91 = India country code):
   ```javascript
   const WA_NUMBER = '919XXXXXXXXX'; // Your 10-digit mobile
   ```
3. Save → re-upload to GitHub

### Step 3: (Optional) WhatsApp Business API
For automated responses, use **Interakt** or **Wati.io** (affordable Indian WhatsApp API providers):
1. Sign up at https://interakt.shop
2. Connect your WhatsApp Business number
3. Set up auto-reply for new leads

---

## PHASE 6 — (Optional) Google Forms Backend

To store contact form submissions in a Google Sheet:

1. Go to https://forms.google.com → Create a form with fields:
   - Name, Phone, Email, Status, Interests, Time, Message
2. Go to Responses → click Sheets icon (link to Google Sheets)
3. In your form, click **⋮** → **Get pre-filled link**
4. Use the form's `action` URL to submit from your website
5. Contact form submissions will appear in your Google Sheet

---

## 📱 MOBILE-FRIENDLY CONFIRMATION

Your website is fully responsive. Test it at:  
https://search.google.com/test/mobile-friendly

---

## 🔄 HOW TO UPDATE YOUR WEBSITE LATER

1. Edit `index.html` on your computer
2. Go to your GitHub repo
3. Click on `index.html` → click the ✏️ pencil icon
4. Paste your updated code → click **Commit changes**
5. GitHub Pages auto-updates within 2–3 minutes
6. Google Sites automatically shows the updated version

---

## ✅ CHECKLIST SUMMARY

- [ ] Create GitHub account + repo
- [ ] Upload `index.html` to GitHub  
- [ ] Enable GitHub Pages
- [ ] Create Google Site + embed iframe
- [ ] Publish Google Site
- [ ] Add custom domain in Google Sites
- [ ] Update DNS records at domain registrar
- [ ] Verify domain ownership
- [ ] Create Razorpay account + get API key
- [ ] Replace `YOUR_RAZORPAY_KEY_ID` in code
- [ ] Replace WhatsApp number in code
- [ ] Re-upload updated HTML to GitHub
- [ ] Test payment with Razorpay test card
- [ ] Test WhatsApp link opens correctly
- [ ] Test contact form submission

---

## 📞 Quick Reference: Important Links

| Service | URL |
|---------|-----|
| GitHub Pages | https://github.com |
| Google Sites | https://sites.google.com |
| Razorpay Dashboard | https://dashboard.razorpay.com |
| DNS Propagation Check | https://dnschecker.org |
| Mobile-Friendly Test | https://search.google.com/test/mobile-friendly |
| WhatsApp Business | https://business.whatsapp.com |

---

*PathwayToData LMS — Built with ❤️ for India's Data Education*

