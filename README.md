# 🍯 Hundred Acre Garden

A whimsical garden planning dashboard themed around Winnie the Pooh's Hundred Acre Wood. Built for Zone 6 gardening in Akron, Ohio.

![Garden Planner Preview](https://img.shields.io/badge/Theme-Hundred%20Acre%20Wood-E8A838?style=for-the-badge)
![Zone](https://img.shields.io/badge/Zone-6-4A7C42?style=for-the-badge)
![Last Frost](https://img.shields.io/badge/Last%20Frost-May%204-87CEEB?style=for-the-badge)

## 🌻 Features

### Dashboard
- **Overview Stats**: Track total plants, started seeds, and task completion
- **Progress Bars**: Visual progress for seeds started and tasks completed
- **Upcoming Tasks**: High-priority items that need attention
- **Important Notes**: Warnings about special requirements (tomatillos need 2+ plants, etc.)

### Timeline View (Christopher Robin's Planting Calendar)
- **Visual Timeline**: Week-by-week view of your entire planting schedule
- **Color-Coded Tasks**: 
  - 🟢 Green: Start indoors
  - 🔵 Blue: Transplant to garden
  - 🌱 Direct sow
- **Current Week Indicator**: Easily see where you are in the season

### Plant Encyclopedia (Owl's Encyclopedia)
- **21 Plant Varieties** with detailed information:
  - Planting dates (indoor start vs direct sow)
  - Transplant dates
  - Spacing requirements
  - Days to harvest
  - Growing tips and warnings
- **Status Tracking**: 
  - Not Planted → Germinating → Growing → Hardening Off → In Garden → Flowering → Harvesting
- **Filter by Type**: Tomato, Pepper, Brassica, Root, Herb, etc.
- **Character Associations**: Each plant is assigned to a Hundred Acre Wood character!

### Garden Layout (Rabbit's Garden Map)
- **Interactive 30' × 60' Grid**: Click to place plants
- **6-inch Resolution**: Each cell represents 6" × 6"
- **Plant Selection**: Choose from your seed inventory
- **Color-Coded Legend**: See what's planted where
- **Clear All Option**: Start fresh anytime

### Task Checklist (Piglet's To-Do List)
- **Auto-Generated Tasks**: Based on your plant schedule
- **Priority Levels**: High/Medium/Low based on timing
- **Check Off Completed**: Track your progress
- **Persistent Storage**: Tasks save between visits

### Notifications & Reminders
- **Browser Notifications**: Get alerts for upcoming tasks (requires permission)
- **Google Calendar Integration**: Click "Remind" to add events to your calendar
- **In-App Notifications**: Toast messages for status updates

## 🌱 Your 2025 Seed Inventory

### Tomatoes (Start indoors ~March 8)
1. San Marzano - Paste tomato for sauce
2. Purple Bumble Bee - Striped cherry
3. Druzba - Bulgarian heirloom
4. Boxcar Willie - Classic red slicer
5. Black Sea Man - Russian heirloom
6. Azoychka - Yellow Russian heirloom

### Other Nightshades
7. Rio Grande Verde Tomatillo (⚠️ Need 2+ plants!)
8. Big Red Bell Pepper

### Brassicas
9. Catskill Brussels Sprout (Best after frost!)
10. White Vienna Kohlrabi
11. Broccoli Rabe - Spring Rapini

### Cucurbits
12. Luffa Gourd (⚠️ Challenging in Zone 6!)
13. Marketmore 76 Cucumber

### Corn
14. Peaches and Cream (Plant in 4+ row blocks!)

### Root Vegetables (Direct Sow)
15. Danvers 126 Carrot
16. Rainbow Mix Carrot
17. Assorted Beet Mix
18. Sparkler White Tip Radish

### Alliums & Herbs
19. Cipollini Onion
20. Genovese Basil

### Perennials
21. UC-157 Asparagus (⚠️ Don't harvest for 2-3 years!)

## 📅 Key Dates for Akron, OH (Zone 6)

| Event | Date |
|-------|------|
| Last Frost | May 4, 2025 |
| First Fall Frost | October 11, 2025 |
| Growing Season | ~160 days |

## 🚀 Deployment to Cloudflare Pages

### Step 1: Create a GitHub Repository

1. Go to [github.com](https://github.com) and sign in
2. Click the **+** icon → **New repository**
3. Name it: `hundred-acre-garden`
4. Set to **Public** (required for free Cloudflare Pages)
5. Click **Create repository**

### Step 2: Upload Your Files

**Option A: Using GitHub Web Interface**
1. In your new repo, click **uploading an existing file**
2. Drag and drop `index.html` into the upload area
3. Add commit message: "Initial garden planner"
4. Click **Commit changes**

**Option B: Using Git Command Line**
```bash
# Clone your new repo
git clone https://github.com/YOUR_USERNAME/hundred-acre-garden.git
cd hundred-acre-garden

# Copy the index.html file to this folder
# Then commit and push
git add index.html
git commit -m "Initial garden planner"
git push origin main
```

### Step 3: Connect to Cloudflare Pages

1. Go to [dash.cloudflare.com](https://dash.cloudflare.com)
2. Sign in (or create a free account)
3. In the sidebar, click **Workers & Pages**
4. Click **Create application** → **Pages** → **Connect to Git**
5. Select **GitHub** and authorize Cloudflare
6. Select your `hundred-acre-garden` repository
7. Configure your build:
   - **Project name**: `hundred-acre-garden`
   - **Production branch**: `main`
   - **Build command**: (leave empty)
   - **Build output directory**: (leave empty or `/`)
8. Click **Save and Deploy**

### Step 4: Access Your Site

After deployment (usually 1-2 minutes):
- Your site will be live at: `https://hundred-acre-garden.pages.dev`
- Or a custom domain if you configure one

### Step 5: Enable Browser Notifications

When you first visit your site:
1. Your browser will ask for notification permission
2. Click **Allow** to receive planting reminders
3. Notifications work even when the tab is in the background!

## 🔧 Customization

### Changing the Last Frost Date
Edit line 140 in `index.html`:
```javascript
const LAST_FROST_DATE = new Date(2025, 4, 4); // Month is 0-indexed (4 = May)
```

### Adding New Plants
Add to the `INITIAL_PLANTS` array starting at line 163:
```javascript
{ 
    id: 22, // Unique ID
    name: "New Plant Name", 
    character: "pooh", // Character assignment
    type: "tomato", // Category for filtering
    startIndoors: -8, // Weeks before last frost (negative = before)
    transplant: 2, // Weeks after last frost
    // OR for direct sow:
    // directSow: 1, // Weeks after last frost
    daysToHarvest: 75,
    spacing: 18, // Inches apart
    notes: "Growing tips here",
    color: "#E53935" // Hex color for garden grid
}
```

### Changing Garden Dimensions
Edit lines 498-499 in the `GardenLayout` component:
```javascript
const GRID_COLS = 60; // Width in 6" units (60 = 30 feet)
const GRID_ROWS = 120; // Length in 6" units (120 = 60 feet)
```

## 💾 Data Storage

All data is stored in your browser's localStorage:
- `hundredAcreGarden_plants` - Plant status data
- `hundredAcreGarden_tasks` - Task completion status
- `hundredAcreGarden_grid` - Garden layout

To reset all data, open browser DevTools (F12) → Console → Run:
```javascript
localStorage.clear();
location.reload();
```

## 📱 Mobile Support

The app is fully responsive and works on:
- Desktop browsers
- Tablets
- Mobile phones

The garden grid may require scrolling on smaller screens.

## 🐛 Troubleshooting

### Notifications not working?
1. Check browser settings → Site permissions → Notifications
2. Make sure you clicked "Allow" when prompted
3. Some browsers block notifications in incognito/private mode

### Data disappeared?
- Data is stored per-browser. Different browsers = different data
- Clearing browser cache/cookies will delete saved data
- Data doesn't sync between devices

### Garden grid too small?
- Zoom out in your browser (Ctrl/Cmd + minus)
- Or use a larger screen

## 📄 License

This project is open source and available for personal use.

---

*"Sometimes the smallest things take up the most room in your heart."* - Winnie the Pooh

Happy Gardening! 🌻🍯🐝
