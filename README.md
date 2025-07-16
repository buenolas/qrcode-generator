# QR Code Generator

A Spring Boot application that generates QR codes and stores them in an AWS S3 bucket. The service provides public access URLs to the generated QR code images.

---

## 🚀 Features

- ✅ Generate QR codes from text input  
- ☁️ Upload and store QR code images to Amazon S3  
- 🔗 Retrieve public URLs for each generated code  
- 🛡️ Environment variable-based configuration for AWS credentials  
- 🐳 Dockerized for easy deployment  

---

## 🛠️ Technologies Used

- Java 21  
- Spring Boot 3  
- AWS SDK for Java (S3)  
- Maven  
- Docker  

---

## 📦 How to Build and Run

### 🔧 Requirements

- Java 21+
- Maven
- Docker (optional for containerized run)
- AWS credentials (IAM user with S3 access)

---

### 🧪 Running Locally

1. Clone the repository:

```bash
git clone https://github.com/buenolas/qrcode-generator.git
cd qrcode-generator
````

2. Set up the `.env` file (or export env vars):

```
AWS_ACCESS_KEY_ID=your-access-key-id
AWS_SECRET_ACCESS_KEY=your-secret-access-key
AWS_REGION=us-east-1
AWS_BUCKET_NAME=test-qrcode-storage-bueno
```

3. Build the project:

```bash
mvn clean package
```

4. Run the application:

```bash
java -jar target/qrcode-generator-0.0.1-SNAPSHOT.jar
```

---

### 🐳 Running with Docker

```bash
docker build -t qrcode-generator:1.0 .
docker run --env-file .env -p 8080:8080 qrcode-generator:1.0
```

---

## 📤 API Endpoints

| Method | Endpoint      | Description                                       |
| ------ | ------------- | ------------------------------------------------- |
| POST   | `/api/qrcode` | Generates a QR code from text and returns the URL |

### 📥 Example Request

```http
POST /api/qrcode
Content-Type: application/json

{
  "text": "https://example.com"
}
```

### 📤 Example Response

```json
{
  "url": "https://test-qrcode-storage-bueno.s3.us-east-1.amazonaws.com/abcd1234.png"
}
```

---

## 🔐 AWS Setup

To allow the app to upload files to S3, your IAM user should have the following policy attached:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:PutObject", "s3:GetObject", "s3:ListBucket"],
      "Resource": [
        "arn:aws:s3:::test-qrcode-storage-bueno",
        "arn:aws:s3:::test-qrcode-storage-bueno/*"
      ]
    }
  ]
}
```

Make sure your AWS credentials are valid and have the correct permissions to access the bucket.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).
