# Smart Agricultural Product Inventory Management System

A web application to manage farm stock: items, warehouses, suppliers, batches, stock receiving, usage/wastage, FIFO/FEFO dispatch suggestions, distributor orders, and low-stock / expiry alerts. It includes role-based access control with login/logout enforcement for Farm Manager, Warehouse Officer, and Distributor.

## Team Members:

1. Tahmina Aktar Neha (TN) - 2220592 ([@TahminaAktarNeha30](https://github.com/TahminaAktarNeha30))
2. Maksuratun Rashmi (MR) - 2220871 ([@rashmii01](https://github.com/rashmii01))
3. Maimuna Akter Tripty (MT) - 2221582 ([@maimunaaaaa](https://github.com/maimunaaaaa))
4. Mehnaj Akter (MA) - 2222624 ([@Mehnaj14](https://github.com/Mehnaj14))

### Course Information:
**CSE451: Software Engineering, Section 02, Autumn 2026**  
Department of Computer Science & Engineering, Independent University, Bangladesh (IUB)  
**Submitted to:** Dr. Md. Mushfique Anwar

---

# How to Use

## 1. Clone the project
- Install Git / Git Bash
- Open your local directory's Git Bash terminal
- Configure Git:
  ```bash
  git config --global user.name <github_username>
  git config --global user.email <github_email>
  ```
- Run command:
  ```bash
  git clone https://github.com/TahminaAktarNeha30/Smart-agricultural-product-inventory-management-system.git
  ```

## 2. Navigate to the project directory commands
- Navigate:
  ```bash
  cd Smart-agricultural-product-inventory-management-system
  ```
- Open VS Code:
  ```bash
  code .
  ```
- Open terminal:
  `Ctrl + ` ` (or `Ctrl + J`)

## 3. Run the Project:
- Check Node.js version (Requires Node.js 18 or newer):
  ```bash
  node --version
  ```
- Install dependencies:
  ```bash
  npm install
  ```
- See branch list:
  ```bash
  git branch -a
  ```
- Checkout to specific branch:
  ```bash
  git checkout <branch_name>
  ```
- Run the project:
  ```bash
  npm start
  ```
- Click and follow: `http://localhost:3000/`

### Demo Login Accounts:
| Role | Username | Password |
|---|---|---|
| Farm Manager | `manager` | `manager123` |
| Warehouse Officer | `officer` | `officer123` |
| Distributor | `distributor` | `distributor123` |

*(The login page also has clickable demo accounts that fill the form for you.)*

### Other Useful Commands:
| Command | What it does |
|---|---|
| `npm test` | Runs all unit tests and prints the coverage table |
| `npm run lint` | Checks the code style with ESLint |
| `npm run docs` | Generates JSDoc documentation into `docs/api/index.html` |
| `npm run demo-data` | Resets `data/db.json` to fresh demo data |

---

# How to Develop

## 1. Create a new branch:
- Always branch off the latest `develop` branch:
  ```bash
  git checkout develop
  git pull origin develop
  git checkout -b <new_branch_name>
  ```
  *Branch naming standard:* `feature/member1-catalog`, `feature/member2-stock-auth`, `feature/member3-usage-fifo`, `feature/member4-orders-alerts`

## 2. Make Changes:
- Modify or create feature code in `src/` and `public/`.
- Run test cases to ensure everything is working as expected:
  ```bash
  npm test
  ```
- Run style checks:
  ```bash
  npm run lint
  ```

## 3. Commit and Push Changes:
- Commit changes to your local branch using conventional commit messages:
  ```bash
  git add .
  git commit -m "feat(catalog): reject empty unit"
  ```
- Push changes to the remote repository:
  ```bash
  git push origin <new_branch_name>
  ```

## 4. Check CI:
- Go to GitHub Actions tab in the repository
- Click on the latest workflow run for your branch
- Ensure all automated tests and lint checks pass

## 5. Create a Pull Request:
- Open a Pull Request from your feature branch to the `develop` branch.
- Detail the features implemented, acceptance criteria tested, and any relevant screenshots.

## 6. Review and Merge:
- Teammates review the changes in the Pull Request.
- Once approved, merge changes into the `develop` branch.
- Periodically, `develop` is merged into `main` for release milestones.

## 7. Update Local Repository:
- Switch back to `develop`:
  ```bash
  git checkout develop
  ```
- Pull the latest changes:
  ```bash
  git pull origin develop
  ```
- Delete the local feature branch (optional):
  ```bash
  git branch -d <new_branch_name>
  ```
- Delete the remote feature branch (if merged and no longer needed):
  ```bash
  git push origin --delete <new_branch_name>
  ```

---

# Architecture & Project Structure

## Layered Architecture
```
Browser (public/)                    Server (Node.js + Express)
┌──────────────────────┐   HTTP    ┌─────────────────────────────────────────────┐
│ 1 PRESENTATION       │  JSON     │ 2 REQUEST HANDLING   routes + controllers   │
│ index.html, css, js  │ ───────►  │   (checks login + role, calls a service)    │
│ shows pages, sends   │           │ 3 BUSINESS LOGIC     services               │
│ requests with token  │ ◄───────  │   (all rules: FIFO/FEFO, no negative stock) │
└──────────────────────┘           │ 4 DATA ACCESS        dal/ (repositories)    │
                                   │   (only layer that touches data/db.json)    │
                                   └─────────────────────────────────────────────┘
```

## Repository Structure
```
agri-product/
├── .github/workflows/        GitHub Actions CI pipeline configuration
├── config/                   Roles, constants, BD date and expiry helpers
├── data/                     db.json database + automatic backups
├── docs/                     Generated API documentation directory (JSDoc output in docs/api)
├── public/                   1. Presentation Layer (SPA: HTML, CSS, client JS)
├── resources/                Architecture documentation, testing reports, and team work split
├── scripts/                  Database reset and helper scripts
├── src/                      Backend implementation
│   ├── controllers/          2. Request Handling layer
│   ├── dal/                  4. Data Access Layer (database & repositories)
│   ├── middleware/           Authentication and role-guard middleware
│   ├── routes/               API URL definitions
│   └── services/             3. Business Logic Layer
├── tests/                    Unit and integration tests
├── .gitignore                Git ignore specifications
├── eslint.config.js          ESLint configuration
├── jsdoc.json                JSDoc generation configuration
├── LICENSE                   MIT License
├── package.json              Project dependencies and npm scripts
├── README.md                 Project documentation & Git guidelines
└── server.js                 Express server bootstrap
```

## Team Work Split & Branch Assignments
| Member | Features | Branch Name | SRS User Stories |
|---|---|---|---|
| **Member 1** (Tahmina Aktar Neha) | **F1 Item Catalog** + **F2 Warehouses & Suppliers** | `feature/member1-catalog` | US-01A, 01B, 01C, 02A, 02B, 02C |
| **Member 2** (Maksuratun Rashmi) | **F3 Stock Receiving** + **F4 Stock Overview** (+ Auth) | `feature/member2-stock-auth` | US-03, US-04 |
| **Member 3** (Maimuna Akter Tripty) | **F5 Usage & Wastage** + **F6 FIFO/FEFO Suggestions** | `feature/member3-usage-fifo` | US-05A, 05B, 06 |
| **Member 4** (Mehnaj Akter) | **F7 Orders & Dispatch** + **F8 Low Stock & Expiry Alerts** | `feature/member4-orders-alerts` | US-7A to 7F, 8A, 8B |

*(For detailed method-level assignments and exam presentation guidelines, see [TEAM_WORK_SPLIT.md](resources/TEAM_WORK_SPLIT.md).)*
