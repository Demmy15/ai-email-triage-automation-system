# AI Email Triage & Response Automation System 🤖📧

An enterprise-grade intelligent email management system that automatically classifies incoming emails into 9 business categories, generates context-aware responses using AI, and creates ready-to-send Gmail drafts - completely hands-free.

## 🎯 Overview

Transform email management from a time sink into an automated process. This system acts as an AI assistant that reads your emails, understands the context, categorizes them intelligently, and drafts professional responses that maintain your brand voice.

## ✨ Key Features

### 🧠 Intelligent Classification
- **Google Gemini AI** classifies emails into 9 business categories
- **Context-aware** analysis using full thread history
- **Custom classification rules** for each category with detailed criteria
- **Smart filtering** skips automated/no-reply emails

### 🤖 AI Response Generation
- **OpenAI GPT-4** generates human-quality responses
- **Category-specific playbooks** with 10-12 templates each
- **Conversation context** from previous 4 messages
- **Personalized greetings** using recipient's first name
- **Brand voice consistency** across all responses

### 📧 Professional Email Handling
- **HTML email formatting** with clean, email-safe markup
- **Branded signatures** with company details and social links
- **Thread preservation** maintains conversation flow
- **Gmail draft creation** for human review before sending
- **Auto-labeling** for organization and tracking

### 📊 Multi-Category Support

| Category | Description | Response Logic |
|----------|-------------|----------------|
| **High Priority - Orders** | POs, order confirmations, urgent fulfillment | Order acknowledgment, dispatch confirmation, tracking provision |
| **Customer Support** | Returns, refunds, product issues, FAQ | Empathetic responses with FAQ templates and resolution steps |
| **Shipping** | Tracking, delivery issues, logistics | Status updates, carrier coordination, customs guidance |
| **Finance Department** | Invoices, payments, VAT queries | Payment confirmations, invoice generation, account statements |
| **Wise Payments** | Transfer notifications, payment alerts | Auto-labeled (no response needed) |
| **Marketing/Collaborations** | Partnership proposals, influencer requests | Warm engagement with media kit requests and next steps |
| **Travel** | Bookings, itineraries, business travel | Acknowledgment with details confirmation |
| **Sales/Product Interest** | Pricing, wholesale, catalogue requests | Professional pitch with pricing and product info |
| **Miscellaneous** | General inquiries, networking, careers | Polite acknowledgment or redirection |

## 🛠️ Tech Stack

- **n8n** - Workflow orchestration (70+ nodes)
- **Gmail API** - Email reading, labeling, draft creation
- **Google Gemini 2.0 Flash** - Email classification
- **OpenAI GPT-4 Mini** - Response generation + HTML formatting
- **JavaScript** - Context extraction, data processing, HTML cleaning

## 📋 Workflow Architecture
```
Gmail Trigger (new unread email)
    ↓
Filter Check (skip no-reply addresses)
    ↓
Get Thread (fetch full conversation)
    ↓
HTTP Request (get email with full headers)
    ↓
Extract Context (parse HTML, get plain text)
    ↓
Split & Clean (remove HTML tags, preserve content)
    ↓
OpenAI Cleaner (extract clean text from HTML)
    ↓
Build Chronological Context (sort by date, last 4 messages)
    ↓
Google Gemini Classifier (categorize into 9 categories)
    ↓
Route to Category Handler:
    ├─→ High Priority Orders → Order Response Playbook
    ├─→ Customer Support → Support Response Playbook
    ├─→ Shipping → Logistics Response Playbook
    ├─→ Finance → Finance Response Playbook
    ├─→ Wise → Label Only (no response)
    ├─→ Marketing → Collaboration Response Playbook
    ├─→ Travel → Travel Acknowledgment Playbook
    ├─→ Sales → Sales Pitch Playbook
    └─→ Miscellaneous → General Response Playbook
    ↓
Generate AI Response (OpenAI with category-specific prompts)
    ↓
HTML Transformer (format response as email-safe HTML)
    ↓
Create Gmail Draft (with threading, signature, labels)
    ↓
Mark as Read + Log
```

## 🚀 Use Cases

- **E-commerce Operations**: Auto-handle order confirmations, shipping inquiries, returns
- **Customer Support Teams**: Generate first-draft responses to common queries
- **Sales Departments**: Respond to wholesale/pricing requests with pitch templates
- **Finance Teams**: Handle invoice requests, payment confirmations
- **Marketing Agencies**: Manage collaboration proposals, partnership inquiries
- **Logistics Coordinators**: Track shipments, coordinate with couriers
- **Any Business**: Receiving 50-200+ emails daily across multiple categories

## 📦 What's Included

- Complete n8n workflow JSON (70+ configured nodes)
- **9 Category Classification System** with detailed criteria
- **Response Playbooks** (10-12 templates per category, 100+ total)
- **HTML Email Templates** with customizable signatures
- **Context Extraction Logic** for thread awareness
- **Smart Filtering Rules** to skip automated emails
- **Error Handling** with graceful degradation
- **Full Documentation** with setup guide

## ⚙️ Setup Requirements

### Required Accounts & APIs
1. **n8n** - Self-hosted or cloud instance
2. **Gmail** - OAuth 2.0 access with Gmail API enabled
3. **Google Cloud** - Gemini AI API access
4. **OpenAI** - GPT-4 API key
5. **Company Domain** - For branded email signatures

### Cost Estimate (Monthly)
- **Gmail API**: Free (within quota)
- **Google Gemini**: ~$5-10 (per 1M tokens, classification)
- **OpenAI GPT-4 Mini**: ~$20-30 (response generation)
- **n8n**: Self-hosted free or $20-50/month cloud
- **Total**: ~$50-90/month for 1,000-2,000 emails

## 🔧 Installation

### 1. Import Workflow
```bash
# Import the JSON file into your n8n instance
```

### 2. Configure Gmail API
- Enable Gmail API in Google Cloud Console
- Create OAuth 2.0 credentials
- Add to n8n credentials manager
- Grant permissions: read, modify, draft creation

### 3. Set Up AI APIs
- **Google Gemini**: Create API key in Google AI Studio
- **OpenAI**: Generate API key from OpenAI dashboard
- Add both to n8n credentials

### 4. Customize Response Playbooks
Each category has a dedicated OpenAI node with system prompts. Edit these to match your:
- Company name and brand voice
- Product/service specifics
- Pricing and terms
- Contact information
- Industry terminology

### 5. Configure Email Signatures
Update HTML signature templates in each draft node:
- Company logo URL
- Team member names and titles
- Contact details (email, phone, website)
- Social media links
- Legal disclaimer text

### 6. Test Classification
Run manual tests with sample emails for each category to verify:
- Correct classification
- Appropriate response generation
- HTML formatting
- Signature appearance
- Gmail labeling

### 7. Activate Trigger
Enable the Gmail Trigger node to start processing new emails automatically.

## 📊 Customization Guide

### Adding New Categories
1. Add category to Gemini classifier prompt
2. Create classification criteria (keywords, exclusions)
3. Add route in Switch node
4. Create Gmail label
5. Build response playbook with templates
6. Add HTML transformer node
7. Configure draft creation node

### Modifying Response Templates
Each category playbook contains 10-12 templates. Edit the system prompt in the OpenAI node:
```javascript
Template 1 - [Scenario Name]
Hi [First Name],
[Response body with variables]
Best regards,
[Your Name]
```

### Adjusting Classification Logic
Edit the Gemini classifier prompt to:
- Add keywords for detection
- Define exclusion rules
- Set precedence between categories
- Fine-tune trigger signals

### Changing Email Signature
Update the HTML block in draft nodes:
```html
<table>
  <tr>
    <td><img src="YOUR_LOGO_URL" /></td>
    <td>
      <strong>Your Name</strong>
      <span>Your Title</span>
      <a href="mailto:YOUR_EMAIL">YOUR_EMAIL</a>
    </td>
  </tr>
</table>
```

## 🎓 Advanced Features

### Context Extraction
The workflow maintains conversation awareness by:
- Fetching full email threads (last 4 messages)
- Parsing complex HTML emails to extract plain text
- Building chronological context with sender/recipient info
- Passing context to AI for relevant responses

### Smart Filtering
- Skips emails from "noreply@" addresses
- Ignores automated system emails
- Filters marketing spam
- Only processes genuine human correspondence

### HTML Safety
- Email-safe HTML formatting (no external CSS)
- Clean paragraph structures
- Left-aligned text with proper spacing
- Compatible with all email clients
- Inline styles only

### Response Quality Control
- First-name personalization
- Context-aware content
- Category-appropriate tone
- Clear next steps
- Professional sign-offs
- No generic "AI voice"

## 💡 Best Practices

### For Classification Accuracy
- Regularly review misclassified emails
- Update trigger keywords based on patterns
- Refine exclusion rules to prevent overlaps
- Test new edge cases

### For Response Quality
- Maintain consistent brand voice in templates
- Include specific product/service details
- Offer clear next steps in every response
- Keep responses concise but helpful
- Review and edit drafts before sending

### For System Maintenance
- Monitor API usage and costs
- Check error logs weekly
- Update templates quarterly
- Archive old conversation contexts
- Backup workflow regularly

## 🐛 Troubleshooting

### Common Issues

**Classification Errors**
- Review Gemini prompt for clarity
- Check for keyword conflicts between categories
- Verify exclusion rules are working

**Draft Not Created**
- Confirm Gmail API permissions
- Check thread ID validity
- Verify HTML formatting is valid

**Context Missing**
- Ensure HTTP Request returns full payload
- Verify JSON parsing in Code nodes
- Check OpenAI token limits

**Poor Response Quality**
- Add more examples to playbook prompts
- Increase specificity in system instructions
- Review context being passed to OpenAI

## 📄 License

MIT License - Free for personal and commercial use

## 🤝 Contributing

Contributions welcome! Areas for enhancement:
- Additional category templates
- Multi-language support
- Sentiment analysis integration
- Auto-send for high-confidence responses
- Analytics dashboard
- Mobile app notifications

## 📚 Resources

- [n8n Documentation](https://docs.n8n.io)
- [Gmail API Reference](https://developers.google.com/gmail/api)
- [Google Gemini API](https://ai.google.dev/docs)
- [OpenAI API Docs](https://platform.openai.com/docs)

---

**⚡ Intelligent email management, perfected**

*From inbox chaos to organized automation in one workflow.*
