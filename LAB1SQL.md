LAB1SQL
# /** G DEL För Moon Missions **/ 
SELECT [Spacecraft],[Launch date],[Carrier rocket],[Operator],[Mission type]  
INTO SuccessfulMissions
FROM MoonMissions
WHERE Outcome = 'Successful'

SELECT * FROM SuccessfulMissions
GO

 UPDATE SuccessfulMissions   
 SET Operator = LTRIM(RTRIM(Operator))

 GO

 /** G DEL För Users **/ 
 SELECT	[ID], [UserName], [Password], [FirstName], [LastName], [Email], [Phone], 		
 CONCAT([FirstName],' ', [LastName])
		AS 'Name',
		CASE
			WHEN (SUBSTRING(ID, 10, 1) % 2 ) = 1
			THEN 'Male'
			ELSE 'Female'
		END AS 'Gender'
INTO NewUsers 
FROM Users;

GO

SELECT [UserName], COUNT([UserName]) AS 'Amount of duplicates'
FROM NewUsers
GROUP BY [UserName]
HAVING COUNT([UserName] ) > 1

GO

SET ANSI_WARNINGS  OFF;
UPDATE NewUsers SET [UserName] = 'sigpet01' WHERE [ID] = '630303-4894'
UPDATE NewUsers SET [UserName] = 'sigpet02' WHERE [ID] = '811008-5301'
UPDATE NewUsers SET [UserName] = 'sigpet03' WHERE [ID] = '580802-4175'
UPDATE NewUsers SET [UserName] = 'felber01' WHERE [ID] = '890701-1480'
UPDATE NewUsers SET [UserName] = 'felber02' WHERE [ID] = '880706-3713'
SET ANSI_WARNINGS ON;

GO
DELETE FROM NewUsers WHERE ID < '7' AND Gender = 'Female';

GO

INSERT INTO NewUsers ([ID], [UserName], [password], [FirstName], [LastName], [Email], [Phone], [Name], Gender)
VALUES ('301412-0173', 
'zaki1', 
 CONVERT(nvarchar(28), HASHBYTES('SHA2_512', 'ZakiÄrBäst2021!'), 2), 
'Zakarie', 
'Isse', 
'zakki96@hotmail.com',
'073-213728', 
'Zakarie Isse', 
'Male');

GO
