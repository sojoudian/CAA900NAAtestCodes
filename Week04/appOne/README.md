# Setting up MySQL for Flask App

## Prerequisites
Before you begin, ensure you have the following installed on your system:
- **Python 3.10+**
- **MySQL Server**
- **pip** (Python package installer)
- (Optional) **Virtual Environment** (recommended)

## Setup Instructions

### 1. Install MySQL
Follow the [official MySQL installation guide](https://dev.mysql.com/downloads/installer/) for your platform.

### 2. Start MySQL and Create a Database
Open MySQL as the root user:
```bash
mysql -u root -p
```
Create a new database:
```sql
CREATE DATABASE mydatabase;
```

### 3. Create a MySQL User and Grant Privileges
```sql
CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON mydatabase.* TO 'newuser'@'localhost';
FLUSH PRIVILEGES;
```
Exit MySQL:
```bash
exit
```

### 4. Clone the Project Repository
```bash
git clone <repository-url>
cd <project-directory>
```

### 5. Create and Activate a Virtual Environment (Optional but Recommended)
```bash
# Create a virtual environment
python -m venv venv

# Activate the virtual environment
# On macOS/Linux:
source venv/bin/activate
# On Windows:
venv\Scripts\activate
```

### 6. Install Dependencies
```bash
pip install -r requirements.txt
```

### 7. Configure Database Connection
Update the Flask app’s configuration file (e.g., `config.py` or `app.py`) with the following:
```python
app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql+pymysql://newuser:password@localhost/mydatabase'
```

### 8. Initialize the Database
Ensure database tables are created before running the application:
```python
if __name__ == '__main__':
    with app.app_context():
        db.create_all()
    app.run(debug=True)
```

### 9. Run the Flask Application
```bash
python app.py
```
Visit [http://127.0.0.1:5000](http://127.0.0.1:5000) in your web browser to access the application.

## Troubleshooting

### Access Denied Errors
If you encounter:
```bash
sqlalchemy.exc.OperationalError: (pymysql.err.OperationalError) (1045, "Access denied for user 'newuser'@'localhost'")
```
Ensure:
- The MySQL user is created with the correct host specification (`localhost`).
- Your Flask app’s connection string is properly configured.

### MySQL Not Running
Check if the MySQL server is running:
```bash
# On Linux:
sudo service mysql status
# On macOS (Homebrew):
brew services list
# On Windows:
net start mysql
```

## License
Include your license information here if applicable.

## Acknowledgments
- [Flask Documentation](https://flask.palletsprojects.com/)
- [SQLAlchemy Documentation](https://docs.sqlalchemy.org/)
- [PyMySQL Documentation](https://pymysql.readthedocs.io/)

