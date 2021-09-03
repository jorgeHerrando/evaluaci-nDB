# evaluacionDB
Diseño base de datos relacional

Hola Mati y Juan.

No sabía bien si podíamos entregar el archivo del dump o entregar uno hecho desde cero.

Hice uno también desde 0, que funcionó igualmente. Tiene menos código, pero una vez creada la DB y hacer un dump para probar, el código es idéntico al posteado.

Se lo dejo a continuación: 

CREATE TABLE users (
	id INT NOT NULL AUTO_INCREMENT,
	first_name VARCHAR(100) NOT NULL,
	last_name VARCHAR(100) NOT NULL,
	email VARCHAR(100) NOT NULL,
	PRIMARY KEY (id),
	UNIQUE KEY (email)
)

INSERT INTO users
VALUES (1, 'jorge', 'herrando', 'jorge@gmail.com'),
(2, 'pablo', 'motos', 'pablo@gmail.com'),
(3, 'dani', 'rovira', 'dani@gmail.com'),
(4, 'dani', 'mateo', 'dmateo@gmail.com'),
(5, 'mario', 'casas', 'mario@gmail.com'),
(6, 'nuria', 'roca', 'nuria@gmail.com'),
(7, 'esther', 'pueyo', 'esther@gmail.com'),
(8, 'candela', 'peña', 'candela@gmail.com'), 
(9, 'rocío', 'carrasco', 'rocio@gmail.com'),
(10, 'lali', 'espósito', 'lali@gmail.com')

CREATE TABLE notes (
	id INT NOT NULL AUTO_INCREMENT,
	title VARCHAR(100) NOT NULL,
	createdAt TIMESTAMP NOT NULL,
	updatedAt timestamp DEfault '2000-01-01 00:00:00',
	description TEXT NOT NULL,
	canDelete TINYINT NOT NULL,
	user_id INT NOT NULL,
	PRIMARY KEY (id),
	FOREIGN KEY (user_id) REFERENCES users(id)
)

INSERT INTO notes
VALUES (1, 'trabajo', '2010-01-19 03:14:07', NULL, 'Los pendientes a realizar en el trabajo', 1, 1),
(2, 'compras', '2011-01-19 03:14:07', NULL, 'Tomate, cebolla', 1, 6),
(3, 'música', '2012-01-19 03:14:07', NULL,'C.Tangana - El Madrileño', 1, 4),
(4, 'passwords', '2013-01-19 03:14:07', NULL,'Banco - XXXXXXX', 0, 4),
(5, 'comidas', '2014-01-19 03:14:07', NULL,'Curry verde - 2 tomates, 1 cebolla...', 1, 6),
(6, 'películas', '2015-01-19 03:14:07', NULL,'Harry Potter', 1, 2),
(7, 'cumpleaños', '2016-01-19 03:14:07', NULL,'Mamá - 03/09, Papá - 01/01', 0, 10),
(8, 'deportes', '2017-01-19 03:14:07', NULL,'tenis, frontón, fútbol', 1, 9), 
(9, 'artistas', '2018-01-19 03:14:07', NULL,'Micheal Jackson', 1, 7),
(10, 'videojuegos', '2019-01-19 03:14:07', NULL,'Final Fantasy', 1, 6)

CREATE TABLE categories (
	id INT NOT NULL AUTO_INCREMENT,
	title VARCHAR(100) NOT NULL,
	PRIMARY KEY (id),
	UNIQUE KEY (title)
)

INSERT INTO categories
VALUES (1, 'aficiones'),
(2, 'seguridad'),
(3, 'planes'),
(4, 'cumpleaños'),
(5, 'trabajo'),
(6, 'deportes'),
(7, 'nutrición'),
(8, 'música'), 
(9, 'televisión'),
(10, 'consejos')

CREATE TABLE note_category (
	id INT NOT NULL AUTO_INCREMENT,
	note_id INT NOT NULL,
	category_id INT NOT NULL,
	PRIMARY KEY (id),
	FOREIGN KEY (note_id) REFERENCES notes(id),
	FOREIGN KEY (category_id) REFERENCES categories(id)
)

INSERT INTO note_category
VALUES (1, 2, 3),
(2, 5, 7),
(3, 6, 1),
(4, 6, 9),
(5, 1, 5),
(6, 4, 2),
(7, 4, 5),
(8, 10, 1), 
(9, 10, 9),
(10, 8, 6)
