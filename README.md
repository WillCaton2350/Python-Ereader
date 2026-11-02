# Django Ereader
A Django-powered book library and e-reader application for organizing a personal collection, opening book documents, writing reviews, and tracking reading progress.
Features
- Book library — Browse books stored in the database, with support for book details such as title, author, publisher, format, price, cover image, and document file.
- E-reader — Open a selected book document from the collection and navigate between available books.
- Search — Find books by title.
- Pagination — Display book collections in manageable pages.
- Reviews — Rate books and save written reviews. (WIP)
- Reading-status tracking — Organize books into:
  - Currently Reading
  - Finished Books
  - Did Not Finish (DNF)
- Status transitions — The intended workflow keeps a book in only one of the three reading-status categories at a time.
- Django admin — Manage database records through Django's administrative interface.
- REST API — Django REST Framework serializers and endpoints support book data operations.
Technology Stack
- Python
- Django
- Django REST Framework
- SQLite (development database)
- HTML, CSS, and JavaScript
- Django templates
Project Structure
The exact layout may vary depending on your local checkout. The application includes components such as:
book_tracker_app/
├── backend/
│   ├── manage.py
│   ├── backend/              # Django project configuration
│   └── frontend/             # App code (models, views, serializers, URLs)
├── venv/                     # Python virtual environment
└── README.md
The app's codebase includes Django models for books, reviews, currently reading, DNF, and finished books, along with serializers, views, URL routes, and templates such as index.html, library.html, Reviews.html, and ereader.html.
Requirements
- Python 3.13 (or a compatible Python version for your installed Django version)
- pip
- A terminal
- Git, if cloning the project
- The Python packages listed in your project's requirements.txt, if available
Setup
1. Get the project
If the project is hosted in a Git repository:
git clone <repository-url>
cd book_tracker_app
If you already have the project locally, navigate to its root directory instead.
2. Create and activate a virtual environment
macOS/Linux:
python3 -m venv venv
source venv/bin/activate
If your virtual environment already exists, activate it rather than creating another one.
3. Install dependencies
If the project has a requirements.txt file:
pip install -r requirements.txt
Otherwise, install the packages your project uses. At minimum, the known framework dependencies include:
pip install Django djangorestframework Pillow
Pillow is used for Django image-field support. Your project may require additional packages.
4. Enter the Django project directory
Navigate to the directory containing manage.py. For example, if manage.py is inside backend/:
cd backend
Adjust this path to match your checkout.
5. Apply database migrations
python manage.py makemigrations
python manage.py migrate
If migrations already exist in the repository, python manage.py migrate is normally sufficient. Avoid regenerating migrations unnecessarily in an established project.
6. Create an administrator account
python manage.py createsuperuser
Follow the prompts to set the administrator credentials.
7. Start the development server
python manage.py runserver
Open the development URL printed in the terminal, usually:
- Application: http://127.0.0.1:8000/
- Django admin: http://127.0.0.1:8000/admin/
Using the App
1. Add book records through the Django admin or the application's supported data-entry/API workflow.
2. Provide book metadata and, when applicable, a cover image and document file.
3. Browse the collection through the home or library pages.
4. Select a book to open it in the e-reader.
5. Add a review and rating from the Reviews page.
6. Track a book as Currently Reading, Finished, or DNF using the application's status controls.
A book's document must be uploaded and accessible to Django for the e-reader to open it. Supported document formats depend on the file types and viewer behavior implemented in the application.
Data Models
The application currently uses models corresponding to these concepts:
Model	Purpose
book_model	Stores book metadata, cover images, and document files
review_model	Stores a book's rating, written review, and timestamp
currently_reading_model	Tracks books currently being read and the last-read timestamp
books_finished_model	Tracks books marked as finished
dnf_model	Tracks books marked as Did Not Finish


The reading-status workflow is intended to be mutually exclusive: when a book changes status, it should be removed from the other status categories. Check the relevant view functions if you change this behavior.
URL Routes
The project has routes for the home page, library, Reviews page, and e-reader. It also includes routes for adding DNF and finished-book statuses and removing a book from Currently Reading. The exact URL paths are defined in the app's urls.py.
REST API
The project uses Django REST Framework serializers for book and related data. Available operations and request formats are defined by the API views and URL configuration. Consult those files for the exact endpoint paths, required fields, and whether an endpoint accepts individual objects or lists.
Configuration and Media Files
- Keep secret keys and environment-specific settings out of source control.
- Configure DEBUG, ALLOWED_HOSTS, database settings, and media-file settings appropriately for your environment.
- Uploaded cover images and book files require correct Django MEDIA_ROOT and MEDIA_URL configuration.
- Do not use Django's development server as a production server.
Development Notes
- Make model changes through Django migrations.
- Back up the SQLite database before making schema changes or resetting development data.
- If existing database records predate a new relationship, associate or migrate those records carefully rather than assuming they already reference a book.
- When debugging pagination or AJAX/HTMX requests, check both the view context and the template partial that renders the results.
Future Improvements
Possible additions include:
- Automated tests for book CRUD operations, reading-status transitions, and pagination
- More robust filtering by author and book format
- Improved reader controls and document-format handling
- Dependency pinning in requirements.txt
- Production deployment configuration
License
Add a license here if you intend to distribute this project publicly.
