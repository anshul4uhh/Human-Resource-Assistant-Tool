<div align="center">

<br/>

```
██╗  ██╗██████╗      █████╗ ███████╗███████╗██╗███████╗████████╗
██║  ██║██╔══██╗    ██╔══██╗██╔════╝██╔════╝██║██╔════╝╚══██╔══╝
███████║██████╔╝    ███████║███████╗███████╗██║███████╗   ██║   
██╔══██║██╔══██╗    ██╔══██║╚════██║╚════██║██║╚════██║   ██║   
██║  ██║██║  ██║    ██║  ██║███████║███████║██║███████║   ██║   
╚═╝  ╚═╝╚═╝  ╚═╝    ╚═╝  ╚═╝╚══════╝╚══════╝╚═╝╚══════╝   ╚═╝   
```

### 🤖 AI-Powered Human Resource Management via MCP

<br/>

[![Python](https://img.shields.io/badge/Python-3.12+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![MCP](https://img.shields.io/badge/MCP-FastMCP-FF6B6B?style=for-the-badge&logo=anthropic&logoColor=white)](https://github.com/anthropics/mcp)
[![License](https://img.shields.io/badge/License-MIT-22C55E?style=for-the-badge)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Active-22C55E?style=for-the-badge)]()
[![uv](https://img.shields.io/badge/Package_Manager-uv-7C3AED?style=for-the-badge)](https://github.com/astral-sh/uv)

<br/>

> *Streamline your HR operations with an intelligent AI assistant — manage employees, leaves, meetings, tickets, and emails all through natural language.*

<br/>

</div>

---

## ✨ Overview

**HR Assist Tool** is a **Model Context Protocol (MCP) server** that plugs your Human Resource Management System (HRMS) directly into AI assistants like Claude. Instead of navigating complex HR dashboards, you simply *talk* to your AI — and it handles the rest.

From onboarding a new hire to scheduling meetings and managing leave balances, this tool brings the full power of an HRMS into a conversational interface.

---

## 🗂️ Project Structure

```
Human-Resource-Assistant-Tool/
│
├── 📄 server.py          # MCP server — tools, prompts & resources
├── 📄 main.py            # Entry point
├── 📄 emails.py          # Email sending via SMTP (Gmail)
├── 📄 utils.py           # Seeding & utility helpers
│
├── 📁 hrms/              # Core HRMS logic
│   ├── employee_manager  # Employee CRUD & search
│   ├── leave_manager     # Leave balance & history
│   ├── meeting_manager   # Meeting scheduling & cancellation
│   └── ticket_manager    # Equipment/resource tickets
│
├── 📄 pyproject.toml     # Project dependencies
├── 📄 uv.lock            # Locked dependency versions
└── 📄 .python-version    # Python version pin
```

---

## 🚀 Features

| Feature | Description |
|---|---|
| 👤 **Employee Management** | Add employees, search by name, fetch full details |
| 🌴 **Leave Management** | Apply for leave, check balances, view history |
| 📅 **Meeting Scheduler** | Schedule, list, and cancel meetings |
| 🎫 **Ticket System** | Raise & track equipment/resource requests |
| 📧 **Email Automation** | Send emails via Gmail SMTP directly from the AI |
| 🤖 **Onboarding Prompt** | One-shot AI prompt to fully onboard a new hire |
| 🔌 **MCP Compatible** | Works with any MCP-capable AI client (Claude, etc.) |

---

## 🛠️ MCP Tools

The server exposes the following tools to AI assistants:

```python
🔧 add_employee(emp_name, manager_id, email)
        → Add a new employee to the system

🔧 get_employee_details(name)
        → Look up an employee's full profile

🔧 send_email(subject, body, to_emails)
        → Send an email via Gmail SMTP

🔧 create_ticket(emp_id, item, reason)
        → Raise a ticket for laptop, ID card, etc.

🔧 update_ticket_status(ticket_id, status)
        → Update the status of an existing ticket

🔧 list_tickets(employee_id, status)
        → View tickets filtered by status

🔧 schedule_meeting(employee_id, datetime, topic)
        → Book a meeting for an employee

🔧 get_meetings(employee_id)
        → List all upcoming meetings

🔧 cancel_meeting(employee_id, datetime, topic)
        → Cancel a scheduled meeting

🔧 get_employee_leave_balance(emp_id)
        → Check remaining leave days

🔧 apply_leave(emp_id, leave_dates)
        → Submit a leave application

🔧 get_leave_history(emp_id)
        → View an employee's leave history
```

### 💬 Built-in Prompt

```
📋 onboard_new_employee(employee_name, manager_name, employee_email)
```
A complete onboarding flow that automatically:
- Registers the employee in the HRMS
- Sends a welcome email
- Notifies the manager
- Raises tickets for required equipment
- Schedules an intro meeting with the manager

---

## ⚙️ Setup & Installation

### Prerequisites

- Python **3.12+**
- A Gmail account with **App Password** enabled
- [`uv`](https://github.com/astral-sh/uv) package manager

### 1. Clone the Repository

```bash
git clone https://github.com/anshul4uhh/Human-Resource-Assistant-Tool.git
cd Human-Resource-Assistant-Tool
```

### 2. Install Dependencies

```bash
uv sync
```

### 3. Configure Environment Variables

Create a `.env` file in the root directory:

```env
HR_email=your-gmail@gmail.com
HR_password=your-gmail-app-password
```

> ⚠️ **Note:** Use a [Gmail App Password](https://support.google.com/accounts/answer/185833), not your regular account password.

### 4. Run the Server

```bash
uv run server.py
```

---

## 🔌 Connecting to Claude (MCP Client)

Add the following to your Claude MCP configuration file (`claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "hr-assist": {
      "command": "uv",
      "args": [
        "--directory",
        "/absolute/path/to/Human-Resource-Assistant-Tool",
        "run",
        "server.py"
      ]
    }
  }
}
```

Once connected, you can chat with Claude to manage your entire HR workflow!

---

## 💡 Example Usage

Once connected to Claude, you can say things like:

```
"Onboard a new employee — John Doe, manager is Sarah, email is john@company.com"

"What's the leave balance for employee E003?"

"Schedule a meeting with E005 on Friday at 3pm to discuss Q2 goals"

"Raise a laptop ticket for employee E002 — they're starting next week"

"Send a reminder email to the engineering team about the all-hands meeting"
```

---

## 🏗️ Architecture

```
┌─────────────────────┐         ┌──────────────────────┐
│                     │  MCP    │                      │
│   AI Client         │◄───────►│   server.py          │
│   (Claude, etc.)    │ stdio   │   (FastMCP Server)   │
│                     │         │                      │
└─────────────────────┘         └──────────┬───────────┘
                                           │
                      ┌────────────────────┼────────────────────┐
                      │                    │                    │
             ┌────────▼──────┐   ┌─────────▼──────┐   ┌────────▼────────┐
             │  EmployeeManager│  │  LeaveManager  │   │ MeetingManager  │
             └───────────────┘   └────────────────┘   └─────────────────┘
                      │
             ┌────────▼──────┐   ┌────────────────┐
             │ TicketManager │   │  EmailSender   │
             └───────────────┘   └────────────────┘
```

---

## 🤝 Contributing

Contributions are welcome! Here's how to get started:

1. **Fork** the repository
2. **Create** a feature branch: `git checkout -b feature/amazing-feature`
3. **Commit** your changes: `git commit -m 'Add amazing feature'`
4. **Push** to the branch: `git push origin feature/amazing-feature`
5. **Open** a Pull Request

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

<div align="center">

Made with ❤️ by [anshul4uhh](https://github.com/anshul4uhh)

⭐ Star this repo if you found it useful!

</div>
