# SafChat Component

## Overview

SafChat is a comprehensive chat interface component designed for real-time messaging and communication features. It provides a complete chat experience with message bubbles, typing indicators, emoji support, file sharing, message reactions, and thread management. The component is ideal for customer support interfaces, team collaboration tools, client communication portals, and any application requiring interactive messaging capabilities.

## React API

### SafChat

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `messages` | `ChatMessage[]` | Yes | - | Array of chat messages to display |
| `currentUser` | `ChatUser` | Yes | - | Current logged-in user information |
| `participants` | `ChatUser[]` | No | `[]` | List of chat participants |
| `variant` | `'default' \| 'compact' \| 'minimal' \| 'threaded'` | No | `'default'` | Chat interface layout variant |
| `showTypingIndicator` | `boolean` | No | `true` | Whether to show typing indicators |
| `showTimestamps` | `boolean` | No | `true` | Whether to show message timestamps |
| `showAvatars` | `boolean` | No | `true` | Whether to show user avatars |
| `showUserNames` | `boolean` | No | `true` | Whether to show user names |
| `enableEmoji` | `boolean` | No | `true` | Enable emoji picker and reactions |
| `enableFileUpload` | `boolean` | No | `true` | Enable file sharing |
| `enableMarkdown` | `boolean` | No | `false` | Enable markdown formatting |
| `enableThreads` | `boolean` | No | `false` | Enable message threading |
| `enableReactions` | `boolean` | No | `true` | Enable message reactions |
| `enableSearch` | `boolean` | No | `false` | Enable message search |
| `maxMessageLength` | `number` | No | `2000` | Maximum characters per message |
| `autoScroll` | `boolean` | No | `true` | Auto-scroll to new messages |
| `placeholder` | `string` | No | `'Type a message...'` | Input placeholder text |
| `typingUsers` | `ChatUser[]` | No | `[]` | Users currently typing |
| `onlineUsers` | `ChatUser[]` | No | `[]` | Currently online users |
| `height` | `string \| number` | No | `'400px'` | Chat container height |
| `loading` | `boolean` | No | `false` | Whether chat is loading |
| `disabled` | `boolean` | No | `false` | Whether chat input is disabled |
| `onSendMessage` | `(message: string, attachments?: File[]) => void \| Promise<void>` | No | - | Callback when message is sent |
| `onTyping` | `(isTyping: boolean) => void` | No | - | Callback when user types |
| `onReaction` | `(messageId: string, emoji: string) => void` | No | - | Callback when reaction is added |
| `onFileUpload` | `(files: File[]) => void \| Promise<void>` | No | - | Callback for file uploads |
| `onMessageEdit` | `(messageId: string, newContent: string) => void` | No | - | Callback when message is edited |
| `onMessageDelete` | `(messageId: string) => void` | No | - | Callback when message is deleted |
| `onThreadCreate` | `(parentMessageId: string) => void` | No | - | Callback when thread is created |
| `onLoadMore` | `() => void \| Promise<void>` | No | - | Callback to load older messages |
| `className` | `string` | No | - | Additional CSS classes |
| `testId` | `string` | No | - | Test identifier |

### ChatMessage Interface

```typescript
interface ChatMessage {
  id: string;
  content: string;
  user: ChatUser;
  timestamp: Date | string;
  type?: 'text' | 'file' | 'image' | 'system' | 'typing';
  edited?: boolean;
  editedAt?: Date | string;
  attachments?: ChatAttachment[];
  reactions?: ChatReaction[];
  parentId?: string; // For threaded messages
  threadCount?: number;
  metadata?: { [key: string]: any };
  status?: 'sending' | 'sent' | 'delivered' | 'read' | 'failed';
}

interface ChatUser {
  id: string;
  name: string;
  avatar?: string;
  role?: string;
  status?: 'online' | 'offline' | 'away' | 'busy';
  isCurrentUser?: boolean;
}

interface ChatAttachment {
  id: string;
  name: string;
  url: string;
  type: string;
  size: number;
  thumbnail?: string;
}

interface ChatReaction {
  emoji: string;
  users: ChatUser[];
  count: number;
}
```

## Angular API

### saf-chat

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `[messages]` | `ChatMessage[]` | Yes | - | Array of chat messages to display |
| `[currentUser]` | `ChatUser` | Yes | - | Current logged-in user information |
| `[participants]` | `ChatUser[]` | No | `[]` | List of chat participants |
| `[variant]` | `'default' \| 'compact' \| 'minimal' \| 'threaded'` | No | `'default'` | Chat interface layout variant |
| `[showTypingIndicator]` | `boolean` | No | `true` | Whether to show typing indicators |
| `[showTimestamps]` | `boolean` | No | `true` | Whether to show message timestamps |
| `[showAvatars]` | `boolean` | No | `true` | Whether to show user avatars |
| `[showUserNames]` | `boolean` | No | `true` | Whether to show user names |
| `[enableEmoji]` | `boolean` | No | `true` | Enable emoji picker and reactions |
| `[enableFileUpload]` | `boolean` | No | `true` | Enable file sharing |
| `[enableMarkdown]` | `boolean` | No | `false` | Enable markdown formatting |
| `[enableThreads]` | `boolean` | No | `false` | Enable message threading |
| `[enableReactions]` | `boolean` | No | `true` | Enable message reactions |
| `[enableSearch]` | `boolean` | No | `false` | Enable message search |
| `[maxMessageLength]` | `number` | No | `2000` | Maximum characters per message |
| `[autoScroll]` | `boolean` | No | `true` | Auto-scroll to new messages |
| `[placeholder]` | `string` | No | `'Type a message...'` | Input placeholder text |
| `[typingUsers]` | `ChatUser[]` | No | `[]` | Users currently typing |
| `[onlineUsers]` | `ChatUser[]` | No | `[]` | Currently online users |
| `[height]` | `string \| number` | No | `'400px'` | Chat container height |
| `[loading]` | `boolean` | No | `false` | Whether chat is loading |
| `[disabled]` | `boolean` | No | `false` | Whether chat input is disabled |
| `(sendMessage)` | `EventEmitter<{message: string, attachments?: File[]}>` | No | - | Event when message is sent |
| `(typing)` | `EventEmitter<boolean>` | No | - | Event when user types |
| `(reaction)` | `EventEmitter<{messageId: string, emoji: string}>` | No | - | Event when reaction is added |
| `(fileUpload)` | `EventEmitter<File[]>` | No | - | Event for file uploads |
| `(messageEdit)` | `EventEmitter<{messageId: string, newContent: string}>` | No | - | Event when message is edited |
| `(messageDelete)` | `EventEmitter<string>` | No | - | Event when message is deleted |
| `(threadCreate)` | `EventEmitter<string>` | No | - | Event when thread is created |
| `(loadMore)` | `EventEmitter<void>` | No | - | Event to load older messages |

## Usage Examples

### Legal Client Support Chat

#### React
```jsx
import { SafChat, SafIcon, SafAvatar, SafBadge } from '@saffron/react';
import { useState, useEffect, useRef } from 'react';

const LegalClientSupportChat = () => {
  const [messages, setMessages] = useState([]);
  const [typingUsers, setTypingUsers] = useState([]);
  const [onlineUsers, setOnlineUsers] = useState([]);
  const [chatLoading, setChatLoading] = useState(false);
  const typingTimeoutRef = useRef(null);

  // Current user (client)
  const currentUser = {
    id: 'client-001',
    name: 'Sarah Thompson',
    avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=sarah',
    role: 'Client',
    status: 'online',
    isCurrentUser: true
  };

  // Support team members
  const supportTeam = [
    {
      id: 'lawyer-001',
      name: 'David Martinez',
      avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=david',
      role: 'Senior Associate',
      status: 'online'
    },
    {
      id: 'paralegal-001',
      name: 'Emma Chen',
      avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=emma',
      role: 'Paralegal',
      status: 'online'
    },
    {
      id: 'support-001',
      name: 'Legal Support Bot',
      avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=bot',
      role: 'AI Assistant',
      status: 'online'
    }
  ];

  // Sample chat messages
  const initialMessages = [
    {
      id: 'msg-1',
      content: 'Hello Sarah! I\'m David Martinez from Thomson Reuters Legal. I\'ll be assisting you with your contract review today.',
      user: supportTeam[0],
      timestamp: new Date(Date.now() - 900000), // 15 minutes ago
      type: 'text',
      status: 'read'
    },
    {
      id: 'msg-2',
      content: 'Hi David! Thank you for reaching out. I have some questions about the merger agreement draft we received.',
      user: currentUser,
      timestamp: new Date(Date.now() - 870000),
      type: 'text',
      status: 'read'
    },
    {
      id: 'msg-3',
      content: 'Of course! I\'d be happy to help. Could you please share the specific sections you\'d like me to review?',
      user: supportTeam[0],
      timestamp: new Date(Date.now() - 840000),
      type: 'text',
      status: 'read',
      reactions: [
        { emoji: '👍', users: [currentUser], count: 1 }
      ]
    },
    {
      id: 'msg-4',
      content: 'Here\'s the merger agreement draft. I\'m particularly concerned about Section 7.3 regarding intellectual property transfer.',
      user: currentUser,
      timestamp: new Date(Date.now() - 810000),
      type: 'file',
      status: 'read',
      attachments: [
        {
          id: 'file-1',
          name: 'Merger_Agreement_Draft_v2.1.pdf',
          url: '/files/merger-agreement.pdf',
          type: 'application/pdf',
          size: 2458944,
          thumbnail: '/thumbnails/pdf-icon.png'
        }
      ]
    },
    {
      id: 'msg-5',
      content: 'I\'ve reviewed Section 7.3. There are a few areas that need clarification regarding IP warranties and indemnification. Let me provide detailed feedback.',
      user: supportTeam[0],
      timestamp: new Date(Date.now() - 600000), // 10 minutes ago
      type: 'text',
      status: 'read'
    },
    {
      id: 'msg-6',
      content: 'I can also help with initial document analysis using our AI review tools if needed.',
      user: supportTeam[2], // Bot
      timestamp: new Date(Date.now() - 580000),
      type: 'text',
      status: 'read'
    }
  ];

  useEffect(() => {
    setMessages(initialMessages);
    setOnlineUsers([...supportTeam, currentUser]);
  }, []);

  const handleSendMessage = async (message, attachments) => {
    const newMessage = {
      id: `msg-${Date.now()}`,
      content: message,
      user: currentUser,
      timestamp: new Date(),
      type: attachments && attachments.length > 0 ? 'file' : 'text',
      status: 'sending',
      attachments: attachments ? attachments.map((file, index) => ({
        id: `file-${Date.now()}-${index}`,
        name: file.name,
        url: URL.createObjectURL(file),
        type: file.type,
        size: file.size
      })) : undefined
    };

    setMessages(prev => [...prev, newMessage]);

    // Simulate message sending delay
    setTimeout(() => {
      setMessages(prev => 
        prev.map(msg => 
          msg.id === newMessage.id 
            ? { ...msg, status: 'delivered' }
            : msg
        )
      );

      // Simulate lawyer response after a delay
      setTimeout(() => {
        const response = {
          id: `msg-response-${Date.now()}`,
          content: 'Thank you for that information. I\'ll review this and get back to you within the hour with detailed feedback.',
          user: supportTeam[0],
          timestamp: new Date(),
          type: 'text',
          status: 'sent'
        };
        setMessages(prev => [...prev, response]);
      }, 2000);
    }, 1000);
  };

  const handleTyping = (isTyping) => {
    if (isTyping) {
      // Clear any existing timeout
      if (typingTimeoutRef.current) {
        clearTimeout(typingTimeoutRef.current);
      }

      // Simulate other users seeing typing indicator
      console.log('User is typing...');

      // Auto-stop typing after 3 seconds of inactivity
      typingTimeoutRef.current = setTimeout(() => {
        console.log('User stopped typing');
      }, 3000);
    }
  };

  const handleReaction = (messageId, emoji) => {
    setMessages(prev => 
      prev.map(msg => {
        if (msg.id === messageId) {
          const existingReactions = msg.reactions || [];
          const existingReaction = existingReactions.find(r => r.emoji === emoji);
          
          if (existingReaction) {
            // Toggle reaction
            const userAlreadyReacted = existingReaction.users.some(u => u.id === currentUser.id);
            if (userAlreadyReacted) {
              // Remove reaction
              return {
                ...msg,
                reactions: existingReactions.map(r => 
                  r.emoji === emoji 
                    ? {
                        ...r,
                        users: r.users.filter(u => u.id !== currentUser.id),
                        count: r.count - 1
                      }
                    : r
                ).filter(r => r.count > 0)
              };
            } else {
              // Add reaction
              return {
                ...msg,
                reactions: existingReactions.map(r => 
                  r.emoji === emoji 
                    ? {
                        ...r,
                        users: [...r.users, currentUser],
                        count: r.count + 1
                      }
                    : r
                )
              };
            }
          } else {
            // New reaction
            return {
              ...msg,
              reactions: [
                ...existingReactions,
                {
                  emoji,
                  users: [currentUser],
                  count: 1
                }
              ]
            };
          }
        }
        return msg;
      })
    );
  };

  const handleFileUpload = async (files) => {
    console.log('Files uploaded:', files);
    // Handle file upload logic
  };

  const handleMessageEdit = (messageId, newContent) => {
    setMessages(prev => 
      prev.map(msg => 
        msg.id === messageId 
          ? { 
              ...msg, 
              content: newContent, 
              edited: true, 
              editedAt: new Date() 
            }
          : msg
      )
    );
  };

  const handleMessageDelete = (messageId) => {
    setMessages(prev => prev.filter(msg => msg.id !== messageId));
  };

  const handleLoadMore = async () => {
    setChatLoading(true);
    // Simulate loading older messages
    await new Promise(resolve => setTimeout(resolve, 1000));
    
    const olderMessages = [
      {
        id: 'msg-old-1',
        content: 'Welcome to Thomson Reuters Legal Support. How can we assist you today?',
        user: supportTeam[2],
        timestamp: new Date(Date.now() - 1800000), // 30 minutes ago
        type: 'text',
        status: 'read'
      }
    ];
    
    setMessages(prev => [...olderMessages, ...prev]);
    setChatLoading(false);
  };

  // Simulate typing users
  useEffect(() => {
    const interval = setInterval(() => {
      // Randomly show/hide typing indicator
      if (Math.random() > 0.8) {
        setTypingUsers([supportTeam[0]]);
        setTimeout(() => setTypingUsers([]), 2000);
      }
    }, 10000);

    return () => clearInterval(interval);
  }, []);

  return (
    <div className="legal-client-support-demo">
      <h2>Legal Client Support Chat</h2>

      <div className="chat-variants">
        {/* Main Support Chat */}
        <div className="chat-section">
          <div className="chat-header">
            <h3>Contract Review Consultation</h3>
            <div className="participants-info">
              <SafBadge variant="success" size="small">
                {onlineUsers.length} online
              </SafBadge>
              <div className="participant-avatars">
                {onlineUsers.slice(0, 3).map(user => (
                  <SafAvatar
                    key={user.id}
                    src={user.avatar}
                    name={user.name}
                    size="small"
                    status={user.status}
                  />
                ))}
              </div>
            </div>
          </div>

          <SafChat
            messages={messages}
            currentUser={currentUser}
            participants={[...supportTeam, currentUser]}
            variant="default"
            height="500px"
            showTypingIndicator={true}
            showTimestamps={true}
            showAvatars={true}
            showUserNames={true}
            enableEmoji={true}
            enableFileUpload={true}
            enableReactions={true}
            typingUsers={typingUsers}
            onlineUsers={onlineUsers}
            placeholder="Ask about your legal matter..."
            loading={chatLoading}
            onSendMessage={handleSendMessage}
            onTyping={handleTyping}
            onReaction={handleReaction}
            onFileUpload={handleFileUpload}
            onMessageEdit={handleMessageEdit}
            onMessageDelete={handleMessageDelete}
            onLoadMore={handleLoadMore}
          />
        </div>

        {/* Compact Support Chat */}
        <div className="chat-section">
          <h3>Quick Questions (Compact View)</h3>
          
          <SafChat
            messages={messages.slice(-3)} // Show only recent messages
            currentUser={currentUser}
            participants={supportTeam}
            variant="compact"
            height="300px"
            showTimestamps={false}
            showAvatars={true}
            showUserNames={false}
            enableEmoji={false}
            enableFileUpload={false}
            enableReactions={false}
            placeholder="Quick question..."
            onSendMessage={handleSendMessage}
          />
        </div>

        {/* Threaded Discussion */}
        <div className="chat-section">
          <h3>Threaded Legal Discussion</h3>
          
          <SafChat
            messages={messages}
            currentUser={currentUser}
            participants={supportTeam}
            variant="threaded"
            height="400px"
            enableThreads={true}
            enableMarkdown={true}
            enableSearch={true}
            showTimestamps={true}
            showAvatars={true}
            placeholder="Discuss legal topics..."
            onSendMessage={handleSendMessage}
            onThreadCreate={(parentId) => console.log('Thread created for:', parentId)}
          />
        </div>
      </div>

      {/* Chat Features Demo */}
      <div className="features-demo">
        <h3>Advanced Chat Features</h3>
        
        <div className="feature-grid">
          <div className="feature-item">
            <SafIcon name="paperclip" />
            <h4>File Sharing</h4>
            <p>Share documents, images, and attachments</p>
          </div>
          
          <div className="feature-item">
            <SafIcon name="smile" />
            <h4>Emoji Reactions</h4>
            <p>React to messages with emojis</p>
          </div>
          
          <div className="feature-item">
            <SafIcon name="edit" />
            <h4>Message Editing</h4>
            <p>Edit and delete your messages</p>
          </div>
          
          <div className="feature-item">
            <SafIcon name="message-square" />
            <h4>Message Threading</h4>
            <p>Create threaded discussions</p>
          </div>
          
          <div className="feature-item">
            <SafIcon name="search" />
            <h4>Message Search</h4>
            <p>Search through chat history</p>
          </div>
          
          <div className="feature-item">
            <SafIcon name="eye" />
            <h4>Read Receipts</h4>
            <p>See when messages are read</p>
          </div>
        </div>
      </div>
    </div>
  );
};
```

#### Angular
```typescript
// legal-client-support-chat.component.ts
import { Component, OnInit, OnDestroy } from '@angular/core';

interface ChatMessage {
  id: string;
  content: string;
  user: ChatUser;
  timestamp: Date;
  type?: 'text' | 'file' | 'image' | 'system';
  edited?: boolean;
  editedAt?: Date;
  attachments?: ChatAttachment[];
  reactions?: ChatReaction[];
  status?: 'sending' | 'sent' | 'delivered' | 'read' | 'failed';
}

interface ChatUser {
  id: string;
  name: string;
  avatar?: string;
  role?: string;
  status?: 'online' | 'offline' | 'away' | 'busy';
  isCurrentUser?: boolean;
}

interface ChatAttachment {
  id: string;
  name: string;
  url: string;
  type: string;
  size: number;
  thumbnail?: string;
}

interface ChatReaction {
  emoji: string;
  users: ChatUser[];
  count: number;
}

@Component({
  selector: 'app-legal-client-support-chat',
  template: `
    <div class="legal-client-support-demo">
      <h2>Legal Client Support Chat</h2>

      <div class="chat-variants">
        <!-- Main Support Chat -->
        <div class="chat-section">
          <div class="chat-header">
            <h3>Contract Review Consultation</h3>
            <div class="participants-info">
              <saf-badge variant="success" size="small">
                {{ onlineUsers.length }} online
              </saf-badge>
              <div class="participant-avatars">
                <saf-avatar
                  *ngFor="let user of onlineUsers.slice(0, 3)"
                  [src]="user.avatar"
                  [name]="user.name"
                  size="small"
                  [status]="user.status">
                </saf-avatar>
              </div>
            </div>
          </div>

          <saf-chat
            [messages]="messages"
            [currentUser]="currentUser"
            [participants]="allParticipants"
            variant="default"
            height="500px"
            [showTypingIndicator]="true"
            [showTimestamps]="true"
            [showAvatars]="true"
            [showUserNames]="true"
            [enableEmoji]="true"
            [enableFileUpload]="true"
            [enableReactions]="true"
            [typingUsers]="typingUsers"
            [onlineUsers]="onlineUsers"
            placeholder="Ask about your legal matter..."
            [loading]="chatLoading"
            (sendMessage)="handleSendMessage($event.message, $event.attachments)"
            (typing)="handleTyping($event)"
            (reaction)="handleReaction($event.messageId, $event.emoji)"
            (fileUpload)="handleFileUpload($event)"
            (messageEdit)="handleMessageEdit($event.messageId, $event.newContent)"
            (messageDelete)="handleMessageDelete($event)"
            (loadMore)="handleLoadMore()">
          </saf-chat>
        </div>

        <!-- Compact Support Chat -->
        <div class="chat-section">
          <h3>Quick Questions (Compact View)</h3>
          
          <saf-chat
            [messages]="recentMessages"
            [currentUser]="currentUser"
            [participants]="supportTeam"
            variant="compact"
            height="300px"
            [showTimestamps]="false"
            [showAvatars]="true"
            [showUserNames]="false"
            [enableEmoji]="false"
            [enableFileUpload]="false"
            [enableReactions]="false"
            placeholder="Quick question..."
            (sendMessage)="handleSendMessage($event.message, $event.attachments)">
          </saf-chat>
        </div>

        <!-- Threaded Discussion -->
        <div class="chat-section">
          <h3>Threaded Legal Discussion</h3>
          
          <saf-chat
            [messages]="messages"
            [currentUser]="currentUser"
            [participants]="supportTeam"
            variant="threaded"
            height="400px"
            [enableThreads]="true"
            [enableMarkdown]="true"
            [enableSearch]="true"
            [showTimestamps]="true"
            [showAvatars]="true"
            placeholder="Discuss legal topics..."
            (sendMessage)="handleSendMessage($event.message, $event.attachments)"
            (threadCreate)="handleThreadCreate($event)">
          </saf-chat>
        </div>
      </div>

      <!-- Chat Features Demo -->
      <div class="features-demo">
        <h3>Advanced Chat Features</h3>
        
        <div class="feature-grid">
          <div class="feature-item">
            <saf-icon name="paperclip"></saf-icon>
            <h4>File Sharing</h4>
            <p>Share documents, images, and attachments</p>
          </div>
          
          <div class="feature-item">
            <saf-icon name="smile"></saf-icon>
            <h4>Emoji Reactions</h4>
            <p>React to messages with emojis</p>
          </div>
          
          <div class="feature-item">
            <saf-icon name="edit"></saf-icon>
            <h4>Message Editing</h4>
            <p>Edit and delete your messages</p>
          </div>
          
          <div class="feature-item">
            <saf-icon name="message-square"></saf-icon>
            <h4>Message Threading</h4>
            <p>Create threaded discussions</p>
          </div>
          
          <div class="feature-item">
            <saf-icon name="search"></saf-icon>
            <h4>Message Search</h4>
            <p>Search through chat history</p>
          </div>
          
          <div class="feature-item">
            <saf-icon name="eye"></saf-icon>
            <h4>Read Receipts</h4>
            <p>See when messages are read</p>
          </div>
        </div>
      </div>
    </div>
  `
})
export class LegalClientSupportChatComponent implements OnInit, OnDestroy {
  messages: ChatMessage[] = [];
  typingUsers: ChatUser[] = [];
  onlineUsers: ChatUser[] = [];
  chatLoading = false;
  private typingTimeout: any;
  private typingInterval: any;

  // Current user (client)
  currentUser: ChatUser = {
    id: 'client-001',
    name: 'Sarah Thompson',
    avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=sarah',
    role: 'Client',
    status: 'online',
    isCurrentUser: true
  };

  // Support team members
  supportTeam: ChatUser[] = [
    {
      id: 'lawyer-001',
      name: 'David Martinez',
      avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=david',
      role: 'Senior Associate',
      status: 'online'
    },
    {
      id: 'paralegal-001',
      name: 'Emma Chen',
      avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=emma',
      role: 'Paralegal',
      status: 'online'
    },
    {
      id: 'support-001',
      name: 'Legal Support Bot',
      avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=bot',
      role: 'AI Assistant',
      status: 'online'
    }
  ];

  get allParticipants(): ChatUser[] {
    return [...this.supportTeam, this.currentUser];
  }

  get recentMessages(): ChatMessage[] {
    return this.messages.slice(-3);
  }

  ngOnInit() {
    this.loadInitialMessages();
    this.onlineUsers = [...this.supportTeam, this.currentUser];
    this.startTypingSimulation();
  }

  ngOnDestroy() {
    if (this.typingTimeout) {
      clearTimeout(this.typingTimeout);
    }
    if (this.typingInterval) {
      clearInterval(this.typingInterval);
    }
  }

  loadInitialMessages() {
    this.messages = [
      {
        id: 'msg-1',
        content: 'Hello Sarah! I\'m David Martinez from Thomson Reuters Legal. I\'ll be assisting you with your contract review today.',
        user: this.supportTeam[0],
        timestamp: new Date(Date.now() - 900000),
        type: 'text',
        status: 'read'
      },
      {
        id: 'msg-2',
        content: 'Hi David! Thank you for reaching out. I have some questions about the merger agreement draft we received.',
        user: this.currentUser,
        timestamp: new Date(Date.now() - 870000),
        type: 'text',
        status: 'read'
      },
      {
        id: 'msg-3',
        content: 'Of course! I\'d be happy to help. Could you please share the specific sections you\'d like me to review?',
        user: this.supportTeam[0],
        timestamp: new Date(Date.now() - 840000),
        type: 'text',
        status: 'read',
        reactions: [
          { emoji: '👍', users: [this.currentUser], count: 1 }
        ]
      }
    ];
  }

  async handleSendMessage(message: string, attachments?: File[]) {
    const newMessage: ChatMessage = {
      id: `msg-${Date.now()}`,
      content: message,
      user: this.currentUser,
      timestamp: new Date(),
      type: attachments && attachments.length > 0 ? 'file' : 'text',
      status: 'sending',
      attachments: attachments ? attachments.map((file, index) => ({
        id: `file-${Date.now()}-${index}`,
        name: file.name,
        url: URL.createObjectURL(file),
        type: file.type,
        size: file.size
      })) : undefined
    };

    this.messages = [...this.messages, newMessage];

    // Simulate message sending
    setTimeout(() => {
      this.messages = this.messages.map(msg => 
        msg.id === newMessage.id 
          ? { ...msg, status: 'delivered' }
          : msg
      );

      // Simulate response
      setTimeout(() => {
        const response: ChatMessage = {
          id: `msg-response-${Date.now()}`,
          content: 'Thank you for that information. I\'ll review this and get back to you within the hour with detailed feedback.',
          user: this.supportTeam[0],
          timestamp: new Date(),
          type: 'text',
          status: 'sent'
        };
        this.messages = [...this.messages, response];
      }, 2000);
    }, 1000);
  }

  handleTyping(isTyping: boolean) {
    if (isTyping) {
      if (this.typingTimeout) {
        clearTimeout(this.typingTimeout);
      }

      console.log('User is typing...');

      this.typingTimeout = setTimeout(() => {
        console.log('User stopped typing');
      }, 3000);
    }
  }

  handleReaction(messageId: string, emoji: string) {
    this.messages = this.messages.map(msg => {
      if (msg.id === messageId) {
        const existingReactions = msg.reactions || [];
        const existingReaction = existingReactions.find(r => r.emoji === emoji);
        
        if (existingReaction) {
          const userAlreadyReacted = existingReaction.users.some(u => u.id === this.currentUser.id);
          if (userAlreadyReacted) {
            return {
              ...msg,
              reactions: existingReactions.map(r => 
                r.emoji === emoji 
                  ? {
                      ...r,
                      users: r.users.filter(u => u.id !== this.currentUser.id),
                      count: r.count - 1
                    }
                  : r
              ).filter(r => r.count > 0)
            };
          } else {
            return {
              ...msg,
              reactions: existingReactions.map(r => 
                r.emoji === emoji 
                  ? {
                      ...r,
                      users: [...r.users, this.currentUser],
                      count: r.count + 1
                    }
                  : r
              )
            };
          }
        } else {
          return {
            ...msg,
            reactions: [
              ...existingReactions,
              {
                emoji,
                users: [this.currentUser],
                count: 1
              }
            ]
          };
        }
      }
      return msg;
    });
  }

  handleFileUpload(files: File[]) {
    console.log('Files uploaded:', files);
  }

  handleMessageEdit(messageId: string, newContent: string) {
    this.messages = this.messages.map(msg => 
      msg.id === messageId 
        ? { 
            ...msg, 
            content: newContent, 
            edited: true, 
            editedAt: new Date() 
          }
        : msg
    );
  }

  handleMessageDelete(messageId: string) {
    this.messages = this.messages.filter(msg => msg.id !== messageId);
  }

  async handleLoadMore() {
    this.chatLoading = true;
    await new Promise(resolve => setTimeout(resolve, 1000));
    
    const olderMessages: ChatMessage[] = [
      {
        id: 'msg-old-1',
        content: 'Welcome to Thomson Reuters Legal Support. How can we assist you today?',
        user: this.supportTeam[2],
        timestamp: new Date(Date.now() - 1800000),
        type: 'text',
        status: 'read'
      }
    ];
    
    this.messages = [...olderMessages, ...this.messages];
    this.chatLoading = false;
  }

  handleThreadCreate(parentMessageId: string) {
    console.log('Thread created for:', parentMessageId);
  }

  private startTypingSimulation() {
    this.typingInterval = setInterval(() => {
      if (Math.random() > 0.8) {
        this.typingUsers = [this.supportTeam[0]];
        setTimeout(() => this.typingUsers = [], 2000);
      }
    }, 10000);
  }
}
```

### Team Collaboration Chat

#### React
```jsx
import { SafChat, SafIcon, SafBadge } from '@saffron/react';
import { useState, useEffect } from 'react';

const TeamCollaborationChat = () => {
  const [teamMessages, setTeamMessages] = useState([]);
  const [projectMessages, setProjectMessages] = useState([]);

  // Team members
  const teamMembers = [
    {
      id: 'team-lead',
      name: 'Alex Chen',
      avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=alex',
      role: 'Team Lead',
      status: 'online'
    },
    {
      id: 'developer-1',
      name: 'Jordan Smith',
      avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=jordan',
      role: 'Senior Developer',
      status: 'online'
    },
    {
      id: 'designer',
      name: 'Maya Patel',
      avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=maya',
      role: 'UX Designer',
      status: 'away'
    },
    {
      id: 'current-user',
      name: 'You',
      avatar: 'https://api.dicebear.com/7.x/avataaars/svg?seed=you',
      role: 'Developer',
      status: 'online',
      isCurrentUser: true
    }
  ];

  const currentUser = teamMembers.find(m => m.isCurrentUser);

  // Team chat messages
  const teamChatMessages = [
    {
      id: 'team-1',
      content: 'Good morning team! Let\'s discuss today\'s sprint planning.',
      user: teamMembers[0],
      timestamp: new Date(Date.now() - 600000),
      type: 'text',
      status: 'read'
    },
    {
      id: 'team-2',
      content: 'I\'ve completed the user authentication module. Ready for code review.',
      user: teamMembers[1],
      timestamp: new Date(Date.now() - 540000),
      type: 'text',
      status: 'read',
      reactions: [
        { emoji: '🎉', users: [teamMembers[0], teamMembers[2]], count: 2 },
        { emoji: '👍', users: [teamMembers[0]], count: 1 }
      ]
    },
    {
      id: 'team-3',
      content: 'Great work! I\'ll review it this afternoon. Also attaching the latest design mockups.',
      user: teamMembers[2],
      timestamp: new Date(Date.now() - 480000),
      type: 'file',
      status: 'read',
      attachments: [
        {
          id: 'design-1',
          name: 'Login_Mockups_v3.figma',
          url: '/files/login-mockups.figma',
          type: 'application/figma',
          size: 1248576,
          thumbnail: '/thumbnails/figma-icon.png'
        },
        {
          id: 'design-2',
          name: 'Dashboard_Wireframes.png',
          url: '/files/dashboard-wireframes.png',
          type: 'image/png',
          size: 892154,
          thumbnail: '/files/dashboard-wireframes.png'
        }
      ]
    }
  ];

  // Project-specific messages with threading
  const projectChatMessages = [
    {
      id: 'proj-1',
      content: '**Project Update**: Saffron Design System v2.0 is 75% complete! 🎯',
      user: teamMembers[0],
      timestamp: new Date(Date.now() - 900000),
      type: 'text',
      status: 'read'
    },
    {
      id: 'proj-2',
      content: 'Should we discuss the component architecture changes in a separate thread?',
      user: teamMembers[1],
      timestamp: new Date(Date.now() - 870000),
      type: 'text',
      status: 'read',
      threadCount: 3
    },
    {
      id: 'proj-2-thread-1',
      content: 'Yes, let\'s discuss the breaking changes for the Button component.',
      user: teamMembers[0],
      timestamp: new Date(Date.now() - 860000),
      type: 'text',
      status: 'read',
      parentId: 'proj-2'
    },
    {
      id: 'proj-2-thread-2',
      content: 'I\'ve documented all the prop changes in the migration guide.',
      user: currentUser,
      timestamp: new Date(Date.now() - 850000),
      type: 'text',
      status: 'read',
      parentId: 'proj-2'
    },
    {
      id: 'proj-3',
      content: 'The new SafChat component looks amazing! When can we start integration testing?',
      user: teamMembers[2],
      timestamp: new Date(Date.now() - 300000),
      type: 'text',
      status: 'read'
    }
  ];

  useEffect(() => {
    setTeamMessages(teamChatMessages);
    setProjectMessages(projectChatMessages);
  }, []);

  const handleTeamMessage = (message, attachments) => {
    const newMessage = {
      id: `team-${Date.now()}`,
      content: message,
      user: currentUser,
      timestamp: new Date(),
      type: attachments?.length > 0 ? 'file' : 'text',
      status: 'sent',
      attachments: attachments?.map((file, index) => ({
        id: `file-${Date.now()}-${index}`,
        name: file.name,
        url: URL.createObjectURL(file),
        type: file.type,
        size: file.size
      }))
    };

    setTeamMessages(prev => [...prev, newMessage]);
  };

  const handleProjectMessage = (message, attachments) => {
    const newMessage = {
      id: `proj-${Date.now()}`,
      content: message,
      user: currentUser,
      timestamp: new Date(),
      type: attachments?.length > 0 ? 'file' : 'text',
      status: 'sent',
      attachments: attachments?.map((file, index) => ({
        id: `file-${Date.now()}-${index}`,
        name: file.name,
        url: URL.createObjectURL(file),
        type: file.type,
        size: file.size
      }))
    };

    setProjectMessages(prev => [...prev, newMessage]);
  };

  return (
    <div className="team-collaboration-demo">
      <h2>Team Collaboration Chat</h2>

      <div className="collaboration-layout">
        {/* General Team Chat */}
        <div className="chat-panel">
          <div className="panel-header">
            <h3>
              <SafIcon name="users" />
              General Team Chat
            </h3>
            <SafBadge variant="success" size="small">
              {teamMembers.filter(m => m.status === 'online').length} online
            </SafBadge>
          </div>

          <SafChat
            messages={teamMessages}
            currentUser={currentUser}
            participants={teamMembers}
            variant="default"
            height="350px"
            showTimestamps={true}
            showAvatars={true}
            showUserNames={true}
            enableEmoji={true}
            enableFileUpload={true}
            enableReactions={true}
            enableMarkdown={false}
            placeholder="Message the team..."
            onSendMessage={handleTeamMessage}
            onReaction={(msgId, emoji) => {
              setTeamMessages(prev => 
                prev.map(msg => {
                  if (msg.id === msgId) {
                    const reactions = msg.reactions || [];
                    const existing = reactions.find(r => r.emoji === emoji);
                    if (existing) {
                      return {
                        ...msg,
                        reactions: reactions.map(r => 
                          r.emoji === emoji 
                            ? { ...r, users: [...r.users, currentUser], count: r.count + 1 }
                            : r
                        )
                      };
                    } else {
                      return {
                        ...msg,
                        reactions: [...reactions, { emoji, users: [currentUser], count: 1 }]
                      };
                    }
                  }
                  return msg;
                })
              );
            }}
          />
        </div>

        {/* Project-Specific Chat with Threading */}
        <div className="chat-panel">
          <div className="panel-header">
            <h3>
              <SafIcon name="folder" />
              Saffron DS v2.0 Project
            </h3>
            <div className="project-status">
              <SafBadge variant="warning" size="small">75% Complete</SafBadge>
              <SafBadge variant="info" size="small">Threading Enabled</SafBadge>
            </div>
          </div>

          <SafChat
            messages={projectMessages}
            currentUser={currentUser}
            participants={teamMembers}
            variant="threaded"
            height="350px"
            showTimestamps={true}
            showAvatars={true}
            showUserNames={true}
            enableEmoji={true}
            enableFileUpload={true}
            enableReactions={true}
            enableMarkdown={true}
            enableThreads={true}
            enableSearch={true}
            placeholder="Discuss project updates..."
            onSendMessage={handleProjectMessage}
            onThreadCreate={(parentId) => {
              console.log('Creating thread for message:', parentId);
            }}
          />
        </div>
      </div>

      {/* Minimal Status Updates */}
      <div className="status-updates">
        <h3>Quick Status Updates</h3>
        
        <SafChat
          messages={[
            {
              id: 'status-1',
              content: '✅ Deployed to staging',
              user: teamMembers[1],
              timestamp: new Date(Date.now() - 120000),
              type: 'text',
              status: 'read'
            },
            {
              id: 'status-2',
              content: '🚀 New feature branch pushed',
              user: teamMembers[2],
              timestamp: new Date(Date.now() - 60000),
              type: 'text',
              status: 'read'
            }
          ]}
          currentUser={currentUser}
          participants={teamMembers}
          variant="minimal"
          height="150px"
          showTimestamps={false}
          showAvatars={true}
          showUserNames={false}
          enableEmoji={true}
          enableFileUpload={false}
          enableReactions={false}
          placeholder="Quick update..."
          onSendMessage={(message) => console.log('Status update:', message)}
        />
      </div>

      {/* Integration Examples */}
      <div className="integration-examples">
        <h3>Integration Features</h3>
        
        <div className="integration-grid">
          <div className="integration-item">
            <SafIcon name="github" />
            <h4>Git Integration</h4>
            <p>Automatic notifications for commits, PRs, and deployments</p>
          </div>
          
          <div className="integration-item">
            <SafIcon name="calendar" />
            <h4>Calendar Sync</h4>
            <p>Meeting reminders and schedule updates</p>
          </div>
          
          <div className="integration-item">
            <SafIcon name="bug" />
            <h4>Issue Tracking</h4>
            <p>Automatic bug reports and task assignments</p>
          </div>
          
          <div className="integration-item">
            <SafIcon name="cloud" />
            <h4>Cloud Storage</h4>
            <p>Seamless file sharing from cloud providers</p>
          </div>
        </div>
      </div>
    </div>
  );
};
```

## Best Practices

1. **Message Management**
   - Implement efficient message pagination
   - Use virtualization for large message lists
   - Cache messages locally for offline access
   - Handle message ordering and deduplication

2. **Real-time Features**
   - Implement WebSocket connections for live updates
   - Handle connection failures gracefully
   - Provide appropriate retry mechanisms
   - Show connection status indicators

3. **User Experience**
   - Auto-scroll to new messages appropriately
   - Preserve scroll position when loading history
   - Provide clear visual feedback for message states
   - Implement smooth animations and transitions

4. **File Handling**
   - Validate file types and sizes
   - Provide upload progress indicators
   - Support file previews when possible
   - Implement secure file sharing mechanisms

5. **Accessibility**
   - Support keyboard navigation throughout
   - Provide screen reader announcements
   - Ensure proper focus management
   - Use semantic markup for message structure

## Accessibility Considerations

1. **Screen Reader Support**
   - Announce new messages appropriately
   - Provide context for message authors and timestamps
   - Use proper ARIA labels for interactive elements
   - Support navigation landmarks

2. **Keyboard Navigation**
   - Tab navigation through message actions
   - Keyboard shortcuts for common operations
   - Support arrow key navigation in message lists
   - Accessible emoji picker and reactions

3. **Visual Accessibility**
   - Sufficient color contrast for all message states
   - Clear visual indicators for message status
   - Support for reduced motion preferences
   - Scalable text and interface elements

4. **Content Accessibility**
   - Format timestamps accessibly
   - Provide alternative text for images and attachments
   - Support for multiple languages
   - Clear indication of message edit history

## Related Components

- **SafAvatar**: User profile pictures in messages
- **SafIcon**: Message type indicators and actions
- **SafBadge**: Online status and notification counts
- **SafButton**: Message action buttons
- **SafFileUpload**: File attachment functionality

## Notes

- Chat component supports real-time updates through WebSocket integration
- Built-in message virtualization for performance with large message histories
- Comprehensive emoji support with custom emoji sets
- Thread management with nested conversation support
- File sharing with preview capabilities and size limits
- Message editing and deletion with proper audit trails
- Mobile-responsive design with touch-friendly interactions
