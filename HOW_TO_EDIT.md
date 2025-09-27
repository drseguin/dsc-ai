# How to Edit This Website Visually

This guide will help you edit the website using Stackbit's visual editor interface, which allows you to make changes without touching code.

## Prerequisites

Make sure you have Node.js installed on your computer.

## Step 1: Install Stackbit CLI (One-time setup)

Open your terminal and run:

```bash
npm install -g @stackbit/cli
```

You only need to do this once. You might see some deprecation warnings - these are normal and can be ignored.

## Step 2: Start the Development Servers

You need to run TWO servers for visual editing to work:

### Terminal 1 - Start the Website Server
1. Open a terminal
2. Navigate to your project folder: `cd /Users/davidseguin/git/dsc-ai`
3. Run: `./start.sh` (or `npm run dev`)
4. Wait until you see "Ready in X.Xs" - this means the server is running on http://localhost:3000
5. **Keep this terminal open and running**

### Terminal 2 - Start the Visual Editor
1. Open a **NEW** terminal window (keep the first one running)
2. Navigate to your project folder: `cd /Users/davidseguin/git/dsc-ai`
3. Run: `stackbit dev`
4. Wait until you see "Server started" and "Open http://localhost:8090/_stackbit"

## Step 3: Access the Visual Editor

Open your web browser and go to:
**http://localhost:8090/_stackbit**

You'll need to register or sign in to Stackbit, then you'll be directed to the visual editor for your website.

## What You Can Edit Visually

Once in the visual editor, you can:

### Content Changes
- **Text content**: Click on any text to edit it directly
- **Images**: Click on images to replace them with new ones
- **Blog posts**: Add, edit, or delete blog posts
- **Page content**: Modify content on any page

### Layout Changes
- **Add new sections**: Add hero sections, feature sections, galleries, etc.
- **Rearrange content**: Drag and drop sections to reorder them
- **Change layouts**: Switch between different page layouts

### Styling Changes
- **Colors**: Change background colors, text colors
- **Spacing**: Adjust margins and padding
- **Typography**: Change fonts, sizes, styles
- **Component styles**: Modify button styles, card layouts, etc.

### Navigation
- **Menu items**: Add, remove, or reorder navigation links
- **Logo**: Replace the site logo (we recently changed it to DSC-logo.png)

## File-Based Editing (Alternative)

If you prefer to edit files directly, you can also modify:

- **Content pages**: Files in `content/pages/`
- **Blog posts**: Files in `content/pages/blog/`
- **Site settings**: Files in `content/data/`
- **Header/Footer**: `content/data/header.json` and `content/data/footer.json`

Changes to these files will automatically appear in both the development server and visual editor.

## Troubleshooting

### "Failed to connect to your site's local server"
- Make sure the Next.js server is running on localhost:3000 first
- Check that `npm run dev` is running in a separate terminal
- Wait for "Ready in X.Xs" message before starting Stackbit

### Visual editor not loading
- Make sure both servers are running
- Try refreshing the browser
- Check the terminal for any error messages

### Changes not appearing
- Save your changes in the visual editor
- Check that both terminal windows are still running
- Refresh your browser

## Saving Changes

- Changes made in the visual editor are automatically saved to your Git repository
- All changes are stored in the `content/` directory as markdown and JSON files
- You can commit and push changes to Git as usual

## Quick Reference

- **Website URL**: http://localhost:3000
- **Visual Editor URL**: http://localhost:8090/_stackbit
- **Start script**: `./start.sh`
- **Manual start**: `npm run dev` then `stackbit dev` in separate terminals

## Next Steps

- Explore the visual editor interface
- Try making small changes to see how it works
- Check out the Stackbit documentation for advanced features
- Remember to commit your changes to Git when you're happy with them