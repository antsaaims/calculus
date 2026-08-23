*A free Obsidian + Quartz + GitHub Pages workflow for creating a course website with notes, concept maps, LaTeX, search, and automatic deployment.*  


## Goal  

I wanted a website where I could:  

- Create notes in Obsidian  
- Build interactive concept maps using Obsidian Canvas  
- Write mathematics in LaTeX  
- Publish everything automatically  
- Avoid paying for Obsidian Publish (context: I'm a graduate student!)
- Give students a single website that updates whenever I update my notes  

The final result is:  

```text  

Obsidian  

↓  

Obsidian Git  

↓  

GitHub  

↓  

GitHub Actions  

↓  

Quartz  

↓  

Course Website  

```  

# Step 1: Create a Quartz Website  

## Install Node.js  

Download and install the latest LTS version of Node.js:  

https://nodejs.org  


Verify installation:  


```powershell  

node --version  

npm --version  

```  
  
## Create a GitHub Repository  

Create a new public repository:  


```text  

calculus  

```  

  
(or whatever you want to call your website)  

## Clone the Repository  
 

Using GitHub Desktop:  


```text  

File  

→ Clone Repository  

```  

Clone it somewhere convenient, for example:  

```text  

D:\Repositories\calculus  

```  

## Install Quartz  

Open a terminal in the repository:  

```powershell  

npm install  

npx quartz create  

```  

When prompted:  

```text  

Choose how to initialize content:  

```  

select:  

```text  

Empty Quartz  

```  

When asked for the site URL enter:  

```text  

https://YOUR_USERNAME.github.io/REPOSITORY_NAME  

```  

Example:  

```text  

https://antsaaims.github.io/calculus  

```  
 
## Preview Locally  
 
Run:  
 

```powershell  

npx quartz build --serve  

```  
 
Open:  

```text  

http://localhost:8080  

```  

You should see your website.  
# Step 2: Deploy to GitHub Pages  

## Enable GitHub Pages  

On GitHub:  

```text  

Repository  

→ Settings  

→ Pages  

```  

Set:  

```text  

Source = GitHub Actions  

```  

## Add a GitHub Pages Workflow  

Create:  


```text  

.github/workflows/pages.yml  

```  

  

with:  

  

```yaml  

name: Deploy Quartz to GitHub Pages  

  

on:  

push:  

branches:  

- v5  

  

permissions:  

contents: read  

pages: write  

id-token: write  

  

concurrency:  

group: pages  

cancel-in-progress: true  

  

jobs:  

build:  

runs-on: ubuntu-latest  

  

steps:  

- uses: actions/checkout@v4  

  

- uses: actions/setup-node@v4  

with:  

node-version: 24  

  

- run: npm install  

  

- run: npx quartz build  

  

- uses: actions/upload-pages-artifact@v3  

with:  

path: public  

  

deploy:  

needs: build  

runs-on: ubuntu-latest  

  

environment:  

name: github-pages  

url: ${{ steps.deployment.outputs.page_url }}  

  

permissions:  

pages: write  

id-token: write  

  

steps:  

- id: deployment  

uses: actions/deploy-pages@v4  

```  

Commit and push.  


Once the workflow succeeds, the site will be live:  


```text  

https://YOUR_USERNAME.github.io/REPOSITORY_NAME  

```  

# Step 3: Install Git  


Install Git for Windows:  
https://git-scm.com/download/win  
Verify:  

```powershell  

git --version  

```  

# Step 4: Install Obsidian Git  

Inside Obsidian:  

```text  

Settings  

→ Community Plugins  

→ Browse  

→ Obsidian Git  

```  

Install and enable it.  
# Step 5: The Critical Canvas Fix  

At first I opened:  

```text  

D:\Repositories\calculus  

```  

as my vault.  

  
This caused Canvas file cards to store paths like:  

```json  

"file":"content/concepts/rate-of-change.md"  

```  

  

Quartz interpreted those paths incorrectly and generated broken links.  

## Correct Solution  

Open:  

```text  

D:\Repositories\calculus\content  

```  

as the Obsidian vault.  

Now Canvas stores:  
```json  

"file":"concepts/rate-of-change.md"  

```  

which Quartz understands correctly.  

This solved:  

- Canvas file links  
- Note previews  
- Clickable concept maps  

# Step 6: Organize Content  

I use:  

```text  

content/  

├── index.md  

├── Concepts/  

│ ├── Rate of Change.md  

│ ├── Accumulated Change.md  

│ └── Signed Area.md  

├── Concept Maps/  

│ ├── Functions and Derivatives.canvas  

│ └── Integration.canvas  

├── Unit 1/  

├── Unit 2/  

├── Unit 6/  

└── Resources/  

```  

Everything inside `content/` is published automatically.  
# Step 7: Use File Cards in Canvas  

Instead of large text cards, I use:  

```text  

Markdown Note  

↓  

Canvas File Card  

```  
Example note:  

```markdown  

# Rate of Change  

  

$$  

f(x)=F'(x)  

$$  

  

How fast a quantity changes.  

```  

When dragged into a Canvas:  

```text  

Rate of Change  

--------------  

f(x)=F'(x)  

  

How fast a quantity changes.  

```  

Advantages:  

- LaTeX works  
- Preview works  
- Clicking opens the full note  
- Easy to maintain  

# LaTeX Notes  


LaTeX works correctly in Markdown notes:  


```markdown  

$$  

F(b)-F(a)  

=  

\text{Signed Area}  

$$  

```  



In my experience:  

- Markdown notes render LaTeX correctly.  

- Canvas text cards do not reliably render LaTeX.  

For best results, put mathematical content inside notes and use file cards in the Canvas.  
# Daily Workflow  

## Create Notes  

Create notes inside:  

```text  

content/  

```  


Example:  

```text  

content/Unit 6/Section 6.1.md  

```  
## Create Concept Maps  


Create:  

```text  

.canvas  

```  

files and drag notes onto the Canvas as file cards.  
## Sync  

Use:  

```text  

Ctrl+P  

→ Obsidian Git: Commit-and-sync  

```  


## Automatic Deployment  
After syncing:  


```text  

Obsidian  

↓  

GitHub  

↓  

GitHub Actions  

↓  

Quartz  

↓  

Website Updated  

```  

usually within a minute.  
# Final Result  

  
This setup provides:  
✅ Free website hosting  
✅ Obsidian editing workflow  
✅ Automatic deployment  
✅ LaTeX support  
✅ Interactive Canvas concept maps  
✅ Search  
✅ Graph view  
✅ Version history  
✅ Git backups  
✅ Student-friendly URLs  
# If I Were Starting Again  

  I would:  
1. Create the Quartz site.  
2. Deploy GitHub Pages.  
3. Open the **content folder** as the Obsidian vault.  
4. Install Obsidian Git.  
5. Build all concept maps using file cards linked to notes.  
 

This avoids every issue I encountered and produces a very smooth workflow.