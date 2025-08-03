# CompressoX - Advanced Multi-File Compression Platform

<div align="center">

![CompressoX Logo](https://img.shields.io/badge/CompressoX-Multi--File%20Compressor-00ff9d?style=for-the-badge&logo=python)
![Python](https://img.shields.io/badge/Python-3.8+-blue?style=for-the-badge&logo=python)
![Flask](https://img.shields.io/badge/Flask-2.0+-red?style=for-the-badge&logo=flask)
![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-yellow?style=for-the-badge&logo=javascript)

**A powerful, modern file compression application supporting multiple file formats with both lossy and lossless compression algorithms.**

[Features](#features) • [Installation](#installation) • [Usage](#usage) • [API Documentation](#api-documentation) • [Architecture](#architecture) • [Contributing](#contributing)

</div>

---

## 🚀 Features

### 📁 Multi-Format Support
- **Images**: JPEG, PNG, GIF, BMP, WebP
- **Videos**: MP4, AVI, MOV, WMV, WebM
- **Documents**: PDF, DOCX, DOC
- **Text Files**: TXT, MD, LOG, HTML, CSS, JS

### 🔧 Compression Algorithms
- **Lossy Compression**: Optimized for maximum file size reduction
- **Lossless Compression**: Preserves original quality
- **Adaptive Quality Control**: 1-100% quality adjustment
- **Real-time Statistics**: Live compression ratio and size metrics

### 🎯 Advanced Algorithms
- **Huffman Coding**: Frequency-based compression
- **Run-Length Encoding (RLE)**: Sequential data compression
- **LZ77/LZ78**: Dictionary-based compression
- **DCT Transform**: Discrete Cosine Transform for images/videos
- **Motion Compensation**: Video frame optimization

### 💻 Modern Interface
- **Responsive Design**: Works on desktop and mobile
- **Drag & Drop**: Intuitive file upload
- **Real-time Preview**: File preview before compression
- **Progress Tracking**: Live compression progress
- **Dark Theme**: Modern, eye-friendly interface

## 📋 Prerequisites

- Python 3.8 or higher
- Node.js (optional, for development)
- Modern web browser

## 🛠️ Installation

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/compressox.git
cd compressox
```

### 2. Set Up Python Environment
```bash
# Create virtual environment
python -m venv .venv

# Activate virtual environment
# On Windows:
.venv\Scripts\activate
# On macOS/Linux:
source .venv/bin/activate
```

### 3. Install Dependencies
```bash
# Install Python dependencies
pip install -r requirements.txt
```

### 4. Install Frontend Dependencies (Optional)
```bash
# Navigate to frontend directory
cd frontend

# Install Node.js dependencies (if using npm)
npm install
```

## 🚀 Quick Start

### 1. Start the Backend Server
```bash
# From the project root
cd CompressoX_Backend
python app.py
```

The server will start on `http://localhost:8080`

### 2. Open the Frontend
```bash
# Open frontend/index.html in your browser
# Or serve it using a local server:
python -m http.server 8000
# Then visit http://localhost:8000
```

### 3. Start Compressing!
1. Drag and drop files or click to browse
2. Choose compression mode (Lossy/Lossless)
3. Adjust quality settings
4. Click "Compress File"
5. Download your compressed file

## 📖 Usage Guide

### Web Interface
1. **File Upload**: Drag files to the upload area or click to browse
2. **Compression Mode**: 
   - **Lossy**: Smaller file size, some quality loss
   - **Lossless**: Preserves quality, larger file size
3. **Quality Control**: Adjust from 1-100% (affects compression ratio)
4. **Compression**: Click "Compress File" to start
5. **Download**: Get your compressed file instantly

### Supported File Types

| File Type | Extensions | Compression Mode |
|-----------|------------|------------------|
| Images | .jpg, .jpeg, .png, .bmp, .gif | Lossy/Lossless |
| Videos | .mp4, .avi, .mov, .wmv | Lossy/Lossless |
| Documents | .pdf, .docx, .doc | Lossy/Lossless |
| Text | .txt, .md, .log | Lossy/Lossless |

## 🔌 API Documentation

### Base URL
```
http://localhost:8080
```

### Endpoints

#### 1. Get Compression Metadata
```http
POST /compress/metadata
```

**Request:**
- `files`: File to compress
- `fileType`: Type of file (image, video, pdf, docx, text)
- `isLossy`: Boolean (true/false)
- `quality`: Integer (1-100)

**Response:**
```json
{
  "success": true,
  "algorithm": "JPEG DCT Compression",
  "description": "Uses Discrete Cosine Transform with quality 50",
  "original_size": 1024000,
  "compressed_size": 512000,
  "ratio": 2.0
}
```

#### 2. Get Compressed File
```http
POST /compress/file
```

**Request:** Same as metadata endpoint

**Response:** Compressed file as binary data

#### 3. Health Check
```http
GET /health
```

**Response:**
```json
{
  "status": "healthy"
}
```

### Example API Usage

```javascript
// Get compression metadata
const formData = new FormData();
formData.append('files', file);
formData.append('fileType', 'image');
formData.append('isLossy', 'true');
formData.append('quality', '50');

const response = await fetch('http://localhost:8080/compress/metadata', {
  method: 'POST',
  body: formData
});

const metadata = await response.json();
console.log('Compression ratio:', metadata.ratio);
```

## 🏗️ Architecture

### Backend Structure
```
CompressoX_Backend/
├── app.py                 # Main Flask application
├── algorithms/            # Compression algorithms
│   ├── __init__.py
│   ├── text_compression.py
│   ├── text_lossy_compression.py
│   ├── text_lossless_compression.py
│   ├── image_compression.py
│   ├── pdf_compression.py
│   ├── video_compression.py
│   └── docx_compression.py
└── temp/                  # Temporary files
```

### Frontend Structure
```
frontend/
├── index.html            # Main application page
├── script.js             # JavaScript functionality
└── styles.css            # Styling and animations
```

### Compression Algorithms

#### Text Compression
- **Lossy**: Whitespace removal, punctuation removal, case conversion
- **Lossless**: Huffman coding with frequency analysis

#### Image Compression
- **Lossy**: JPEG with DCT transform and quantization
- **Lossless**: PNG with DEFLATE algorithm

#### Video Compression
- **Lossy**: Motion compensation, DCT transform, frame differencing
- **Lossless**: Huffman coding, RLE, LZ77 compression

#### PDF Compression
- **Lossy**: Image compression, structure optimization
- **Lossless**: Stream compression, object optimization

#### DOCX Compression
- **Lossy**: Image compression, color reduction
- **Lossless**: Structure optimization, content compression

## 🛠️ Development

### Project Structure
```
compressox/
├── CompressoX_Backend/     # Backend Flask application
│   ├── algorithms/         # Compression algorithms
│   ├── app.py             # Main application
│   └── temp/              # Temporary files
├── frontend/              # Frontend web application
│   ├── index.html         # Main page
│   ├── script.js          # JavaScript logic
│   └── styles.css         # Styling
├── .venv/                 # Python virtual environment
├── requirements.txt        # Python dependencies
└── README.md             # This file
```

### Adding New Compression Algorithms

1. Create new algorithm file in `CompressoX_Backend/algorithms/`
2. Implement compression function with standard interface
3. Add import to `algorithms/__init__.py`
4. Update `app.py` to handle new file types

### Example Algorithm Interface
```python
def compress_new_format(input_path: str, output_path: str, is_lossy: bool = True, quality: int = 50) -> dict:
    """
    Compress a new file format
    
    Returns:
        dict: {
            'success': bool,
            'algorithm': str,
            'description': str,
            'original_size': int,
            'compressed_size': int,
            'ratio': float
        }
    """
    # Implementation here
    pass
```

## 🧪 Testing

### Backend Testing
```bash
# Run backend tests
cd CompressoX_Backend
python -m pytest tests/
```

### Frontend Testing
```bash
# Run frontend tests
cd frontend
npm test
```

## 📊 Performance

### Compression Ratios
- **Text Files**: 2-5x compression (lossless), 3-8x (lossy)
- **Images**: 2-10x compression (lossy), 1.5-3x (lossless)
- **Videos**: 3-15x compression (lossy), 2-5x (lossless)
- **PDFs**: 1.5-4x compression (lossless)
- **DOCX**: 1.2-3x compression (lossless)

### Processing Speed
- **Small Files (< 1MB)**: < 1 second
- **Medium Files (1-10MB)**: 1-5 seconds
- **Large Files (10-100MB)**: 5-30 seconds

## 🤝 Contributing

We welcome contributions! Please follow these steps:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/AmazingFeature`)
3. **Commit** your changes (`git commit -m 'Add some AmazingFeature'`)
4. **Push** to the branch (`git push origin feature/AmazingFeature`)
5. **Open** a Pull Request

### Contribution Guidelines
- Follow PEP 8 for Python code
- Use meaningful commit messages
- Add tests for new features
- Update documentation as needed

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **PIL/Pillow**: Image processing capabilities
- **OpenCV**: Video processing and computer vision
- **PyPDF2**: PDF manipulation and compression
- **python-docx**: DOCX file handling
- **Flask**: Web framework for the backend
- **Font Awesome**: Icons and UI elements

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/yourusername/compressox/issues)
- **Discussions**: [GitHub Discussions](https://github.com/yourusername/compressox/discussions)
- **Email**: your.email@example.com

## 🔄 Changelog

### Version 1.0.0 (Current)
- ✅ Multi-format file compression
- ✅ Lossy and lossless compression modes
- ✅ Real-time compression statistics
- ✅ Modern web interface
- ✅ RESTful API
- ✅ Comprehensive algorithm support

---

<div align="center">

**Made with ❤️ by [Your Name]**

[![GitHub stars](https://img.shields.io/github/stars/yourusername/compressox?style=social)](https://github.com/yourusername/compressox)
[![GitHub forks](https://img.shields.io/github/forks/yourusername/compressox?style=social)](https://github.com/yourusername/compressox)
[![GitHub issues](https://img.shields.io/github/issues/yourusername/compressox)](https://github.com/yourusername/compressox/issues)

</div>
