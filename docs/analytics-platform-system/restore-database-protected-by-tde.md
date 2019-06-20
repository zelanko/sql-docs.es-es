---
title: Restaurar una base de datos protegida por TDE - almacenamiento de datos paralelos | Microsoft Docs
description: Siga estos pasos para restaurar una base de datos se cifra mediante cifrado de datos transparente en Analytics Platform System Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: a791d4110dc70c506025f8f11fb06b9ba2e5dcb3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63157015"
---
# <a name="restore-a-database-protected-by-tde-in-parallel-data-warehouse"></a>Restaurar una base de datos protegida por TDE en almacenamiento de datos paralelos
Siga estos pasos para restaurar una base de datos se cifra mediante cifrado de datos transparente.  
  
El [utilizando el cifrado de datos transparente](transparent-data-encryption.md#using-tde) ejemplo tiene código para habilitar TDE en el `AdventureWorksPDW2012` base de datos. El código siguiente continúa ese ejemplo, mediante la creación de una copia de seguridad de la base de datos en el dispositivo de Analytics Platform System (APS) original y, a continuación, restaurar el certificado y la base de datos en otro dispositivo.  
  
El primer paso es crear una copia de seguridad de la base de datos de origen.  
  
```sql  
BACKUP DATABASE AdventureWorksPDW2012   
TO DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
Prepare el nuevo SQL Server PDW para TDE mediante la creación de una clave maestra, habilitar el cifrado y crear una credencial de red.  
  
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
  
Los dos últimos pasos volver a crear el certificado mediante el uso de las copias de seguridad de la versión original de SQL Server PDW. Use la contraseña que usó cuando creó la copia de seguridad del certificado.  
  
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
[RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)
  
