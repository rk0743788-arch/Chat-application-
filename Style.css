// Global Variables
let currentUser = '';
const STORAGE_KEYS = {
    USER: 'chatUser',
    MESSAGES: 'chatMessages',
    CONTACTS: 'chatContacts',
    THEME: 'chatTheme'
};

// Initialize App
document.addEventListener('DOMContentLoaded', function() {
    const loginForm = document.getElementById('login-form');
    loginForm.addEventListener('submit', handleLogin);

    const messageForm = document.getElementById('message-form');
    messageForm.addEventListener('submit', handleSendMessage);

    loadTheme();
    loadProfile();
    if (localStorage.getItem(STORAGE_KEYS.USER)) {
        currentUser = localStorage.getItem(STORAGE_KEYS.USER);
        showMainApp();
    }
});

// Login Handler
function handleLogin(e) {
    e.preventDefault();
    const username = document.getElementById('username').value.trim();
    if (username) {
        currentUser = username;
        localStorage.setItem(STORAGE_KEYS.USER, currentUser);
        showMainApp();
        loadMessages();
        loadContacts();
        document.getElementById('profile-username').textContent = currentUser;
    } else {
        alert('Please enter a username.');
    }
}

// Show Main App (Hide Login, Show Sidebar and First Section)
function showMainApp() {
    document.getElementById('login-section').classList.remove('active');
    document.getElementById('sidebar').classList.remove('hidden');
    showSection('chat-section');
}

// Show Specific Section
function showSection(sectionId) {
    // Hide all sections
    document.querySelectorAll('.section').forEach(sec => sec.classList.add('hidden'));
    // Show selected
    document.getElementById(sectionId).classList.remove('hidden');
    if (sectionId === 'chat-section') loadMessages();
    if (sectionId === 'contacts-section') loadContacts();
}

// Logout
function logout() {
    localStorage.removeItem(STORAGE_KEYS.USER);
    localStorage.removeItem(STORAGE_KEYS.MESSAGES);
    localStorage.removeItem(STORAGE_KEYS.CONTACTS);
    currentUser = '';
    document.getElementById('sidebar').classList.add('hidden');
    document.getElementById('login-section').classList.add('active');
    document.getElementById('username').value = '';
}

// Handle Send Message
function handleSendMessage(e) {
    e.preventDefault();
    const input = document.getElementById('message-input');
    const message = input.value.trim();
    if (message) {
        const messages = getFromStorage(STORAGE_KEYS.MESSAGES, []);
        messages.push({
            id: Date.now(),
            sender: currentUser,
            content: message,
            timestamp: new Date().toLocaleTimeString()
        });
        saveToStorage(STORAGE_KEYS.MESSAGES, messages);
        input.value = '';
        loadMessages();
    }
}

// Load Messages
function loadMessages() {
    const messages = getFromStorage(STORAGE_KEYS.MESSAGES, []);
    const container = document.getElementById('chat-messages');
    container.innerHTML = '';
    messages.forEach(msg => {
        const div = document.createElement('div');
        div.className = `message ${msg.sender === currentUser ? 'sent' : 'received'}`;
        div.innerHTML = `<strong>${msg.sender}:</strong> ${msg.content} <small>${msg.timestamp}</small>`;
        container.appendChild(div);
    });
    container.scrollTop = container.scrollHeight;
}

// Add Contact
function addContact() {
    const name = prompt('Enter contact name:');
    const email = prompt('Enter email:');
    if (name && email) {
        const contacts = getFromStorage(STORAGE_KEYS.CONTACTS, []);
        contacts.push({
            id: Date.now(),
            name: name,
            email: email,
            status: 'Offline'
        });
        saveToStorage(STORAGE_KEYS.CONTACTS, contacts);
        loadContacts();
    }
}

// Load Contacts
function loadContacts() {
    const contacts = getFromStorage(STORAGE_KEYS.CONTACTS, []);
    const list = document.getElementById('contacts-list');
    list.innerHTML = '';
    contacts.forEach(contact => {
        const li = document.createElement('li');
        li.className = 'contact';
        li.innerHTML = `
            <span>${contact.name} (${contact.email}) - ${contact.status}</span>
            <div>
                <button onclick="editContact(${contact.id})">Edit</button>
                <button onclick="deleteContact(${contact.id})">Delete</button>
            </div>
        `;
        list.appendChild(li);
    });
}

// Edit Contact (Simulation)
function editContact(id) {
    alert(`Edit contact with ID: ${id} (Implement full edit form here)`);
}

// Delete Contact
function deleteContact(id) {
    if (confirm('Delete this contact?')) {
        let contacts = getFromStorage(STORAGE_KEYS.CONTACTS, []);
        contacts = contacts.filter(c => c.id !== id);
        saveToStorage(STORAGE_KEYS.CONTACTS, contacts);
        loadContacts();
    }
}

// Theme Management
function changeTheme() {
    const theme = document.getElementById('theme-select').value;
    document.body.className = theme === 'dark' ? 'dark' : '';
    localStorage.setItem(STORAGE_KEYS.THEME, theme);
}

function loadTheme() {
    const theme = localStorage.getItem(STORAGE_KEYS.THEME) || 'light';
    document.getElementById('theme-select').value = theme;
    document.body.className = theme === 'dark' ? 'dark' : '';
}

// Load Profile
function loadProfile() {
    const user = localStorage.getItem(STORAGE_KEYS.USER);
    if (user) {
        document.getElementById('profile-username').textContent = user;
    }
}

// Storage Helpers
function getFromStorage(key, defaultValue) {
    const data = localStorage.getItem(key);
    return data ? JSON.parse(data) : defaultValue;
}

function saveToStorage(key, data) {
    localStorage.setItem(key, JSON.stringify(data));
}

// Simulate Real-Time Updates (Polling every 5 seconds)
setInterval(() => {
    if (currentUser) {
        loadMessages();
        // Simulate status updates for contacts
        let contacts = getFromStorage(STORAGE_KEYS.CONTACTS, []);
        contacts.forEach(c => {
            if (Math.random() > 0.7) c.status = 'Online';
            else c.status = 'Offline';
        });
        saveToStorage(STORAGE_KEYS.CONTACTS, contacts);
        if (document.getElementById('contacts-section').classList.contains('hidden') === false) {
            loadContacts();
        }
    }
}, 5000);
