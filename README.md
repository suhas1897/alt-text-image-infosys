# AltContextPro

An AI-powered image analysis tool that generates detailed alt text, contextual insights, and sentiment analysis for images using advanced AI models.

## Key Features

- **📥 Seamless Image Upload:** Drag-and-drop support for easy image processing.
- **🎨 AI-Driven Alt Text Generation:** Automatically generates descriptive alt text for enhanced accessibility.
- **🔎 Contextual Insights:** Provides enriched context about the content of images.
- **😎 Sentiment Analysis:** Detects emotional elements within images.
- **🤖 Multi-Model Integration:** Supports OpenAI, Gemini, and Hugging Face AI models.
- **🕺 Modern UI:** A stylish and responsive interface built with styled-components.

## Project Structure

## Deployment on Vercel

### Frontend Deployment

1. **Prepare Frontend**

   ```bash
   cd frontend
   npm run build  # Test build locally first
   ```

2. **Install Vercel CLI**

   ```bash
   npm install -g vercel
   ```

3. **Deploy to Vercel**

   ```bash
   vercel login
   vercel
   ```

   Alternatively, deploy via the Vercel Dashboard:

   - Push your code to GitHub.

   - Import your repository into the Vercel Dashboard.

   - Configure build settings:

     ```
     Build Command: npm run build
     Output Directory: .next
     Install Command: npm install
     ```

   - Add environment variables:

     ```
     NEXT_PUBLIC_API_URL=https://your-backend-url.vercel.app
     ```

### Backend Deployment

1. **Prepare Backend**

   - Create a `vercel.json` file in the backend directory:

   ```json
   {
     "version": 2,
     "builds": [
       {
         "src": "run.py",
         "use": "@vercel/python"
       }
     ],
     "routes": [
       {
         "src": "/(.*)",
         "dest": "run.py"
       }
     ]
   }
   ```

   - Generate `requirements.txt`:

   ```bash
   cd backend
   pipenv lock -r > requirements.txt
   ```

2. **Deploy Backend**

   ```bash
   vercel
   ```

   Alternatively, use the Vercel Dashboard:

   - Import your backend repository.
   - Configure build settings:
     ```
     Build Command: pip install -r requirements.txt
     Output Directory: .
     Install Command: python run.py
     ```
   - Add environment variables:
     ```
     HUGGINGFACE_API_KEY=your_key
     OPENAI_API_KEY=your_key
     GEMINI_API_KEY=your_key
     ```

### Post-Deployment

1. **Update Frontend API URL**

   - Obtain your backend deployment URL from Vercel.
   - Update the frontend environment variable:

   ```
   NEXT_PUBLIC_API_URL=https://your-backend-url.vercel.app
   ```

2. **Configure CORS**

   - Update backend CORS settings in `app/__init__.py`:

   ```python
   CORS(app, resources={
       r"/api/*": {
           "origins": ["https://your-frontend-url.vercel.app"],
           "methods": ["GET", "POST", "OPTIONS"]
       }
   })
   ```

3. **Verify Deployment**

   - Test the frontend: `https://your-frontend-url.vercel.app`
   - Test the backend: `https://your-backend-url.vercel.app/api/test`

### Troubleshooting Deployment

1. **Backend Issues**

   - Check Vercel logs for Python errors.
   - Ensure environment variables are correctly set.
   - Test API endpoints using Postman.

2. **Frontend Issues**

   - Check build logs in the Vercel dashboard.
   - Verify the API URL is correct.
   - Check the browser console for CORS errors.

3. **Common Solutions**

   - Redeploy after making environment variable changes.
   - Clear the Vercel cache if needed.
   - Check for function execution timeout limits.

