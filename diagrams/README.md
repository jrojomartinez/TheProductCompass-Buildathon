# CareerAgent Diagrams

## How to Use These Files

### Files in This Folder:
- `system_architecture.mmd` - System architecture diagram
- `workflow_sequence.mmd` - Sequence diagram showing agent workflow
- `agent_coordination.mmd` - Multi-agent coordination visualization
- `risk_buckets.md` - 4 Buckets of Risk matrix

### Converting to Images for Slides:

#### Method 1: Mermaid Live (Recommended - Fast & Easy)
1. Visit https://mermaid.live
2. Copy content from any `.mmd` file
3. Paste into left panel (renders automatically on right)
4. Click "Actions" → Download as PNG or SVG
5. Insert into your PowerPoint/Keynote/Google Slides

#### Method 2: Mermaid Chart (Most Professional)
1. Visit https://www.mermaidchart.com
2. Sign up for free account
3. Create new diagram and paste Mermaid code
4. Customize colors and styling
5. Export high-resolution images

#### Method 3: VS Code (If you use it)
1. Install "Markdown Preview Mermaid Support" extension
2. Open any `.mmd` file
3. Right-click → "Mermaid: Export Diagram"

#### Method 4: GitHub (Quick Preview)
1. Push these files to your repo
2. GitHub renders Mermaid automatically
3. Take screenshots for slides

## Color Scheme Used:

- **Scout Agent**: Green (#50C878)
- **Matcher Agent**: Orange (#FFB347)
- **Composer Agent**: Red (#FF6B6B)
- **Tracker Agent**: Purple (#9B59B6)
- **Database**: Dark Gray (#34495E)
- **Orchestrator**: Blue (#4A90E2)

## Tips for Slides:

1. **Use PNG with transparent background** for clean integration
2. **Size**: Export at least 1920x1080 for presentation quality
3. **Consistency**: Use the same color scheme across all slides
4. **Labels**: Ensure text is readable - may need to increase font sizes
5. **Simplify**: For slides, clarity > completeness

## Which Diagram for Which Slide:

- **Slide 4** (Solution Overview): Use `system_architecture.mmd`
- **Slide 9** (Multi-Agent Coordination): Use `workflow_sequence.mmd`
- **Slide 10** (4 Buckets of Risk): Use the table from `risk_buckets.md`
- **Slide 12** (Detailed Architecture): Use `agent_coordination.mmd`

## Need Help?

If diagrams need modifications, edit the `.mmd` files directly. Mermaid syntax is intuitive:
- `graph TB` = Top to Bottom flowchart
- `sequenceDiagram` = Sequence diagram
- `-->` = Arrow
- `subgraph` = Grouping

Documentation: https://mermaid.js.org/intro/
