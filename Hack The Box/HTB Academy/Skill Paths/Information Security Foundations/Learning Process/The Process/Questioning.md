### Introduction
- **Asking the right questions is a crucial skill** in both technical and non-technical situations, helping guide decisions and actions.
- **Questions serve as orientation**, providing an overview to understand a situation and guide future steps.
- In cybersecurity and penetration testing, **finding the right question is more important and challenging than finding the right answer**.
- **Asking the right question** becomes difficult when we lack understanding of the topic, but it’s essential for solving complex problems.
- To improve, reflect on **3 to 5 situations** in your life where you were uncertain, and write down the questions you should have asked.
- This exercise helps identify **the difference between ineffective and effective questions**, aiding personal growth and problem-solving.



### Question States
- **There are no "good" or "bad" questions**; these labels are subjective and do not affect the outcome.
- **The question "What are 'good' questions?"** is not inherently "good" or "bad"—the answer remains the same regardless.
- Just as the **condition of water** (cold, hot, dark) doesn’t change the result of jumping into it, **the state of a question (good or bad)** doesn’t affect the answer.
- People assign labels like "good" or "bad" to questions based on the **expected benefits** of the answer, but these labels do not influence the result.
- Instead of "good" or "bad," questions can be categorized as **rough** or **precise**, which can affect the clarity of the answer.
- **Precision in questions** helps guide better answers, but still doesn’t make the question "good" or "bad."



### Questions in General
- **Questions are an integral part of everyday life**, with people asking 3-5 questions per minute on average, depending on the situation.
- **Questions drive the thinking and learning process** by connecting information in our minds and guiding our next steps.
- **Learning is hindered without questioning**, just like following a recipe without understanding the process.
- **Questions can be rough or precise**, but they are not inherently "good" or "bad"; instead, their quality affects the clarity of the answer.
- **The purpose of questions** is not always to acquire information but to guide decisions, actions, and understanding, sometimes challenging the traditional definition.
- **Three aspects shape our questions**: origin, process, and result/goal, which influence how we approach situations (e.g., past, present, future).
- **A question can be as simple as one word**, like "Why?" or "How?", which still qualifies as a legitimate question despite the official definition.
- **The official definition of a question** (to acquire information) is limited and does not always apply to situations like penetration testing, where the goal may not always be to gain direct information.



### Relationship-Oriented-Questioning Model
- To do this, we must consider what our questions have in common. 
- All our questions have a commonality: the `relationship` between the individual components. 
- So let us take a quick look at a model we have developed, which we call the `Relationship-Oriented-Questioning Model` (`ROQ`), and see how it looks and works.
![[Questioning1_png.png]]
- This model represents five components:
![[Screenshot_20241107_144203.png]]
- We need these components to be able to ask any question correctly.
- To do this, we ask any question we are interested in and break it down using the `ROQ` model. 
- Certain aspects must be considered with this model, as with all others.
	1. We need to find out the core element of the question and insert it as the object.
	2. We must have at least two components defined in the model. More than two components are optional.
- The good thing is that we always already have one component:
	- Our position in the question.
- So even for questions that do not directly concern us or about situations we are not involved in, we still have a position and view on the object. 
- So let us look at an example using the following question:
	- `What are all the methods available to remotely access Windows operating systems?`
- Once we have asked our question, we can break it down into its constituent parts in the `ROQ` model:
![[Questioning2_png.png]]
![[Screenshot_20241107_144329.png]]
- Based on the parts assigned to the components, we now have to define in which relationship they act among each other. 
- In the graphic, we see solid and dashed lines.
	- `Solid line`: Connection - How is X connected to Y?
	- `Dashed line`: Affection - How does Y influence the state of component X?
- #### Connecting the Components
	- With this, we can go through the individual relationships and establish them between the individual components. 
	- It is recommended to always start with the object, which in this case is the Windows operating system.
	- First, we need to establish and understand our position on the object.
		- What is the purpose for us to use Windows?
	- Mainly we use the operating system to use its functions to solve our tasks. We describe this as `Operating on`.
		- How does Windows influence our state in our position?
	- Windows is the most used operating system in the world and has the most compatibility and many user-friendly functions.
	- Therefore, we can also summarize this and call it `Provides functionality`.
![[Questioning3_png.png]]
- Now we can connect the relations between Windows and the methods we know.
	- What must Windows do or offer to be managed by remote access methods?
- A service must allow remote access over the Internet or network. 
- We know for sure `WinRM`, `Remote Desktop`, and a few more. (If not, it does not matter. We will learn about these in other modules).
- Otherwise, we would not be able to access it remotely. 
- We call this connection `Listening Service`.
- Next, the following question comes up:
	- How do the remote access methods affect Windows and thus change the state of Windows? What do these methods provide us with?
- Here the answer and the purpose are already in the description - these allow `Remote Access`.
![[Questioning4_png.png]]
- Now let us look at what we know about the known remote access methods.
	- What is the purpose of remote access methods?
- The purpose is to be able to manage Windows in different ways remotely. So all we do with it is to use it. So, therefore, we call this connection `Using`.
	- How do the different remote access methods that we know affect us?
- Apart from the different services these methods are designed for, they all have one thing in common. 
- They allow us to interact with Windows. Therefore we call this connection `Allow to interact with`.
![[Questioning5_png.png]]
- Since we already know some remote access methods, we know how they are connected to Windows. 
- Before Windows can be accessed remotely, the corresponding service must be running.
	- Which services must Windows have running to use methods unknown to us?
- We can not know this because the methods are unknown to us. Therefore we name it like this: `???`
- Now the same question arises again.
	- How do the remote access methods affect Windows and thus change the state of Windows? What do these methods offer us?
- The different methods offer different ways to access Windows. 
- Because the purpose of the methods, in this case, has not changed. 
- Therefore we call it again: `Remote Access`.
![[Questioning6_png.png]]
- Now that we know and understand the relationships between all the individual components, we know exactly what information we are missing and what we should focus on. 
- In this case, we can use `Windows services` to find the unknown remote access methods. 
- Therefore, if we look closely at all possible services that allow remote access, we can probably even find our own ways to use the service for remote access.
- The special thing about this model is that it is stackable.
- For example, if we have identified such Windows services and found unknown methods, the field `Unknown` becomes `Known` and would look like this:
![[Questioning7_png.png]]



### Practice
- **The model may feel unfamiliar initially**, but with practice, most people can apply it subconsciously after 5-10 repetitions.
- **After practicing**, you will naturally start using this model in conversations without much thought, leading to noticeable improvements.
- **With consistent practice**, you'll internalize the model, enabling automatic application in various situations.
- **Apply this model** to the 3-5 questions from earlier, and you'll be surprised by the insights it generates.
- **If the model doesn't work for a question**, rephrase it to make it more precise, as the `ROQ` model only works with questions that have clear answers.
- **The right question** is defined as: A precise question that helps establish relationships between components, enhances understanding, and brings you closer to the desired answer.