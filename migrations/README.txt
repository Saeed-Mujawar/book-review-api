Step-by-Step Guide
1. Install Alembic
To install Alembic, use pip:

    pip install alembic

2. Initialize Alembic with Async Support
Run the following command to initialize Alembic with async support:

    alembic init -t async migrations

This will create an alembic directory with a migrations folder and necessary configuration files.

3. Configure env.py
Edit the env.py file inside the migrations directory to set up the database URL and metadata.

Open the env.py file located at migrations/env.py.
Add the following code snippet:

    from sqlmodel import SQLModel
    from src.config import Config

    # Set up the SQLAlchemy database URL
    database_url = Config.DATABASE_URL
    target_metadata = SQLModel.metadata

    def run_migrations_online():
        # Retrieve the config object and set the database URL
        config.set_main_option("sqlalchemy.url", database_url)

        # Additional setup for async migration (if needed) would go here

Make sure to adjust src.config.Config to match the actual path to your configuration module.

4. Create a New Migration
To create a new migration with auto-generated changes, use the following command:

    alembic revision --autogenerate -m "init"

This command will create a new migration file in the migrations/versions directory with the specified message "init".

5. Apply Migrations
To apply the migrations to your database, use:

    alembic upgrade head

This will apply all the changes from your migration files to the database.