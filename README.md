# POD Book Weight Calculator Documentation

## Overview
The POD (Print on Demand) Book Weight Calculator is a web application that provides accurate weight estimations for books based on their dimensions, paper type, and binding style. It's designed for publishers and printers to calculate approximate book weights for production planning and shipping calculations.

## Technical Specifications

### Technologies Used
- HTML5
- JavaScript (ES6+)
- Bootstrap 5.3.2
- CSS3

### Assets
- favicon-32x32.png (32x32 favicon)
- apple-touch-icon.png (180x180 Apple touch icon)

### Input Parameters

#### Required Fields
1. **Height (mm)**
   - Input type: Number
   - Unit: Millimeters
   - HTML ID: `length`
   - Validation: Required field

2. **Width (mm)**
   - Input type: Number
   - Unit: Millimeters
   - HTML ID: `width`
   - Validation: Required field

3. **Number of Pages**
   - Input type: Number
   - HTML ID: `pages`
   - Validation: Required field

4. **Paper Type (Grammage)**
   - Input type: Select dropdown
   - HTML ID: `paperType`
   - Options:
     * 70 gsm
     * 80 gsm
     * 90 gsm
     * 115 gsm
   - Validation: Required field

5. **Binding Type**
   - Input type: Select dropdown
   - HTML ID: `bindingType`
   - Options:
     * Limp Bound
     * Cased Bound
   - Validation: Required field

## Calculation Logic

### Base Weight Calculation
```javascript
// Convert dimensions from mm to meters
const lengthInM = length / 1000;
const widthInM = width / 1000;

// Calculate area of one page in square meters
const pageArea = lengthInM * widthInM;

// Calculate initial weight
let totalWeight = (pageArea * paperWeight * pages) / 2;
```

### Paper Weight Multipliers
The calculator uses different multipliers based on paper weight. These can be modified in the switch statement:

```javascript
switch (paperWeight) {
    case 70:
        baseMultiplier = 1.04;  // 4% addition
        break;
    case 80:
        baseMultiplier = 1.06;  // 6% addition
        break;
    case 90:
        baseMultiplier = 1.08;  // 8% addition
        break;
    case 115:
        baseMultiplier = 1.10;  // 10% addition
        break;
    default:
        baseMultiplier = 1.06;  // Default multiplier
}
```

### Binding Weight Additions
```javascript
if (bindingType === 'cased') {
    totalWeight += 150; // Add 150 grams for the case
}
```

## Modifiable Parameters

### To Modify Paper Weights:
1. Update the select options in the HTML:
```html
<select class="form-select" id="paperType" required>
    <option value="70">70 gsm</option>
    <!-- Add or modify options here -->
</select>
```

2. Update the corresponding switch statement in the JavaScript:
```javascript
switch (paperWeight) {
    case 70:
        baseMultiplier = 1.04;
    // Add or modify cases here
}
```

### To Modify Case Weight:
Adjust the fixed weight value in the binding condition:
```javascript
if (bindingType === 'cased') {
    totalWeight += 150; // Modify this value to change case weight
}
```

### To Add New Binding Types:
1. Add new option to the HTML select element:
```html
<select class="form-select" id="bindingType" required>
    <option value="limp">Limp Bound</option>
    <option value="cased">Cased Bound</option>
    <!-- Add new binding types here -->
</select>
```

2. Modify the binding logic in calculateWeight():
```javascript
if (bindingType === 'cased') {
    totalWeight += 150;
} else if (bindingType === 'newType') {
    // Add logic for new binding type
}
```

## Form Validation

### Required Field Validation
```javascript
const requiredFields = form.querySelectorAll('[required]');
requiredFields.forEach(field => {
    if (!field.value) {
        field.classList.add('is-invalid');
        isValid = false;
    }
});
```

### Form Reset Functionality
```javascript
function clearForm() {
    document.getElementById('calculatorForm').reset();
    document.querySelectorAll('.is-invalid')
        .forEach(element => element.classList.remove('is-invalid'));
    document.getElementById('result').style.display = 'none';
}
```

## Future Enhancement Suggestions

1. **Extended Paper Types**
   - Add more grammage options
   - Include different paper qualities
   - Add custom paper weight input

2. **Advanced Binding Options**
   - Variable case weights based on dimensions
   - Additional binding styles
   - Custom binding weight calculations

3. **User Interface Improvements**
   - Weight conversion options (g/kg/oz/lb)
   - Dimension conversion (mm/cm/inches)
   - Batch calculation capabilities
   - Save/load calculation presets

4. **Additional Features**
   - Cost calculation based on weight
   - Shipping cost estimations
   - PDF specification output
   - Weight history tracking

## Maintenance Notes

### Adding New Paper Types
1. Add new option to paperType select element
2. Add corresponding case in switch statement
3. Define appropriate multiplier for new paper weight

### Modifying Weight Calculations
1. Adjust multipliers in switch statement
2. Modify case weight value (150g default)
3. Update validation logic if needed

### Browser Compatibility
- Tested with modern browsers
- Uses ES6+ JavaScript features
- Requires Bootstrap 5.3.2 compatibility