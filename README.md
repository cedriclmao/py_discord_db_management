## Discord Mysql Management Framework 
This package is used to dynamically **add new data** to your existing Mysql tables.<br>
You're also able to **delete** or **view** data.<br>
It'll return you an embed & a view for you to send back.

**TODO: MAKE IT FULLY WORKING WITH PYCORD**

### Built With
[![Python][python]][python-url]
[![MySQL][mysql]][mysql-url]
![Discord](https://img.shields.io/badge/Discord-%235865F2.svg?style=for-the-badge&logo=discord&logoColor=white)


### How to get started
1. Install the package
```py
pip install -U git+https://github.com/cedriclmao/py_discord_db_management
```
2. Create a new command for your discord Bot and create a `database` object inside that. Make sure to fill out your own credentials.
3. Call `create_db_management` and pass the `database` object as the parameter and return your **embed** & **view** 
4. Use the returned embed & view and attach them to your message
```py
import py_discord_db_management
from py_discord_db_management.classes.database import Database
from py_discord_db_management.dbpyman import create_db_management

@bot.command()
@commands.is_owner() # making only the owner able to use the command
async def dbmanagement(ctx: commands.Context):

    database = Database(
      host='db_host',
      user='db_user',
      password='db_password',
      port=3306,
      database_name='db_name',
      charset='utf8mb4'
    )

    embed, view = create_db_management(database)

    await ctx.send(embed=embed, view=view)   
```


### Advanced usage
The framework features various methodes to further customize the UI & behavior of your data management process.

#### Hide certain tables from the embed
In general the framework will attach all tables as buttons to the view.<br>
You can prevent that by using

```py
database = Database(...)
database.set_table_hidden('MyTableName')
database.set_table_hidden('MySecondTableName')

embed, view = dbpyman.create_db_management(database)
```

#### Hide certain columns from a table
In general the framework will generate all columns for the modal when adding data however<br>
You can prevent that by using

```py
database = Database(...)
database.set_column_hidden('MyTableName', 'MyColumnName')
database.set_column_hidden('MySecondTableName', 'MySecondColumnName')

embed, view = dbpyman.create_db_management(database)
```

#### Set a default value for a column
This will set a **default value** for that specific column. When **adding data** to a table, you'll see the **default value** as the input preview.
This will also allow you to *skip* the insertion of those specific column input fields and simply use the assigned **default value** when that input field is empty ( even if the table is marked as `NOT NULL` ).
```py
database = Database(...)
database.set_column_default_value('MyTableName', 'MyColumnName', 0)
database.set_column_default_value('MySecondTableName', 'MySecondColumnName', 'Banana')

embed, view = dbpyman.create_db_management(database)
```

### Contribute
Feel free to contribute to the project, it's open source.<br>
It's probably possible to *not only* support MySQL and work with inheritance to allow other database types.

<!-- MARKDOWN LINKS & IMAGES -->
[python]: https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white
[mysql]: https://img.shields.io/badge/MySQL-00000F?style=for-the-badge&logo=mysql&logoColor=white
[mysql-url]: https://www.mysql.com/
[python-url]: https://www.python.org/
