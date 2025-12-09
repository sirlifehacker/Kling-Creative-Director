# **Kling 2.6 Creative Director: AI Video Generator**

## YouTube Video Walkthrough
For a visual walkthrough of how to setup the automation and multiple examples, [watch the video here](https://www.youtube.com/watch?v=DGNSc1QCocU&t=232s)

## **Overview**

The **Kling 2.6 Creative Director** is a fully autonomous **AI video-production pipeline** built inside **n8n**.  
It transforms a single reference image into a **cinematic video**, using:

- **OpenAI / GPT-4o-mini** for image analysis  
- A custom **Creative Director LLM agent** for generating cinematic camera movement + actor direction  
- **Kling 2.6 (Fal AI)** to render ultra-realistic videos  
- **Google Drive** for asset hosting  
- **Notion** for task management + status tracking  

The automation behaves like a *micro creative studio* running on autopilot — producing high-quality, realistic video ads that would normally take a full production team.
---

## **What This Automation Does**

For every row in your Notion database with `Status = Not started`, the workflow:

1. **Fetches pending shots** from Notion  
2. **Loops through each item**  
3. **Analyzes the reference image** (pose, clothing, lighting, environment, composition)  
4. **Generates a cinematic video concept** using a Creative Director LLM agent  
5. **Sends the concept to Kling 2.6** via Fal API  
6. **Polls until the video is finished**  
7. **Downloads the rendered video** as binary  
8. **Uploads it to Google Drive**  
9. **Updates Notion** with:  
   - the Google Drive video URL  
   - `Status = Done`  
10. **Moves to the next item**

This pipeline can generate **hundreds of fully-directed videos per day** automatically.

---

## **Tech Stack**

| Component | Purpose |
|----------|---------|
| **n8n** | Orchestrates the automation |
| **OpenAI GPT-4o-mini** | Structured vision analysis |
| **Creative Director LLM Agent** | Generates the cinematic shot direction |
| **Kling 2.6 (Fal AI)** | Image-to-video rendering |
| **Google Drive** | Storage for generated videos |
| **Notion** | Database of tasks + updates |

---


Every component is included in the JSON workflow export:  
:contentReference[oaicite:1]{index=1}

---

## **Setup Instructions**

### **1. Import the Workflow into n8n**
Use the provided JSON file and select **Import Workflow** inside n8n.

### **2. Add Required Credentials**

| Service | Required Credential |
|--------|----------------------|
| OpenAI | API Key |
| OpenRouter (optional) | API Key |
| Notion | Internal Integration Token |
| Google Drive | OAuth2 |
| Fal AI | API Key |

### **3. Prepare Your Notion Database**

Your database must include:

| Property | Type | Purpose |
|----------|------|---------|
| **Status** | Status | Must include “Not started”, “Done” |
| **Reference Photo** | URL | Google Drive link to the source image |
| **Kling Video** | URL | Will be automatically filled |
| **id** | Notion Page ID | Used internally |

The automation only processes items where `Status = Not started`.

### **4. Set Up Your Google Drive Folder**

Inside the Upload File node, replace the folder ID with your own if needed.

---

## **Kling 2.6 Cost Guide**

| Duration | Audio | Cost |
|----------|--------|------|
| **5 seconds** | No | $0.35 |
| **5 seconds** | Yes | $0.70 |
| **10 seconds** | No | $0.70 |
| **10 seconds** | Yes | $1.40 |

Use shorter clips for testing to keep experimentation cheap.

---

## **Customization**

### **Modify Camera Moves / Actor Actions**
Inside the **Creative Director Agent** LLM node, you’ll find lists of:

- Camera moves  
- Actor movements  
- Shot styles  

Add, remove, or adjust to match your brand or aesthetic.

### **Change Vision Model**
You can replace OpenAI Vision with:

- Gemini Flash  
- Claude 3.7 Vision  
- Luma Vision  
- Grok Vision  

As long as the JSON output is consistent.

### **Adjust Video Duration**
Change the `duration` parameter in the Kling API call.

---

## **Troubleshooting**

### **Image Doesn't Load in the Analyze Node**
Make sure reference images use a **Drive export link** (`uc?export=download&id=`).  
This workflow includes code to auto-convert normal Drive links into export links.

### **Kling Video Looks Wrong**
Try:

- Giving the Creative Director agent more specific constraints  
- Removing noise words from the prompt  
- Ensuring the reference image is clean and well-lit  

### **Notion Not Updating**
Confirm:

- Property names match exactly  
- Integration has write permissions  
- Database ID in the node is correct  

---

## **FAQ**

### **Can this run automatically every few minutes?**
Yes — schedule it with n8n’s Cron node.

### **Is this scalable to high volume?**
Yes — you can duplicate branches or use queues for higher throughput.

### **Does this work for clothing brands?**
This workflow is optimized for:

- Streetwear  
- Fitness apparel  
- Lifestyle brands  
- Influencer product demos  
- Commercial product modeling  

### **Can this generate videos without people?**
Yes — remove actor logic and generate product-only prompts.

---

## **Credits**

Built by **Sirlifehacker**  
Powered by **n8n**, **Fal AI**, **OpenAI**, **Notion**, **Google Drive**, and a custom Creative Director agent.

If you use or adapt this workflow, consider linking back to the repo so others can discover it.


