---
title: Cifrar una columna de datos | Microsoft Docs
ms.custom: 
ms.date: 05/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- encryption [SQL Server], columns
- cryptography [SQL Server], columns
- column level encryption
- cell level encryption
ms.assetid: 38e9bf58-10c6-46ed-83cb-e2d76cda0adc
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 30791ad9733446f664db1592b95d1ffec5fc9a1b
ms.openlocfilehash: c27f699eb519c1e9a72756c26e8b320869786c6c
ms.contentlocale: es-es
ms.lasthandoff: 06/23/2017

---
# <a name="encrypt-a-column-of-data"></a>Cifrar una columna de datos
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  En este tema se describe cómo cifrar una columna de datos utilizando el cifrado simétrico en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[tsql](../../../includes/tsql-md.md)]. A veces, esto se conoce como cifrado de nivel de columna, o cifrado de nivel de celda.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   [Para cifrar una columna de datos, usando Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Los siguientes permisos son necesarios para realizar los pasos siguientes:  
  
-   Permiso CONTROL en la base de datos.  
  
-   Permiso CREATE CERTIFICATE en la base de datos. Solo los inicios de sesión de Windows, los inicios de sesión de SQL Server y los roles de aplicación pueden poseer certificados. Los grupos y roles no pueden poseer los certificados.  
  
-   Permiso ALTER en la tabla.  
  
-   Algún permiso en la clave y no debe haberse denegado el permiso VIEW DEFINITION.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  

Para usar los ejemplos siguientes deben tener una clave maestra de base de datos. Si la base de datos aún no tiene una clave maestra de base de datos, cree uno mediante la ejecución de la siguiente instrucción que proporcionar la contraseña:   
```  
CREATE MASTER KEY ENCRYPTION BY   
PASSWORD = '<some strong password>';  
```  
Siempre la clave maestra de base de datos de copia de seguridad. Para obtener más información sobre las claves maestras de base de datos, vea [CREATE MASTER KEY &#40; Transact-SQL &#41; ](../../../t-sql/statements/create-master-key-transact-sql.md).

#### <a name="to-encrypt-a-column-of-data-using-a-simple-symmetric-encryption"></a>Para cifrar una columna de datos usando un cifrado simétrico simple  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    
    GO  
  
    CREATE CERTIFICATE Sales09  
       WITH SUBJECT = 'Customer Credit Card Numbers';  
    GO  
  
    CREATE SYMMETRIC KEY CreditCards_Key11  
        WITH ALGORITHM = AES_256  
        ENCRYPTION BY CERTIFICATE Sales09;  
    GO  
  
    -- Create a column in which to store the encrypted data.  
    ALTER TABLE Sales.CreditCard   
        ADD CardNumber_Encrypted varbinary(128);   
    GO  
  
    -- Open the symmetric key with which to encrypt the data.  
    OPEN SYMMETRIC KEY CreditCards_Key11  
       DECRYPTION BY CERTIFICATE Sales09;  
  
    -- Encrypt the value in column CardNumber using the  
    -- symmetric key CreditCards_Key11.  
    -- Save the result in column CardNumber_Encrypted.    
    UPDATE Sales.CreditCard  
    SET CardNumber_Encrypted = EncryptByKey(Key_GUID('CreditCards_Key11')  
        , CardNumber, 1, HashBytes('SHA1', CONVERT( varbinary  
        , CreditCardID)));  
    GO  
  
    -- Verify the encryption.  
    -- First, open the symmetric key with which to decrypt the data.  
  
    OPEN SYMMETRIC KEY CreditCards_Key11  
       DECRYPTION BY CERTIFICATE Sales09;  
    GO  
  
    -- Now list the original card number, the encrypted card number,  
    -- and the decrypted ciphertext. If the decryption worked,  
    -- the original number will match the decrypted number.  
  
    SELECT CardNumber, CardNumber_Encrypted   
        AS 'Encrypted card number', CONVERT(nvarchar,  
        DecryptByKey(CardNumber_Encrypted, 1 ,   
        HashBytes('SHA1', CONVERT(varbinary, CreditCardID))))  
        AS 'Decrypted card number' FROM Sales.CreditCard;  
    GO  
    ```  
  
#### <a name="to-encrypt-a-column-of-data-using-symmetric-encryption-that-includes-an-authenticator"></a>Para cifrar una columna de datos usando el cifrado simétrico que incluye un autenticador  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
  
    CREATE CERTIFICATE HumanResources037  
       WITH SUBJECT = 'Employee Social Security Numbers';  
    GO  
  
    CREATE SYMMETRIC KEY SSN_Key_01  
        WITH ALGORITHM = AES_256  
        ENCRYPTION BY CERTIFICATE HumanResources037;  
    GO  
  
    USE [AdventureWorks2012];  
    GO  
  
    -- Create a column in which to store the encrypted data.  
    ALTER TABLE HumanResources.Employee  
        ADD EncryptedNationalIDNumber varbinary(128);   
    GO  
  
    -- Open the symmetric key with which to encrypt the data.  
    OPEN SYMMETRIC KEY SSN_Key_01  
       DECRYPTION BY CERTIFICATE HumanResources037;  
  
    -- Encrypt the value in column NationalIDNumber with symmetric   
    -- key SSN_Key_01. Save the result in column EncryptedNationalIDNumber.  
    UPDATE HumanResources.Employee  
    SET EncryptedNationalIDNumber = EncryptByKey(Key_GUID('SSN_Key_01'), NationalIDNumber);  
    GO  
  
    -- Verify the encryption.  
    -- First, open the symmetric key with which to decrypt the data.  
    OPEN SYMMETRIC KEY SSN_Key_01  
       DECRYPTION BY CERTIFICATE HumanResources037;  
    GO  
  
    -- Now list the original ID, the encrypted ID, and the   
    -- decrypted ciphertext. If the decryption worked, the original  
    -- and the decrypted ID will match.  
    SELECT NationalIDNumber, EncryptedNationalIDNumber   
        AS 'Encrypted ID Number',  
        CONVERT(nvarchar, DecryptByKey(EncryptedNationalIDNumber))   
        AS 'Decrypted ID Number'  
        FROM HumanResources.Employee;  
    GO  
    ```  
  
 Para obtener más información, vea:  
  
-   [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-certificate-transact-sql.md)  
  
-   [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
-   [ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)  
  
-   [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/open-symmetric-key-transact-sql.md)  
  
  

