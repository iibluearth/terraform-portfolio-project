# Terraform-Portfolio-Project 

<h1> Client Overview</h1>
<h3> Client: James Smith, Freelance Web Designer </h3>
<h3> Primary Goal: Deploy a modern, responsive single-page portfolio built with Next.js on a scalable, globally available AWS infrastructure using Infrastructure as Code (Terraform). </h3>
<i>James designed a clean, modern, single-page portfolio website using Next.js and wants it deployed on a globally accessible, secure, and scalable cloud infrastructure.</i>

<h2> Your Role </h2>
<h3> You are the Cloud Engineer Consultant tasked with deploying the website on AWS using Terraform to meet the client’s goals: </h3>

- High Availability
- Scalability
- Cost-Effective Hosting
- Fast Global Performance

<h2>Step 1: Create GitHub Repository</h2>

- Clone the repository locally:
`git clone https://github.com/your-username/terraform-portfolio-project.git`

<h2> Step 2: Clone Starter Kit and Set Up Project Locally </h2>

- Navigate to working directory: `cd C:\Users\Kayla`
- Clone a portfolio starter kit (e.g., from Vercel examples or custom): `npx create-next-app@latest nextjs-blog --use-npm --example "https://github.com/vercel/next-learn/tree/main/basics/learn-starter"`
- Move the code into your project folder: `mv nextjs-blog terraform_portfolio_project`
- Navigate into the Next.js blog folder: `cd "terraform_portfolio_project/nextjs-blog"`
- Start the dev server: `npm run dev`
- Open your browser to the local development URL (e.g., `http://localhost:3000`) to verify the site runs.

<p>
<img src="https://i.imgur.com/dTV0ECi.png"/>
</p>

<p>
<img src="https://i.imgur.com/B4L5RyS.png"/>
</p>

<h2> Step 3: Create Configuration File: (`next.config.js`) </h2> 

✅<i> This configuration is essential for exporting the site as static HTML using (`next export`).</i>

<p>
<img src="https://i.imgur.com/bRMnlM1.png"/>
</p>

<h2> Step 4: Build the Project </h2> 

- Run: `npm run build`
- You’ll now see:
  - `.next/`
  - `node_modules/`
  - `out/` → the static export folder you'll deploy to S3

<p>
<img src="https://i.imgur.com/NjlAEIe.png"/>
</p>

<h2> Step 5: Set Up Terraform Configuration </h2> 

- Create a new directory:
  - `mkdir terraform-nextjs`
  - `cd terraform-nextjs`

<i> This will hold your Infrastructure as Code files. </i>

<h2> Step 6: Create Terraform Files </h2> 
<h3> Create these Terraform files: </h3>

`state.tf` → for Terraform backend 
- Configure remote state with S3 and DynamoDB

<p>
<img src="https://i.imgur.com/vV6HHsQ.png"/>
</p>

`main.tf` → contains all AWS resources
<h4> Includes: </h4>

- AWS provider block

<h4> S3 Bucket </h4>

- Static website hosting
- Ownership control
- Block public access
- Access Control List (ACL)
- Bucket policy

<h4> CloudFront Distribution </h4>

- With Origin Access Identity (OAI)

<p>
<img src="https://i.imgur.com/6Je38ev.png"/>
</p>

<p>
<img src="https://i.imgur.com/1miVSa7.png"/>
</p>

<p>
<img src="https://i.imgur.com/SNkYxzL.png"/>
</p>

<p>
<img src="https://i.imgur.com/qJWRRIL.png"/>
</p>

<h2> Step 7: Configure Remote Backend for State </h2> 
<h3> 1. Create a new S3 bucket: </h3>
<p>
<img src="https://i.imgur.com/2rC3CRe.png"/>
</p>

<h3> 2. Create a new DynamoDB table: </h3>
<p>
<img src="https://i.imgur.com/k6LZZIc.png"/>
</p>

<h3> 3. Update state.tf with your new backend details. </h3>

<h2> Step 8: Initialize and Deploy with Terraform </h2>

- `cd terraform-nextjs` 

- `terraform init`
<p>
<img src="https://i.imgur.com/rJLkBCU.png"/>
</p>

- `terraform plan`
<p>
<img src="https://i.imgur.com/1sKJqHc.png"/>
</p>

- `terraform apply`
<p>
<img src="https://i.imgur.com/sYIhiVq.png"/>
</p>

✅<i> Use (`terraform show`) to review your applied resources. </i>
🔍<i> Copy the generated CloudFront domain output (e.g., `cloudfront_url`). </i>
<p>
<img src="[img]https://i.imgur.com/GGF7lva.png[/img]"/>
</p>

<h2> Step 9: Upload Next.js Static Site to S3 </h2>
<h3> From your Next.js project directory: </h3>

- `cd nextjs-blog`
- `aws s3 sync ./out s3://kk-my-tf-website-state`
<i> This uploads your statically generated portfolio to S3. </i>
<p>
<img src="https://i.imgur.com/Dkrdipm.png"/>
</p>

<h2> Step 10: Access the Deployed Portfolio </h2>
<h3> Get your live site URL: </h3>

- `terraform output cloudfront_url`

✅<i> Open it in your browser to view the globally available portfolio website. </i>

<h2> Step 11: Cleanup </h2>
<h3> When finished or for practice teardown: </h3>
 
  - `cd terraform-nextjs`
  - `terraform destroy`

<h2> Summary </h2>

- Next.js: Static Site Generator
- AWS S3: Static File Hosting
- AWS CloudFront: Global CDN
- Terraform: Infrastructure Management
- S3 + DynamoDB: State Locking
- GitHub: Version Control
