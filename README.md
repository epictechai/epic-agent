# Epic Tech AI

## Step-by-Step Guide to Deploy Epic Tech AI on GitHub Pages

### 1. Create a New Repository on GitHub
1. Go to [GitHub](https://github.com) and log in.
2. Click the **New** button to create a new repository.
3. Name the repository, for example, `epic-tech-ai`.
4. Optionally, add a description.
5. Choose **Public**.
6. Click **Create repository**.

### 2. Set Up the Project Locally
1. Clone the repository to your local machine:


bash git clone https://github.com/{your-username}/epic-tech-ai.git cd epic-tech-ai

2. Initialize a new React project with TypeScript:


bash npx create-react-app . --template typescript

3. Install the necessary dependencies:


bash npm install styled-components react-markdown prism-react-renderer

### 3. Create the Chat Component
1. Create a file named `Chat.tsx` in the `src` directory and paste the following code:


typescript import React, { useState, useCallback } from 'react'; import styled from 'styled-components'; import ReactMarkdown from 'react-markdown'; import { Prism as SyntaxHighlighter } from 'react-syntax-highlighter'; import { vscDarkPlus } from 'react-syntax-highlighter/dist/esm/styles/prism';

// Styled components for UI const ChatContainer = styled.div     display: flex;      flex-direction: column;      height: 100vh;      max-width: 800px;      margin: 0 auto;      padding: 20px;      background-color: #f4f4f4;   ;

const MessageList = styled.div     flex-grow: 1;      overflow-y: auto;      padding-bottom: 20px;   ;

const MessageBubble = styled.div<{ isUser?: boolean }>     background: ${props => props.isUser ? '#e0e0e0' : '#007bff'};      color: ${props => props.isUser ? '#000' : '#fff'};      border-radius: 20px;      padding: 10px 15px;      margin: 10px 0;      max-width: 70%;      align-self: ${props => props.isUser ? 'flex-end' : 'flex-start'};   ;

const InputForm = styled.form     display: flex;      margin-top: 20px;   ;

const Input = styled.input     flex-grow: 1;      padding: 10px;      border: 1px solid #ddd;      border-radius: 5px 0 0 5px;   ;

const SubmitButton = styled.button     padding: 10px 20px;      background-color: #007bff;      color: white;      border: none;      border-radius: 0 5px 5px 0;      cursor: pointer;   ;

// Markdown renderer with syntax highlighting const CodeBlock = ({ node, inline, className, children, ...props }) => { const match = /language-(\w+)/.exec(className || ''); return !inline && match ? ( <SyntaxHighlighter style={vscDarkPlus} language={match[1]} PreTag="div" {...props}> {String(children).replace(/\n$/, '')} </SyntaxHighlighter> ) : ( <code className={className} {...props}> {children} </code> ); };

const Chat = () => { const [messages, setMessages] = useState<{ text: string; isUser: boolean }[]>([]); const [input, setInput] = useState('');

 const handleSubmit = useCallback((e: React.FormEvent) => {
   e.preventDefault();
   if (input.trim()) {
     setMessages(prevMessages => [...prevMessages, { text: input, isUser: true }]);
     // Here you'd typically call an API to get Epic Tech AI's response
     // For this example, we'll simulate with a timeout
     setTimeout(() => {
       setMessages(prevMessages => [...prevMessages, {
         text: `Epic Tech AI: ${generateResponse(input)}`,
         isUser: false
       }]);
     }, 500);
     setInput('');
   }
 }, [input]);

 const generateResponse = (userMessage: string): string => {
   // This is a simple placeholder. In a real app, this would interact with Epic Tech AI's logic.
   if (userMessage.includes('implement')) {
     return `Here's how to implement that:\n\n\`\`\`javascript\n// Implementation code\n\`\`\``;
   } else if (userMessage.includes('best practice')) {
     return `Best practice involves:\n- Doing A\n- Doing B\n- Considering C`;
   }
   return "I'm Epic Tech AI, how can I assist you today?";
 };

 return (
   <ChatContainer>
     <MessageList>
       {messages.map((msg, index) => (
         <MessageBubble key={index} isUser={msg.isUser}>
           <ReactMarkdown components={{ code: CodeBlock }}>{msg.text}</ReactMarkdown>
         </MessageBubble>
       ))}
     </MessageList>
     <InputForm onSubmit={handleSubmit}>
       <Input 
         value={input} 
         onChange={(e) => setInput(e.target.value)} 
         placeholder="Type your message here..." 
       />
       <SubmitButton type="submit">Send</SubmitButton>
     </InputForm>
   </ChatContainer>
 );
};

export default Chat;

### 4. Use the Chat Component in Your App
1. Open `src/App.tsx` and replace its content with:


typescript import React from 'react'; import Chat from './Chat';

function App() { return ( <div className="App"> <Chat /> </div> ); }

export default App;

### 5. Set Up GitHub Pages Deployment
1. Install the `gh-pages` package:


bash npm install gh-pages --save-dev

2. Add the following scripts to your `package.json`:


json "scripts": { "predeploy": "npm run build", "deploy": "gh-pages -d build" }

3. Update the `homepage` field in `package.json` to point to your GitHub repository:


json "homepage": "http://{your-username}.github.io/{repository-name}"

Replace `{your-username}` with your GitHub username and `{repository-name}` with the name of your repository, for example:


json "homepage": "http://your-username.github.io/epic-tech-ai"

### 6. Deploy Your Application
1. Build and deploy your application:


bash npm run deploy

This command will build your React application and deploy it to the `gh-pages` branch of your repository.

2. Visit your deployed site:
   - Go to `http://{your-username}.github.io/{repository-name}` to see your deployed chat interface.

### Summary
By following these steps, you will have a fully functional chat interface deployed on GitHub Pages. Users will be able to interact with Epic Tech AI through the chat interface, and the responses will include markdown rendering and syntax highlighting for code blocks.


Replace {your-username} and {repository-name} with your GitHub username and the name of your repository, respectively. Save this content as README.md in the root of your project directory. This file will guide you and others on how to set up and deploy the project.
