# E-learning-Site

## Overview

This is a Django-based web application designed for creating and managing e-learning content. Version 1 includes user authentication functionality, such as signup, login, and logout, along with an admin panel to manage the site.

## Version 1 - Initial Setup

### Features

- **User authentication**:
  - **Signup**: Allows users to create a new account.
  - **Login**: Allows users to authenticate with their account.
  - **Logout**: Allows users to log out of the system.
- **Admin panel**: Accessible via `/admin`, enabling site management and user administration.

### Installation

#### Prerequisites

- Python 3.x
- Django 4.x

#### Setup Steps

1. **Clone the repository**:
   Clone the repository from GitHub using the following command:

   ```bash
   git clone https://github.com/mohsinfolium/E-learning-Site.git
   ```

2. **Navigate to the project directory**:
   After cloning the repository, move into the project directory:

   ```bash
   cd E-learning-Site
   ```

3. **Install required dependencies**:
   It is recommended to set up a virtual environment before installing the dependencies. If you're using `venv`, create a virtual environment and activate it:

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

   Then install the dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. **Initialize Django Project**:
   To create the initial project files, run:

   ```bash
   django-admin startproject elearning
   ```

5. **Run the server**:
   Finally, run the Django development server to see the project in action:
   ```bash
   python manage.py runserver
   ```
