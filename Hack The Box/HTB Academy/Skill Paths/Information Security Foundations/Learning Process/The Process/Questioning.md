### 1. **The Art of Asking Questions**
- **Purpose of Questions**:
    - To gather information, gain orientation, and guide decisions.
    - Questions serve as tools for understanding the situation and defining the next steps.
- **Key Insight in Cybersecurity**:
    - The most challenging part of problem-solving is asking the _right_ question, not finding the answer.



### 2. **Challenges in Questioning**
- It is easier to find answers when the question is precise.
- Asking the right question is especially difficult when:
    1. The concepts are not understood.
    2. There is little or no foundational knowledge in a particular area.
- **Example**:
	- **Rough Question**: "How can I hack X?"
	- **Precise Question**: "How can I use the server's SMB service to identify its existing user accounts?"
	- **Impact of Precision**:
	    - Precise questions yield actionable and meaningful results.



### 3. **Myth of Good vs. Bad Questions**
- There are no inherently "good" or "bad" questions.
    - States like "good" and "bad" are subjective and irrelevant to the result.
    - Example:
        - If an answer to a question is X, Y, Z, labeling the question as "good" or "bad" does not change the answer.
- **Relevant Question States**:
    - **Rough Questions**: Broad and general.
    - **Precise Questions**: Focused and specific, often leading to clearer results.



### 4. **Role of Questions in Thinking and Learning**
- Questions are central to the learning process as they create connections between information in the brain.
- **Questions as Recipes**:
    - Learning material = Ingredients.
    - Questions = Method of preparation.
    - The outcome depends on how well we ask and answer the questions.
- Simply copying answers or methods (e.g., recipes) does not guarantee success without personal application and practice.



### 5. **Practical Activity: Tracking Questions**
- Experiment: Set a timer for 1 minute and record every question that comes to mind.
    - Goal: To observe how frequently we question things in everyday situations.
    - Insight: Asking more questions helps develop a deeper understanding of complex topics.



### 6. **Short and Simple Questions**
- A question can be as short as a single word:
    - Examples: "Why?", "How?", "Where?"
    - These require context to make sense but remain valid questions.
- **Problem with the Official Definition of a Question**:
    - Definition: A sentence worded to elicit information.
    - Issue: Not all questions immediately yield information.
        - Example: “How is Host A connected to Host B?”
            - This question does not provide direct information without additional effort.
            - Therefore, the official definition is limited in scope.



### 7. **Revised Understanding of Questions**
- Questions do not always _obtain information_ directly.
- **New Goal of a Question**:
    - Rather than merely acquiring information, questions should aim to **clarify, explore, and guide** toward a result or deeper understanding.



### 8. **Core Components of Questions**
- Every question is built on three key elements:
1. **Origin**: Where the question stems from (e.g., curiosity, uncertainty).
2. **Process**: How the question is framed or expressed.
3. **Result/Goal**: The intended outcome of asking the question.



### 9. **Goals of Questions in Everyday Life**
- Questions can aim to:
1. **Understand the past**: Why did something happen?
2. **Explore the present**: How does this work?
3. **Predict the future**: What will happen if...?
- By aligning questions with clear goals, they become more effective tools for learning and problem-solving.



### 10. **Key Takeaways**
- To develop better skills in asking questions, focus on **precision** and align the question with the desired goal.
- Questions should clarify paths forward, deepen understanding, and facilitate action.


## Relationship-Oriented Model

### 1. **Purpose of ROQ Model**
- Designed to help formulate questions with clarity and precision.
- Focuses on understanding the **relationships** between components of a question to identify missing information and gaps in knowledge.



### 2. **Components of the ROQ Model**
- The model consists of **five components**:

| Component             | Description                                               |
| --------------------- | --------------------------------------------------------- |
| **Your Position**     | Your perspective or situation regarding the question.     |
| **The Object**        | The core element of the question; central to its meaning. |
| **Known**             | Information already known to you.                         |
| **Unknown**           | Information not yet known to you.                         |
| **Other Position(s)** | Perspective or situation of others involved (optional).   |



### 3. **Steps to Apply the ROQ Model**
1. **Identify Components**:
    - Break the question into its core elements and assign them to the ROQ model components.        
    - Example Question:  
        _"What are all the methods available to remotely access Windows operating systems?"_
    - Breakdown:
        |**Component**|**Question Part**|**Description**|
        |---|---|---|
        |**Your Position**|_(Implicit)_|Your viewpoint or purpose in using Windows.|
        |**The Object**|Windows|The central topic (core element).|
        |**Known**|Methods|Methods that are already known to you.|
        |**Unknown**|Methods|Methods you have yet to discover.|
        |**Other Positions**|_(None for now)_|Not applicable in this example.|
2. **Define Relationships**:
    - Establish **connections** (solid lines) and **influences** (dashed lines) between components:
        - **Solid Line (Connection)**: _How is X connected to Y?_
        - **Dashed Line (Affection)**: _How does Y affect the state of X?_
3. **Example Relationships** (for the question above):
    - **Your Position ↔ Windows**:
        - _What is the purpose of using Windows?_
            - Answer: To use its functions to solve tasks. (We describe this as **Operating on**.)
    - **Windows ↔ Known Methods**:
        - _What must Windows do to be managed by remote access methods?_
            - Answer: Run a service that allows remote access. Example: WinRM, Remote Desktop. (We call this connection **Listening Service**.)
    - **Known Methods ↔ Your Position**:
        - _How do known remote access methods affect us?_
            - Answer: They allow interaction with Windows. (We call this connection **Allow to interact with**.)
    - **Windows ↔ Unknown Methods**:
        - _Which services must Windows have running to use unknown methods?_
            - Answer: Information is missing. (We label this connection as **???**.)
        - _How do unknown methods affect Windows?_
            - Answer: They still enable **Remote Access** (same purpose).



### 4. **Benefits of the ROQ Model**
- **Clarifies Missing Information**:
    - Once relationships are mapped, it’s clear what is **unknown** and where to focus research.
    - Example: Identifying Windows services that allow remote access helps uncover unknown methods.
- **Stackable Structure**:
    - The model is iterative. Once new information is discovered, **Unknown** becomes **Known**, enabling further questioning.
    - Example Progression:
        - After discovering new remote access methods, update the **Unknown** field and continue exploring their impact.



### 5. **Practical Application**
- **Scenario**:
	- Question: _"How can I use the server's SMB service to identify its existing user accounts?"_
- **ROQ Breakdown**:
    |**Component**|**Question Part**|**Description**|
    |---|---|---|
    |**Your Position**|Penetration Tester|Your role or purpose.|
    |**The Object**|SMB Service|Core element of the question.|
    |**Known**|SMB Service Exists|You know the service is running.|
    |**Unknown**|User Account Enumeration Method|You need to discover how to enumerate users.|
    |**Other Positions**|_(None)_|Not applicable in this case.|
- **Relationships**:
    - **SMB ↔ Your Position**: Allows file sharing or communication.
    - **SMB ↔ Known Methods**: Tools like `smbclient` or `enum4linux` interact with SMB.
    - **SMB ↔ Unknown Methods**: How to enumerate accounts using this service (focus area).



### 6. **Key Takeaway**
- The ROQ Model helps to systematically:
    1. Deconstruct questions into manageable components.
    2. Define relationships between known and unknown elements.
    3. Identify where to focus efforts to fill knowledge gaps and reach the desired goal.



### **Practicing the ROQ Model**



### 1. **Practice Makes Perfect**
- **Initial Difficulty**:
    - It’s normal to struggle with applying the ROQ model at first.
    - With practice (5–10 applications), the model becomes intuitive and automatic, even during conversations.
- **Practice Goal**:
    - To internalize the model for clearer and more precise questioning.
    - Once internalized, it becomes second nature to break down complex questions and understand their relationships.



### 2. **Steps for Practice**
1. **Start with Your Questions**:
    - Use the **3 to 5 questions** you previously wrote down from real-life situations.
    - Apply the ROQ model to each question:
        - Break the question into the five components:
            - **Your Position**
            - **The Object**
            - **Known**
            - **Unknown**
            - **Other Position(s)**
        - Define the relationships (connections and affections) between components.
2. **Evaluate Results**:
    - Identify gaps in knowledge and what relationships are missing.
    - Use the insights gained to clarify or refine your understanding.
3. **Refine the Question**:
    - If the model does not work for a particular question, **rephrase the question** to make it more precise.
    - Precision ensures the relationships between components are clear and actionable.



### 3. **Key Insight: What is a Right Question?**
- **Definition**:
    - A **right question** is a precise question that:
        - Establishes relationships between the components.
        - Helps you understand the problem.
        - Brings you closer to the required answer.
- **Precision = Clarity**:
    - If your question lacks clarity or specificity, it will not yield actionable results.



### 4. **Special Feature of the ROQ Model**
- The model **rejects imprecise questions**:
    - If the question cannot be broken down or applied to the ROQ framework, it indicates the need for rephrasing.
    - This ensures every question leads to a clear path forward.



### 5. **Final Practice Task**
- **Apply the Model**:
    - Take the questions you’ve written down:
        1. Break them into components.
        2. Map the relationships between known and unknown parts.
        3. Rephrase if needed for precision.
- **Reflect**:
    - Observe how using the model clarifies your thoughts and highlights missing information.
    - Notice how it guides you toward better, more actionable answers.



### 6. **Key Takeaway**
- A **precise, relationship-oriented question** is the foundation of effective problem-solving.
- The ROQ model helps you frame your questions systematically, ensuring clarity and actionable results.