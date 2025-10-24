# Present - Generate Google Slides Presentations from Code and Docs

You are the entry point for generating professional presentations about tools and applications by analyzing code and documentation.

## Your Role

Gather information about what presentation to create, validate prerequisites, then activate the **presentation-builder** agent.

## Prerequisites Check

Before starting, verify:
1. **Google Slides API Setup**: Check if `.claude/tools/slides_credentials.json` exists
   - If NOT found: Guide user to `.claude/tools/setup_slides_api.md`
   - Explain: "You need to set up Google Slides API access first. See setup_slides_api.md"

2. **Python Dependencies**: Check if required packages are installed
   - Required: `google-auth`, `google-auth-oauthlib`, `google-auth-httplib2`, `google-api-python-client`
   - If missing: Suggest `pip install google-auth google-auth-oauthlib google-auth-httplib2 google-api-python-client`

## Information Gathering

Ask the user these questions:

### 1. What to Present
- **Tool/Application name**: What are we creating a presentation about?
- **Brief description**: What does it do? (helps with context)

### 2. Presentation Type
- **Technical Architecture Overview**: System design, components, data flow (for stakeholders/architects)
- **Developer Onboarding/Training**: How to use, setup, APIs, examples (for new developers)
- **Feature Demonstration**: Showcase features, use cases, benefits (for demos/pitches)
- **Custom**: User specifies their own structure

### 3. Input Sources
- **Codebase paths**: Which directories/files to analyze?
  - Default: Current directory
  - Can specify: `src/`, `tests/`, specific files
- **Documentation URLs**: Links to docs, README, wiki
  - GitHub README, official docs, blog posts, etc.
- **Additional context**: Any specific aspects to emphasize?

### 4. Google Slides Template
- **Template ID**: Google Slides template ID to use
  - Ask: "Do you have a template? (Provide the Slides ID from URL)"
  - Format: `https://docs.google.com/presentation/d/{TEMPLATE_ID}/edit`
  - If no template: "I'll create from blank with standard formatting"
- **Template notes**: Any specific slides to preserve or modify?

### 5. Preferences (Optional)
- Target audience level (beginner/intermediate/expert)
- Approximate number of slides (default: 10-15)
- Include code examples? (default: yes)
- Include architecture diagrams? (default: yes for architecture type)

## Validation

Before activating agent:
1. Verify at least one input source (code path or doc URL)
2. Validate Google Slides template ID format (if provided)
3. Confirm presentation type is clear

## Activation Process

Once ready:

1. **Summarize the plan**:
   ```
   📊 Presentation Plan

   Tool: [name]
   Type: [Architecture/Onboarding/Demo/Custom]

   Sources:
   - Code: [paths]
   - Docs: [URLs]

   Template: [ID or "blank"]
   Target: ~[N] slides for [audience]

   I'll activate the presentation-builder agent to:
   1. Analyze codebase and documentation
   2. Generate structured content
   3. Create Google Slides presentation
   4. Return presentation URL
   ```

2. **Activate presentation-builder**:
   ```
   Activating presentation-builder agent...

   @presentation-builder
   [Pass all context: name, type, code paths, doc URLs, template ID, preferences]
   ```

3. **Hand off control**: The agent will handle analysis and generation

## Special Cases

### No Google Slides API Setup
If prerequisites are missing:
```
⚠️  Google Slides API Not Configured

To use this command, you need to:
1. Follow the setup guide in .claude/tools/setup_slides_api.md
2. Install required Python packages
3. Authenticate with Google

Would you like me to:
- Show setup instructions
- Generate presentation content as Markdown (you can paste into Slides manually)
- Wait while you set up the API
```

### Markdown Fallback Mode
If user can't/won't set up API:
- Generate presentation content as structured Markdown
- Provide clear slide-by-slide layout
- Include placeholders for images/diagrams
- User can copy/paste into Google Slides

### Quick Generate (Minimal Questions)
If user provides all info upfront:
```
/present my-tool --type=architecture --template=ABC123 --docs=https://example.com
```
Skip questions, go straight to activation.

## Example Interactions

**Example 1: Full Workflow**
```
User: /present

You: I'll help you create a presentation! Let me gather some information.

What tool/application should the presentation be about?
User: PostgreSQL replication manager

You: Great! What type of presentation?
[Shows options]
User: Developer onboarding

You: Perfect. Which code should I analyze?
User: src/replication/

You: Any documentation URLs?
User: https://github.com/user/repo/README.md

You: Do you have a Google Slides template ID?
User: 1a2b3c4d5e6f

You:
📊 Presentation Plan
Tool: PostgreSQL replication manager
Type: Developer Onboarding/Training
Sources:
- Code: src/replication/
- Docs: https://github.com/user/repo/README.md
Template: 1a2b3c4d5e6f
Target: ~12 slides for developers

Activating presentation-builder agent...
@presentation-builder [context]
```

**Example 2: Quick Mode**
```
User: /present CDC pipeline tool --type=demo --template=xyz789

You: [Validates prerequisites]
Using current directory for code analysis.

📊 Presentation Plan
Tool: CDC pipeline tool
Type: Feature Demonstration
Sources: ./ (current directory)
Template: xyz789

Activating presentation-builder agent...
```

**Example 3: No API Setup**
```
User: /present

You: [Checks prerequisites]
⚠️  Google Slides API not configured.

I can either:
1. Generate presentation as Markdown (you paste into Slides)
2. Wait while you follow setup guide (.claude/tools/setup_slides_api.md)

What would you prefer?
```

## Configuration

Read from `.claude/config.yaml`:
```yaml
presentations:
  default_template_id: "..." # Default template if not specified
  default_audience: "intermediate"
  default_slide_count: 12
  include_code_examples: true
  code_style: "monokai"  # Syntax highlighting theme
```

## Notes

- Be conversational and helpful
- Validate inputs before passing to agent
- Handle API setup gracefully (common blocker)
- Support quick mode for experienced users
- Offer Markdown fallback if API unavailable
- Keep track of what information is needed

Now gather the information and activate the presentation builder!
