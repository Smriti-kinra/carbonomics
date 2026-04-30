}
# Carbonomics — IUPAC Nomenclature Learning System

Carbonomics is a Python-based CLI application designed to help students learn and practice IUPAC nomenclature for organic and coordination compounds.

It provides structured study material, examples, testing modules, and admin controls for managing content.

## Features

- Study IUPAC rules and examples
- Covers:
  - Organic compounds (alkanes, alkenes, alcohols, etc.)
  - Coordination compounds
- Interactive quizzes with scoring
- Admin panel for managing study data
- User authentication system
- Feedback and rating system

## Tech Stack

- Python 3
- MySQL (mysql-connector)
- Tabulate (for table display)

## Installation

1. Clone the repository:

```bash
git clone https://github.com/your-username/carbonomics.git
cd carbonomics
```

2. Install dependencies:

```bash
pip install tabulate mysql-connector-python
```

3. Set up MySQL:

- Create a MySQL user
- Update credentials in the script (or use environment variables)

4. Run the project:

```bash
python main.py
```

## Usage

- Choose between Admin and User mode
- Study IUPAC rules and examples
- Take tests and track scores
- Admin can add/update/delete study material

## Project Structure

```bash
main.py
README.md
```

## Future Improvements

- GUI version (Tkinter / PyQt)
- Web-based deployment (Flask / Django)
- Better UI formatting
- Password hashing for security

## Security Notes

- Avoid storing plain-text passwords
- Use parameterized SQL queries to prevent injection
- Use environment variables for sensitive credentials

## License

This project is open-source and free to use
