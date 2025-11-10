# File Upload with S3 📂

A modern file upload application built with Next.js and AWS S3, featuring drag-and-drop functionality, real-time upload progress, and image preview capabilities.

## Features

- 🚀 **Drag & Drop Upload**: Intuitive file upload with drag-and-drop support
- 📊 **Real-time Progress**: Visual upload progress tracking with percentage display
- 🖼️ **Image Preview**: Live preview of uploaded images with thumbnails
- 🗑️ **File Management**: Delete uploaded files with confirmation
- 📱 **Responsive Design**: Mobile-friendly interface with Tailwind CSS
- 🌙 **Dark/Light Theme**: Theme switching support with next-themes
- ⚡ **Fast Upload**: Direct-to-S3 upload using presigned URLs
- 🛡️ **Type Safety**: Full TypeScript support with Zod validation
- 📦 **File Validation**: Size and type restrictions (images only, max 10MB)
- 🎨 **Modern UI**: Beautiful components with Radix UI and Tailwind CSS

## Tech Stack

- **Framework**: [Next.js 16](https://nextjs.org/) with App Router
- **Language**: TypeScript
- **Styling**: [Tailwind CSS](https://tailwindcss.com/)
- **UI Components**: [Radix UI](https://radix-ui.com/)
- **File Upload**: [react-dropzone](https://react-dropzone.js.org/)
- **Cloud Storage**: AWS S3 (via t3.storage.dev)
- **Notifications**: [Sonner](https://sonner.emilkowal.ski/)
- **Icons**: [Lucide React](https://lucide.dev/)
- **Code Quality**: ESLint, Commitlint, Husky

## Getting Started

### Prerequisites

- Node.js 18+ 
- npm/yarn/pnpm/bun
- AWS S3 credentials or compatible S3 service

### Installation

1. Clone the repository:
```bash
git clone https://github.com/anhtudo97/file-upload.git
cd file-upload
```

2. Install dependencies:
```bash
npm install
# or
yarn install
# or
pnpm install
```

3. Set up environment variables:
Create a `.env.local` file in the root directory:
```env
AWS_ACCESS_KEY_ID=your_access_key
AWS_SECRET_ACCESS_KEY=your_secret_key
AWS_REGION=your_region
S3_BUCKET_NAME=your_bucket_name
```

4. Run the development server:
```bash
npm run dev
# or
yarn dev
# or
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000) to see the application.

## Project Structure

```
├── app/
│   ├── api/s3/
│   │   ├── upload/route.ts      # Presigned URL generation
│   │   └── delete/route.ts      # File deletion endpoint
│   ├── globals.css              # Global styles
│   ├── layout.tsx               # Root layout
│   └── page.tsx                 # Home page
├── components/
│   ├── ui/                      # Reusable UI components
│   └── web/
│       ├── Uploader.tsx         # Main upload component
│       └── UploadProgress.tsx   # Progress indicator
├── lib/
│   ├── S3Client.ts              # AWS S3 client configuration
│   └── utils.ts                 # Utility functions
└── public/                      # Static assets
```

## Usage

### Basic Upload
1. Visit the application in your browser
2. Click "Select Files" or drag and drop images onto the upload area
3. Watch real-time upload progress
4. View uploaded images in the gallery below

### File Management
- **Delete Files**: Click the trash icon on any uploaded image
- **Supported Formats**: Images only (JPEG, PNG, GIF, WebP, etc.)
- **File Limits**: Maximum 5 files, 10MB per file

## API Endpoints

### POST `/api/s3/upload`
Generates presigned URLs for direct S3 uploads.

**Request Body:**
```json
{
  "filename": "image.jpg",
  "contentType": "image/jpeg", 
  "size": 1048576
}
```

**Response:**
```json
{
  "presignedUrl": "https://...",
  "key": "uuid-filename.jpg"
}
```

### DELETE `/api/s3/delete`
Deletes files from S3 storage.

**Request Body:**
```json
{
  "key": "uuid-filename.jpg"
}
```

## Configuration

### S3 Setup
The application uses AWS S3-compatible storage. Update `lib/S3Client.ts` for your provider:

```typescript
export const S3 = new S3Client({
  region: "auto",
  endpoint: "https://your-s3-endpoint.com",
  forcePathStyle: false,
});
```

### Upload Limits
Modify upload restrictions in `components/web/Uploader.tsx`:

```typescript
const { getRootProps, getInputProps, isDragActive } = useDropzone({
  maxFiles: 5,           // Maximum number of files
  maxSize: 1024 * 1024 * 10, // 10MB file size limit
  accept: {
    "image/*": [],       // Accepted file types
  },
});
```

## Development

### Scripts
- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run start` - Start production server
- `npm run lint` - Run ESLint

### Code Quality
This project uses:
- **ESLint** for code linting
- **Commitlint** for conventional commits
- **Husky** for git hooks
- **TypeScript** for type safety

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Commit changes: `git commit -m 'feat: add amazing feature'`
4. Push to branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

## License

This project is open source and available under the [MIT License](LICENSE).

## Acknowledgments

- [Next.js](https://nextjs.org/) - The React framework
- [Tailwind CSS](https://tailwindcss.com/) - Utility-first CSS framework
- [Radix UI](https://radix-ui.com/) - Low-level UI primitives
- [AWS SDK](https://aws.amazon.com/sdk-for-javascript/) - AWS services integration
