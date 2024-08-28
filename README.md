# Database-queries

This is an assignment from school where we are supposed to make queries in a database


Nr.	SQL-Code

A01	SELECT Name , Vorname, PLZ , ORT , STRASSE
FROM Mitarbeiter
ORDER BY PLZ;

A02	SELECT Mitarbeiter.Name, Mitarbeiter.Vorname, Mitarbeiter.Strasse, Mitarbeiter.Plz, Mitarbeiter.Ort, Mitarbeiter.Telefon, Mitarbeiter.Geschlecht, Mitarbeiter.Eingestellt
FROM Mitarbeiter
ORDER BY Mitarbeiter.Eingestellt DESC;

A03	SELECT Name, Vorname, Strasse, Plz, Ort, Telefon, Geschlecht, Eingestellt
FROM Mitarbeiter
WHERE Eingestellt=#2008-06-01#;

A04	SELECT Name, Vorname, Strasse, Plz, Ort, Telefon, Geschlecht, Eingestellt
FROM Mitarbeiter
WHERE Eingestellt<#2008-01-01#;

A05	SELECT ID_MITARB, SUM(AUFTRAGSWERT) AS GESAMT_AUFTRAGSWERT
FROM Projekt
WHERE STORNIERT = 0
GROUP BY ID_MITARB;

A06	SELECT Geschlecht, COUNT(*) AS Anzahl
FROM Mitarbeiter
GROUP BY Geschlecht;

A07	SELECT Name, Vorname 
FROM Mitarbeiter INNER JOIN Projekt ON Mitarbeiter.ID_MITARB = Projekt.ID_MITARB
ORDER BY Name, Vorname ASC;

A08	SELECT ID_PROJ, Bezeichnung, Beginn, Ende 
FROM Projekt
ORDER BY Beginn ASC;

A09	SELECT DISTINCT Eingestellt 
FROM Mitarbeiter 
ORDER BY Eingestellt ASC;

A10	SELECT ID_PROJ, Bezeichnung, Auftragswert 
FROM Projekt
WHERE Auftragswert >= 20000 AND storniert = TRUE 
ORDER BY Auftragswert DESC;

A11	SELECT ID_PROJ, Bezeichnung, Auftragswert 
FROM Projekt 
WHERE Auftragswert BETWEEN 20000 AND 50000 
ORDER BY Auftragswert ASC;

A12	SELECT Name, Vorname, Ort
FROM Mitarbeiter
WHERE NOT Ort = 'Köln'
ORDER BY Name, Vorname;

A13	SELECT Name, Vorname, Zeitanteil
FROM Mitarbeiter INNER JOIN ProjektMitarbeiter ON Mitarbeiter.ID_MITARB = ProjektMitarbeiter.ID_MITARB 
ORDER BY Name, Vorname ASC;

A14	SELECT NAME , VORNAME , Zeitanteil , Bezeichnung
FROM ((Mitarbeiter  
INNER JOIN Projekt ON Mitarbeiter.ID_MITARB = Projekt.ID_MITARB)
INNER JOIN ProjektMitarbeiter ON ProjektMitarbeiter.ID_MITARB = PROJEKT.ID_MITARB)
ORDER BY Name , Vorname;

A15	SELECT *
FROM Mitarbeiter
WHERE GESCHLECHT = 'w';

A16	SELECT *
FROM PROJEKT
WHERE AUFTRAGSWERT >=20000;

A17	SELECT *
FROM Mitarbeiter
WHERE NAME > 'A*'  < 'MEIER';

A18	SELECT * 
FROM Projekt
WHERE isNULL(BEZAHLT) AND Storniert = 0;

A19	SELECT *
FROM Mitarbeiter
WHERE ID_MITARB LIKE '?0*';

A20	SELECT ID_PROJ , BEZEICHNUNG , AUFTRAGSWERT , Auftragswert / 1000 AS Auftragswert_in_1000€ , BEZAHLT , BEGINN , ENDE , STORNIERT , ID_MITARB
FROM Projekt;

A21	SELECT  BEZEICHNUNG ,  COUNT(ProjektMitarbeiter.ID_MITARB) AS Anzahl_Mitarbeiter
FROM  Projekt
INNER JOIN ProjektMitarbeiter ON Projekt.ID_PROJ = ProjektMitarbeiter.ID_PROJ
GROUP BY Projekt.ID_PROJ , BEZEICHNUNG;

A22	SELECT *
FROM Projekt
WHERE AUFTRAGSWERT = 30000;

A23	SELECT *
FROM Projekt
WHERE AUFTRAGSWERT < 20000 OR AUFTRAGSWERT >= 50000;

A24	SELECT *
FROM MITARBEITER
WHERE NAME = ' Schmi??';

A25	SELECT ID_PROJ, BEZEICHNUNG , Auftragswert AS Netto_Auftragswert, Auftragswert * 0.19 AS MWSt, Auftragswert * 1.19 AS Brutto_Auftragswert
FROM Projekt;

A26	SELECT *
FROM Mitarbeiter
WHERE Ort LIKE 'Köln*';

A27	SELECT Mitarbeiter.ID_MITARB, Mitarbeiter.Vorname, Mitarbeiter.Name, SUM(Projekt.AUFTRAGSWERT) AS Auftragswert_nach_Mitarbeiter
FROM Mitarbeiter 
INNER JOIN Projekt ON Mitarbeiter.ID_MITARB = Projekt.ID_MITARB
GROUP BY Mitarbeiter.ID_MITARB, Mitarbeiter.Vorname, Mitarbeiter.Name
ORDER BY Mitarbeiter.ID_MITARB;

A28	SELECT Mitarbeiter.ID_MITARB AS Mitarbeiter_ID, Mitarbeiter.Vorname AS Mitarbeiter_Vorname, Mitarbeiter.Name AS Mitarbeiter_Nachname, COUNT(Kind.ID_KIND) AS Anzahl_Kinder
FROM Mitarbeiter 
INNER JOIN Kind ON Mitarbeiter.ID_MITARB = Kind.ID_MITARB
WHERE Mitarbeiter.ORT = 'Köln'
GROUP BY Mitarbeiter.ID_MITARB, Mitarbeiter.Vorname, Mitarbeiter.Name
ORDER BY Mitarbeiter.ID_MITARB;

A29	UPDATE Projekt
SET ENDE = #20-08-2024# ,  BEZAHLT = 50000
WHERE Bezeichnung = 'Umzug Stein AG';

A30	DELETE *
FROM PROJEKT
WHERE BEZEICHNUNG = "Umrüstung Neumann OHG"; 

A31	INSERT INTO Mitarbeiter
VALUES (811, 'Eversberg', 'Sandra', 'Drosselgasse 7', '28201', 'Bremen', '0421/314159', 'w', #12-01-2024#);

A32	INSERT INTO Projekt 
VALUES (92, 'Kivinan-WLAN', 28000, NULL, #12-10-2024#, NULL, false, 811);

A33	UPDATE MITARBEITER SET NAME='Schnitt-Schmitt'
WHERE VORNAME ='Klaus' AND NAME = 'Schmitt' OR VORNAME ='Hannelore' AND NAME='Schnitt';

s.141 A58	SELECT Ende-Beginn AS Dauer_in_Tagen, *
FROM Projekt
WHERE (((Projekt.[Ende]) Is Not Null));
