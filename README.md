# 🌾 Crop Residue Utilization Analyzer

An AI-powered tool to help farmers make optimal decisions for crop residue management, promoting sustainable agriculture and reducing crop burning.

## Features

- **Smart Analysis**: Evaluates 5+ residue utilization methods
- **Financial Planning**: Cost-benefit analysis with payback periods
- **Carbon Impact**: Shows environmental benefits vs burning
- **Government Schemes**: Matches relevant subsidies and support programs
- **Action Plans**: Step-by-step implementation guides
- **Farmer-Friendly**: Simple language, practical recommendations

## Utilization Methods Analyzed

1. **Composting** - Convert to organic fertilizer
2. **Biogas Production** - Generate cooking fuel + fertilizer
3. **Biomass Resale** - Sell to power plants/pellet units
4. **Biochar Production** - Create soil amendment
5. **Mulching/Incorporation** - Direct soil enrichment

## Quick Start

### Python Script

```bash
python crop_residue_analyzer.py
```

### Web Interface

Open `web_interface.html` in any browser for a user-friendly form.

## Input Parameters

- Crop Type (Rice, Wheat, Sugarcane, etc.)
- Land Size (acres)
- Residue Quantity (tons)
- Location (State/District)
- Distance to nearest processing plant
- Available machinery
- Labor availability
- Transport access
- Budget range

## Output Includes

### A. Summary Recommendation
Best method with reasoning

### B. Ranked Options Table
Top 3 options with:
- Feasibility score (0-100%)
- Setup costs
- Expected revenue/savings
- Payback period
- Effort level
- Risks

### C. Carbon Impact Analysis
- CO2 from burning
- CO2 saved through conversion
- Net carbon reduction
- Tree planting equivalent

### D. Financial Comparison
Investment vs returns analysis

### E. Government Schemes
Relevant subsidies and eligibility

### F. Action Plan
5-7 step implementation guide

## Example Usage

```python
from crop_residue_analyzer import CropResidueAnalyzer

farmer_data = {
    'crop_type': 'Rice',
    'land_size': 5,
    'residue_quantity': 15,
    'location': 'Ludhiana, Punjab',
    'distance_to_plant': 25,
    'machinery_available': ['tractor', 'rotavator'],
    'labor_available': 'Medium',
    'transport_access': 'Good',
    'budget': 50000
}

analyzer = CropResidueAnalyzer(farmer_data)
report = analyzer.analyze()
print(report)
```

## Benefits

- **For Farmers**: Maximize residue value, reduce costs
- **For Environment**: Reduce air pollution, carbon emissions
- **For Soil**: Improve fertility, organic matter
- **For Community**: Cleaner air, sustainable practices

## Government Schemes Covered

- PM-KUSUM
- National Biofuel Policy
- State Crop Residue Management Schemes
- Subsidy programs for machinery
- Price support mechanisms

## Contact & Support

For technical guidance:
- Nearest Krishi Vigyan Kendra (KVK)
- District Agriculture Office
- State Agriculture Department

## License

Open source for agricultural development

---

**Note**: This tool provides recommendations based on general parameters. Always consult local agricultural experts for site-specific advice.
