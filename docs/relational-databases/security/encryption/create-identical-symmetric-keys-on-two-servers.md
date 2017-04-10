---
title: "Crear claves sim&#233;tricas id&#233;nticas en dos servidores | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "claves simétricas [SQL Server], crear"
ms.assetid: a13d0b21-a43b-43c0-9c22-7ba8f3d15e80
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# Crear claves sim&#233;tricas id&#233;nticas en dos servidores
  En este tema se describe cómo crear claves simétricas idénticas en dos servidores diferentes de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Para descifrar el texto cifrado, se necesita la clave que se usó para cifrarlo. Cuando el cifrado y el descifrado tienen lugar en una sola base de datos, la clave se almacena en la base de datos y está disponible, según los permisos, tanto para el cifrado como para el descifrado. Pero cuando ambos procesos ocurren en bases de datos diferentes o en servidores diferentes, la clave almacenada en una base de datos no está disponible para utilizarla en la segunda base de datos.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   [Para crear claves simétricas idénticas en dos servidores diferentes, mediante Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Cuando se crea una clave simétrica, se debe cifrar mediante uno de los siguientes métodos: certificado, contraseña, clave simétrica, clave asimétrica o PROVIDER. La clave puede tener más de un cifrado de cada tipo. En otras palabras, una misma clave simétrica puede cifrarse con varios certificados, contraseñas, claves simétricas y claves asimétricas a la vez.  
  
-   Si se utiliza una contraseña para cifrar una clave simétrica, en lugar de la clave pública de la clave maestra de base de datos, se utiliza el algoritmo de cifrado TRIPLE DES. Por ello, las claves creadas con un algoritmo de cifrado seguro, como AES, se protegen mediante un algoritmo menos seguro.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Necesita el permiso ALTER ANY SYMMETRIC KEY para la base de datos. Si se especifica la cláusula AUTHORIZATION, es necesario el permiso IMPERSONATE para el usuario de base de datos o el permiso ALTER para el rol de aplicación. Si el cifrado se realiza mediante una clave asimétrica o un certificado, es necesario el permiso VIEW DEFINITION para el certificado o en la clave asimétrica. Solo los inicios de sesión de Windows, los inicios de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y los roles de aplicación pueden poseer claves simétricas. Los grupos y roles no pueden poseer claves simétricas.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### Para crear claves simétricas idénticas en dos servidores diferentes  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Cree una clave ejecutando las siguientes instrucciones, CREATE MASTER KEY, CREATE CERTIFICATE y CREATE SYMMETRIC KEY.  
  
    ```  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'My p@55w0Rd';  
    GO  
    CREATE CERTIFICATE [cert_keyProtection] WITH SUBJECT = 'Key Protection';  
    GO  
    CREATE SYMMETRIC KEY [key_DataShare] WITH  
        KEY_SOURCE = 'My key generation bits. This is a shared secret!',  
        ALGORITHM = AES_256,   
        IDENTITY_VALUE = 'Key Identity generation bits. Also a shared secret'  
        ENCRYPTION BY CERTIFICATE [cert_keyProtection];  
    GO  
    ```  
  
4.  Conéctese a una instancia de servidor independiente, abra otra ventana de consulta y ejecute las instrucciones SQL anteriores para crear la misma clave en el segundo servidor.  
  
5.  Pruebe las claves ejecutando primero la instrucción OPEN SYMMETRIC KEY y la instrucción SELECT después en el primer servidor.  
  
    ```  
    OPEN SYMMETRIC KEY [key_DataShare]   
        DECRYPTION BY CERTIFICATE cert_keyProtection;  
    GO  
    SELECT encryptbykey(key_guid('key_DataShare'), 'MyData' )  
    GO  
    -- For example, the output might look like this: 0x2152F8DA8A500A9EDC2FAE26D15C302DA70D25563DAE7D5D1102E3056CE9EF95CA3E7289F7F4D0523ED0376B155FE9C3  
    ```  
  
6.  En el segundo servidor, pegue el resultado de la instrucción SELECT previa en el siguiente código como el valor de `@blob` y ejecute el siguiente código para comprobar que la clave duplicada pueda descifrar el texto cifrado.  
  
    ```  
    OPEN SYMMETRIC KEY [key_DataShare]   
        DECRYPTION BY CERTIFICATE cert_keyProtection;  
    GO  
    DECLARE @blob varbinary(8000);  
    SET @blob = SELECT CONVERT(varchar(8000), decryptbykey(@blob));  
    GO  
    ```  
  
7.  Cierre la clave simétrica en ambos servidores.  
  
    ```  
    CLOSE SYMMETRIC KEY [key_DataShare];  
    GO  
    ```  
  
 Para obtener más información, vea:  
  
-   [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-master-key-transact-sql.md)  
  
-   [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-certificate-transact-sql.md)  
  
-   [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
-   [ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbykey-transact-sql.md)  
  
-   [DECRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/decryptbykey-transact-sql.md)  
  
-   [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/open-symmetric-key-transact-sql.md)  
  
  