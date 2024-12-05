# Chapter 8
## 1.1 (Запросить список всех клиентов и количество их заказов.)
```python
import sqlite3

conn = sqlite3.connect('Chinook_Sqlite.sqlite')
cursor = conn.cursor()

cursor.execute('''
SELECT Customer.CustomerId, Customer.FirstName, Customer.LastName, COUNT(Invoice.InvoiceId)
FROM Customer 
JOIN Invoice ON Customer.CustomerId=Invoice.CustomerId
GROUP BY Customer.CustomerId;
''')
a=cursor.fetchall()
for i in a:
    print("Клиент: " + i[1] + ". Позиций: " + str(i[3]))
```
## 1.2 (Найти все треки, которые были выпущены после 2010 года.)
```python
import sqlite3

conn = sqlite3.connect('Chinook_Sqlite.sqlite')
cursor = conn.cursor()
# В таблице нет столбца, который отвечал бы за дату выпуска
cursor.execute('''
SELECT Track.Name
            FROM Track            
''')
a=cursor.fetchall()
for i in a:
    print(i)
```
## 1.3 (Создать представление для отображения общего количества продаж по каждому альбому.)
```python
import sqlite3

conn = sqlite3.connect('Chinook_Sqlite.sqlite')
cursor = conn.cursor()
cursor.execute('''
SELECT Album.Title, COUNT(Track.UnitPrice)
FROM Album 
JOIN Track ON Track.TrackId=InvoiceLine.TrackId 
JOIN InvoiceLine ON Album.AlbumId=Track.AlbumId
  GROUP BY Album.AlbumId;    
''')
a=cursor.fetchall()
for i in a:
    print("Альбом: " + i[0] + ". Продаж: " + str(i[1]))
```
## 2 (ORM)
```python
import sqlite3

# Создание класса для представления альбома
class Album:
    def __init__(self, album_id, title, artist_id):
        self.album_id = album_id
        self.title = title
        self.artist_id = artist_id

    def __repr__(self):
        return f"Album(id={self.album_id}, title='{self.title}', artist_id={self.artist_id})"

# Создание класса для представления исполнителя
class Artist:
    def __init__(self, artist_id, name):
        self.artist_id = artist_id
        self.name = name

    def __repr__(self):
        return f"Artist(id={self.artist_id}, name='{self.name}')"

# Функция для подключения к базе данных
def get_connection(db_file):
    return sqlite3.connect(db_file)

# Функция для получения всех альбомов
def get_all_albums(connection):
    cursor = connection.cursor()
    cursor.execute('''
    SELECT Album.Albumid,Album.Title,Artist.ArtistId
    FROM Album     
    JOIN Artist ON Album.ArtistId = Artist.ArtistId;
    ''')
    a = cursor.fetchall()
    return [Album(album_id, title, artist_id) for album_id, title, artist_id in a]

# Функция для получения исполнителей
def get_all_artists(connection):
    cursor = connection.cursor()
    cursor.execute('''
        SELECT *
        FROM Artist     
        ''')
    a = cursor.fetchall()
    return [Artist(artist_id,name) for artist_id, name in a]

# Функция для получения треков, выпущенных после 2010 года
def get_tracks_after_2010(connection):
    cursor = connection.cursor()
    cursor.execute('''
            SELECT Track.Name
            FROM Track     
            ''')
    a = cursor.fetchall()
    return a

def test():
    db_file = 'Chinook_Sqlite.sqlite'
    connection = get_connection(db_file)
    if connection:
        albums = get_all_albums(connection)
        print("Альбомы:")
        for album in albums:
            print(album)

        artists = get_all_artists(connection)
        print("\nИсполнители:")
        for artist in artists:
            print(artist)

        tracks_after_2010 = get_tracks_after_2010(connection)
        print("\nТреки, выпущенные после 2010 года:")
        for track in tracks_after_2010:
            print(track)

        connection.close()

test()
```
## 3 (CRUD)
```python
import sqlite3

# Создание класса для представления альбома
class Album:
    def __init__(self, album_id, title, artist_id):
        self.album_id = album_id
        self.title = title
        self.artist_id = artist_id

    def __repr__(self):
        return f"Album(id={self.album_id}, title='{self.title}', artist_id={self.artist_id})"

# Функция для подключения к базе данных
def get_connection(db_file):
    return sqlite3.connect(db_file)

# CRUD операции для альбомов

# 1. Создание (Create)
def create_album(connection, title, artist_id):
    cursor = connection.cursor()
    insert_artist_query = '''
    INSERT INTO Album (Title,ArtistId) VALUES (?,?)
    '''
    cursor.execute(insert_artist_query,(title,artist_id))
    connection.commit()

# 2. Чтение (Read)
def read_albums(connection):
    cursor = connection.cursor()
    cursor.execute('''
        SELECT *
        FROM Album     
        ''')
    a = cursor.fetchall()
    return [Album(album_id, title, artist_id) for album_id, title, artist_id in a]


# 3. Обновление (Update)
def update_album(connection, album_id, new_title):
    cursor = connection.cursor()
    update_artist_query = '''
    UPDATE Album
    SET Title = ?
    WHERE AlbumId = ?
    '''
    cursor.execute(update_artist_query,(new_title,album_id))
    connection.commit()


# 4. Удаление (Delete)
def delete_album(connection, album_id):
    cursor = connection.cursor()
    delete_album_query = '''
            DELETE FROM Album WHERE AlbumId = ?
            '''
    cursor.execute(delete_album_query, (album_id,))
    connection.commit()


def test():
    conn = get_connection('Chinook_Sqlite.sqlite')

    artist_id = 1
    album_title = "Тест1"

    create_album(conn, album_title, artist_id)

    albums = read_albums(conn)
    print("Список альбомов:")
    for album in albums:
        print(album)

    if albums != None:
        album_id = albums[0].album_id
        new_title = "Обновленный Альбом"
        update_album(conn, album_id, new_title)
        print(f"Альбом с ID {album_id} обновлен.")

        updated_albums = read_albums(conn)
        print("Список альбомов после обновления:")
        for album in updated_albums:
            print(album)

    if albums != None:
        delete_album(conn, album_id)
        print(f"Альбом с ID {album_id} удален.")

    final_albums = read_albums(conn)
    print("Список альбомов после удаления:")
    for album in final_albums:
        print(album)
    conn.close()

test()
```
