### **The Importance of Organization in Infosec**
- Organization is essential for:
    - Client assessments.
    - CTFs (Capture The Flag challenges).
    - Labs and educational exercises.
- Clear documentation is a key skill, benefiting both infosec and other career paths.



### **Folder Structure**
- A well-organized folder structure helps track data during an assessment, such as scoping information, recon data, and evidence.
- **Sample Folder Structure**:
    ```
    Projects/
    └── Client Name
        ├── Assessment Type (e.g., EPT, IPT)
        │   ├── evidence
        │   │   ├── credentials
        │   │   ├── data
        │   │   └── screenshots
        │   ├── logs
        │   ├── scans
        │   ├── scope
        │   └── tools
    ```
    - **Subfolders**:
        - **Evidence**: Store credentials, data, screenshots, etc.
        - **Logs**: Output from tools or manual commands.
        - **Scans**: Results of automated scanning.
        - **Scope**: IP lists, domains, or network ranges in scope.
        - **Tools**: Specific utilities or scripts used during the assessment.
- Customize based on workflow:
    - Folder per target host.
    - Notes and screenshots integrated into a note-taking tool.



### **Note-Taking Tools**
- **Why It Matters**:
    - A technically skilled but disorganized tester may struggle.
    - Choose tools that fit your workflow.
- **Popular Tools**:
    - **Cherrytree**: Hierarchical note-taking.
    - **Visual Studio Code**: Versatile for notes and code.
    - **Notion/GitBook**: Rich features for Wiki-style pages and cheat sheets.
    - **Notepad++/Sublime Text**: Lightweight text editors.
    - **Evernote**: Cloud-based (caution: avoid storing sensitive client data on the cloud).



### **Best Practices for Note-Taking**
1. **Use Markdown**:
    - Easy to learn and visually appealing.
    - Useful for creating organized and readable notes.
2. **Maintain a Knowledge Base**:
    - Store:
        - Setup procedures for common assessments.
        - Cheat sheets for commands used in various phases.
        - Aggregated payloads, commands, and tips.
3. **Build Templates and Checklists**:
    - Report templates for different assessment types.
    - Findings/vulnerability database:
        - Include title, description, impact, remediation advice, and references.



### **Efficiency Tips**
- Aggregate useful commands and payloads from:
    - Labs
    - CTFs
    - Client assessments
- Use pre-prepared findings to speed up reporting.



### **Next Steps**
- Experiment with folder structures and note-taking tools to find your optimal workflow.
- Start early to develop strong habits.
- Use exercises, such as the **Nibbles walkthrough**, to practice documentation and refine your methods.
- Save useful commands and techniques into a common commands cheat sheet for future reference.