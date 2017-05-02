```
-- Create tables
CREATE TABLE pets (
	id SERIAL PRIMARY KEY,
	name VARCHAR(40),
	breed VARCHAR(40),
	color VARCHAR(40)
);

CREATE TABLE visits (
	id SERIAL PRIMARY KEY,
	check_in TIMESTAMP,
	check_out TIMESTAMP,
	pet_id INT REFERENCES pets(id)
);

CREATE TABLE owners (
	id SERIAL PRIMARY KEY,
	first_name VARCHAR(50),
	last_name VARCHAR(50),
	phone_number VARCHAR(20)
);

CREATE TABLE pet_owner (
	pet_id INT REFERENCES pets(id) ON DELETE CASCADE,
	owner_id INT REFERENCES owners(id) ON DELETE CASCADE
);


-- INSERTS
-- Same syntax as always, just more table to manage.

INSERT INTO owners (first_name, last_name, phone_number) VALUES ('bob', 'bobson', '6123456780');
INSERT INTO pets (name, breed, color) VALUES ('fritz', 'amstaff', 'brown');
INSERT INTO pet_owner (pet_id, owner_id) VALUES (1, 1);
INSERT INTO visits (check_in, check_out, pet_id) VALUES (now(), now(), 1);
INSERT INTO visits (check_in, check_out, pet_id) VALUES (now(), now(), 1);
INSERT INTO visits (check_in, check_out, pet_id) VALUES (now(), now(), 2);

--- SELECT
SELECT * FROM pets;

--- SELECT w/ JOINS
SELECT * FROM pets 
JOIN visits ON pets.id = visits.pet_id;

-- * or select specific column names
SELECT owners.first_name, pets.name FROM owners 
JOIN pet_owner ON owners.id = pet_owner.owner_id 
JOIN pets ON pet_owner.pet_id = pets.id
WHERE owners.id = 1;

--- UPDATE
-- Same syntax as always, just more table to manage.

-- DELETE 
-- Same syntax as always, just more table to manage.

DELETE FROM owners WHERE id = 2;

```