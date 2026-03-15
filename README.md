# 🎴 Econo-10X Membership Card Generator

**Complete jsreport-based ID-1 Card Generation System**

Version 1.0.0 | ISO/IEC 7810 Standard | HDP5000 Compatible

---

## 📦 Package Contents

This package contains everything needed to generate professional membership cards for the Econo-10X alternative economic ecosystem.

### Files Included

```
├── econo-10x-card-template.html       # Main HTML template for jsreport
├── sample-data.json                    # Sample data with URLs
├── sample-data-with-base64.json       # Sample data with embedded images
├── econo-10x-card-jsreport-config.json # Complete jsreport configuration
├── cardGenerator.js                    # Node.js integration module
├── package.json                        # npm package configuration
├── QUICKSTART.md                       # 5-minute quick start guide
├── SETUP_GUIDE.md                      # Comprehensive setup documentation
├── FIELD_SPECIFICATIONS.md             # Detailed technical specifications
└── README.md                           # This file
```

---

## 🎯 Quick Start (5 Minutes)

### Test in jsreport Playground

1. Go to https://playground.jsreport.net/
2. Set Recipe: `chrome-pdf`, Engine: `handlebars`
3. Configure Chrome PDF Options (see QUICKSTART.md)
4. Paste HTML from `econo-10x-card-template.html`
5. Paste data from `sample-data-with-base64.json`
6. Click Run → Download PDF

**Full instructions:** See `QUICKSTART.md`

---

## 📋 Card Specifications

### Physical Dimensions
- **Standard:** ISO/IEC 7810 ID-1 (Credit Card Size)
- **Size:** 85.60 mm × 53.98 mm (3.370 × 2.125 inches)
- **Material:** 30 mil PVC card stock
- **Printer:** Fargo HDP5000 (dual-sided with lamination)

### Card Layout

**Front (Page 1):**
- Econo-10X logo
- Circular profile photo (38mm diameter)
- Membership number (large, bold)
- Name, Surname, Structure fields
- QR code (22×22mm)

**Back (Page 2):**
- Econo-X logo
- Contact information
- "IF LOST, PLEASE CONTACT"
- Email, website, physical address

---

## 🔧 Field Inventory

| Field | Example Value | Max Length | Font |
|-------|---------------|------------|------|
| **Profile Image** | URL or Data URI | - | - |
| **Membership No** | CAP-1-000-100-164 | 20 chars | Poppins Bold 14pt |
| **Name** | Rethabile Cordelia | 25 chars | Poppins Bold 11pt |
| **Surname** | Mphahlele | 20 chars | Poppins Bold 11pt |
| **Structure** | Capricorn Cluster | 25 chars | Poppins Bold 11pt |
| **QR Code Data** | Member profile URL | 200 chars | - |

**Complete specifications:** See `FIELD_SPECIFICATIONS.md`

---

## 🎨 Brand Compliance

**Colors:**
- Navy: `#001f3f`
- Red: `#d90429`
- Grey: `#cbd5e1`

**Typography:**
- Headings/Values: Poppins (Google Fonts)
- Labels/Body: Lato (Google Fonts)

---

## 💻 Integration with Econo-10X System

### Node.js Module

```javascript
const { MembershipCardGenerator } = require('./cardGenerator');

const generator = new MembershipCardGenerator();

const memberData = {
  profile_image: 'https://...',
  membership_number: 'CAP-1-000-100-164',
  name: 'Rethabile Cordelia',
  surname: 'Mphahlele',
  structure: 'Capricorn Cluster'
};

// Generate PDF buffer
const pdfBuffer = await generator.generateCard(memberData);

// Or save to file
await generator.generateAndSave(memberData, './card.pdf');
```

### Database Integration

```javascript
const { CardGenerationService } = require('./cardGenerator');
const { Pool } = require('pg');

const db = new Pool({ /* PostgreSQL config */ });
const generator = new MembershipCardGenerator();
const service = new CardGenerationService(db, generator);

// Generate card for specific member
const pdf = await service.generateCardForMember(memberId);

// Generate cards for entire structure
const results = await service.generateCardsForStructure(structureId);
```

### API Endpoint Example

```javascript
// Express.js route
app.post('/api/cards/generate', async (req, res) => {
  try {
    const { member_id } = req.body;
    const service = new CardGenerationService(db, generator);
    const pdfBuffer = await service.generateCardForMember(member_id);
    
    res.contentType('application/pdf');
    res.send(pdfBuffer);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});
```

---

## 📚 Documentation

### For Quick Testing
→ **QUICKSTART.md** - 5-minute jsreport playground setup

### For Developers
→ **SETUP_GUIDE.md** - Complete technical documentation
→ **FIELD_SPECIFICATIONS.md** - Detailed positioning and specs
→ **cardGenerator.js** - Annotated Node.js module

### Key Sections in SETUP_GUIDE.md:
- jsreport configuration
- HDP5000 printer settings
- QR code generation
- Data validation rules
- Troubleshooting
- Production checklist

### Key Sections in FIELD_SPECIFICATIONS.md:
- Exact coordinates for all elements (in mm)
- Typography specifications
- Color palette (brand + print)
- Validation patterns
- CSS unit conversions
- Print production specs

---

## 🖨️ Production Workflow

```
1. Member Registration
   ↓
2. Profile Image Upload & Validation
   ↓
3. Membership Number Auto-Generation
   ↓
4. Structure Assignment (based on location)
   ↓
5. QR Code Data Generation
   ↓
6. jsreport API Call → PDF Generated
   ↓
7. PDF Stored (for reprints)
   ↓
8. Print Queue Updated
   ↓
9. HDP5000 Prints Card (both sides)
   ↓
10. Card Laminated
    ↓
11. Quality Control Check
    ↓
12. Card Dispatched to Member
```

---

## ✅ Testing Checklist

Before production deployment:

- [ ] Test in jsreport playground with sample data
- [ ] Verify all fonts load (Poppins, Lato)
- [ ] Test with various name lengths (short, long, special chars)
- [ ] Validate QR code generation and scanning
- [ ] Print test card on HDP5000
- [ ] Measure printed card (must be 85.6 × 53.98 mm)
- [ ] Verify lamination quality
- [ ] Test batch generation (10+ cards)
- [ ] Validate color consistency
- [ ] Check all field positioning accuracy
- [ ] Test error handling (missing data, invalid URLs)
- [ ] Verify database integration
- [ ] Test API endpoints
- [ ] Document any configuration changes

---

## 🔒 Data Validation

### Built-in Validation Rules

**Membership Number:**
- Pattern: `XXX-X-XXX-XXX-XXX`
- Example: `CAP-1-000-100-164`
- Regex: `/^[A-Z]{3}-\d{1}-\d{3}-\d{3}-\d{3}$/`

**Name:**
- Min: 2 characters
- Max: 25 characters (display truncation)
- Allowed: Letters, spaces, hyphens, apostrophes
- Case: Title Case

**Surname:**
- Min: 2 characters
- Max: 20 characters
- Allowed: Letters, spaces, hyphens, apostrophes
- Case: Title Case

**Structure:**
- Min: 3 characters
- Max: 25 characters
- Allowed: Letters, numbers, spaces
- Case: Title Case

**Profile Image:**
- Format: HTTPS URL or Data URI
- Types: JPG, PNG
- Max size: 500 KB
- Min resolution: 400×400 pixels
- Recommended: 600×600 pixels
- Aspect: 1:1 (square)

---

## 🚨 Troubleshooting

### Images Not Displaying
→ Use `sample-data-with-base64.json` which has embedded images
→ Or verify image URLs are publicly accessible with CORS enabled

### Fonts Not Loading
→ Check internet connection (Google Fonts CDN required)
→ Or download fonts and embed in template

### QR Code Missing
→ Verify QR API is accessible: https://api.qrserver.com/
→ Check QR data URL encoding

### Wrong Dimensions
→ Verify Chrome PDF settings: Custom 85.6mm × 53.98mm
→ Ensure all margins are 0mm

### Text Overlapping
→ Test with maximum length names
→ Adjust font sizes or positions if needed
→ Implement truncation for very long names

**Full troubleshooting guide:** See SETUP_GUIDE.md

---

## 🔄 Version History

**v1.0.0** (2026-03-15)
- Initial release
- ISO/IEC 7810 ID-1 standard implementation
- HDP5000 compatibility
- jsreport template with base64 support
- Node.js integration module
- Complete documentation suite

---

## 📞 Support & Contact

**Econo-X Technical Team**
- **Email:** info@econo-10x.co.za
- **Website:** www.econo-10x.co.za
- **Location:** Pretoria, Brooklyn Bridge rd, Bridge Office Park, Pretoria, 0570 Fehrse

For template modifications, technical support, or integration assistance, contact the development team.

---

## 📄 License

Proprietary - Econo-X (Pty) Ltd (Reg: 2021/582235/07)

This software and documentation are proprietary to Econo-X and may not be distributed, modified, or used without explicit permission.

---

## 🎯 Next Steps

1. **Test:** Run quick test in jsreport playground (QUICKSTART.md)
2. **Review:** Read FIELD_SPECIFICATIONS.md for technical details
3. **Integrate:** Use cardGenerator.js module in your system
4. **Deploy:** Set up jsreport server and HDP5000 printer
5. **Produce:** Generate cards for members

---

**Built for Econo-X Alternative Economic Ecosystem**
*Building Africa's Future Through Integrated Economic Ecosystems*
