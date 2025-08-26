# Efficient Data Processing with PaddleOCR for Item Label Extraction

**Team Name:** AIKENS

## 🎯 Project Overview

This project focuses on automating the extraction of key product details from item labels using Optical Character Recognition (OCR). We successfully processed a large dataset of 131,000 images to extract numeric values and their corresponding units such as:

- Weight (kg, g, lbs)
- Volume (ml, L, oz)
- Wattage (W, kW)
- Dimensions (cm, mm, inches)

## 🛠️ Technology Stack

- **Primary OCR Tool:** PaddleOCR
- **Programming Language:** Python
- **Key Libraries:** 
  - PaddleOCR
  - Regular Expressions (regex)
  - NumPy (for distance calculations)

## 🔍 OCR Tools Evaluation

We conducted extensive testing of multiple OCR solutions:

### 1. Tesseract with PyTesseract
- ❌ Poor accuracy results
- ❌ Significant text extraction inaccuracies
- ❌ Unable to process some images correctly

### 2. EasyOCR
- ✅ Better results than Tesseract
- ❌ Compatibility issues across different systems
- ❌ Challenging uniform setup

### 3. PaddleOCR (Selected Solution)
- ✅ Superior accuracy and performance
- ✅ Easy to use and compatible across systems
- ✅ Excellent handling of multi-lingual text
- ✅ Effective processing of rotated text

## 🚀 Methodology

### Text and Number Extraction Strategy

1. **Unit Identification**
   - Extract all text from images using PaddleOCR
   - Identify relevant units based on expected entity names (kg, cm, W, etc.)

2. **Number Association**
   - Search for closest numeric values using coordinate-based proximity
   - Priority search order: left → top → right → bottom
   - Distance calculation using Euclidean distance between text blocks

3. **String Parsing Optimization**
   - Advanced regular expressions for text refinement
   - Handle edge cases (e.g., "3.5kg", numbers with special characters)

## 💡 Key Challenges & Solutions

### Challenge 1: Large Dataset Processing
**Problem:** Processing 131,000 images caused memory limitations and system crashes

**Solution:** Batch Processing
- Implemented batch processing with 500 images per batch
- Incremental processing with regular progress saves
- Optimal batch size determined through experimentation (100, 200, 500)

### Challenge 2: Memory Management
**Problem:** Memory leaks and system instability during large dataset operations

**Solution:** Efficient Memory Clearance
- Clear data structures after every batch
- Batch-wise result saving to prevent data loss
- Extended processing periods without crashes

### Challenge 3: Accuracy vs Performance
**Problem:** Initial OCR accuracy was only ~40% due to noisy/poor-quality images

**Solution:** Regex Refinements and Adaptive Techniques
- Improved accuracy to 60-70%
- Enhanced regex patterns for mixed alphanumeric strings
- Distance-based number-unit association

## 📊 Performance Metrics

- **Dataset Size:** 131,000 images
- **Batch Size:** 500 images per batch
- **Final Accuracy:** 60-70%
- **Processing Method:** Incremental batch processing
- **Memory Management:** Efficient clearance between batches

## 🏗️ System Architecture

```
Input Images (131K) 
    ↓
Batch Processing (500 images/batch)
    ↓
PaddleOCR Text Extraction
    ↓
Unit Identification
    ↓
Coordinate-based Number Association
    ↓
Regex Pattern Matching & Refinement
    ↓
Extracted Data (Weight, Volume, Wattage, Dimensions)
```

## 🎯 Key Success Factors

1. **Tool Selection:** Thorough OCR tool comparison and selection of PaddleOCR
2. **Scalable Processing:** Batch processing implementation for large datasets
3. **Memory Optimization:** Effective memory management strategies
4. **Accuracy Improvement:** Iterative regex and parsing logic refinements

## 📈 Results

- Successfully processed 131,000 product label images
- Achieved 60-70% accuracy in data extraction
- Created a scalable solution balancing resource constraints with extraction accuracy
- Automated extraction of critical product information including weights, volumes, wattages, and dimensions

## 🔧 Installation & Setup

```bash
# Install PaddleOCR
pip install paddleocr

# Additional dependencies
pip install numpy
pip install opencv-python
```

## 📝 Usage Example

```python
from paddleocr import PaddleOCR

# Initialize PaddleOCR
ocr = PaddleOCR(use_angle_cls=True, lang='en')

# Process image batch
def process_batch(image_batch):
    results = []
    for image_path in image_batch:
        # Extract text with coordinates
        result = ocr.ocr(image_path, cls=True)
        # Apply custom parsing logic
        extracted_data = parse_product_info(result)
        results.append(extracted_data)
    return results
```
mit
