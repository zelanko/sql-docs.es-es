---
title: Restaurar una base de datos protegida por TDE - almacenamiento de datos paralelos | Documentos de Microsoft
description: Siga estos pasos para restaurar una base de datos que se cifra mediante el cifrado transparente de los datos en almacenamiento de datos paralelos de sistema de plataforma de análisis.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: a791d4110dc70c506025f8f11fb06b9ba2e5dcb3
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
---
# <a name="restore-a-database-protected-by-tde-in-parallel-data-warehouse"></a>Restaurar una base de datos protegida por TDE en almacenamiento de datos paralelos
Siga estos pasos para restaurar una base de datos que se cifra mediante el cifrado de datos transparente.  
  
El [usar cifrado de datos transparente](transparent-data-encryption.md#using-tde) en el ejemplo se incluye código para habilitar TDE en la `AdventureWorksPDW2012` base de datos. El código siguiente continúa ese ejemplo, crear una copia de seguridad de la base de datos en el dispositivo Analytics Platform System (APS) original y, a continuación, restaurar el certificado y la base de datos en otro dispositivo.  
  
El primer paso es crear una copia de seguridad de la base de datos de origen.  
  
```sql  
BACKUP DATABASE AdventureWorksPDW2012   
TO DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
Preparar el nuevo SQL Server PDW para TDE, cree una clave maestra, habilitar el cifrado y crear una credencial de red.  
  
```sql  
USE master;  
GO  
  
-- Create a database master key in the master database  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>';  
GO  
  
-- Enable encryption for PDW  
EXEC sp_pdw_database_encryption 1;  
GO  
  
EXEC sp_pdw_add_network_credentials 'SECURE_SERVER', '<domain>\<Windows_user>', '<password>';  
```  
  
Los dos últimos pasos volver a crear el certificado mediante el uso de las copias de seguridad de la versión original de SQL Server PDW. Use la contraseña que utilizó cuando creó la copia de seguridad del certificado.  
  
```sql  
-- Create certificate in master  
CREATE CERTIFICATE MyServerCert  
    FROM FILE = '\\SECURE_SERVER\cert\MyServerCert.cer'   
    WITH PRIVATE KEY (FILE = '\\SECURE_SERVER\cert\MyServerCert.key',   
    DECRYPTION BY PASSWORD = '<password>');  
  
RESTORE DATABASE AdventureWorksPDW2012   
    FROM DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
## <a name="see-also"></a>Vea también  
[BASE DE DATOS DE COPIA DE SEGURIDAD](../t-sql/statements/backup-database-parallel-data-warehouse.md)  
[CREATE MASTER KEY](../t-sql/statements/create-master-key-transact-sql.md) 
[sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
[CREAR CERTIFICADO](../t-sql/statements/create-certificate-transact-sql.md)  
[RESTAURAR BASE DE DATOS](../t-sql/statements/restore-database-parallel-data-warehouse.md)
  
