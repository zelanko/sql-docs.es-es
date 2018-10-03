---
title: BACKUP CERTIFICATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DUMP_CERTIFICATE_TSQL
- BACKUP CERTIFICATE
- sql13.swb.exportcertificate.f1
- DUMP CERTIFICATE
- BACKUP_CERTIFICATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- encryption [SQL Server], certificates
- decryption [SQL Server], certificates
- exporting certificates
- certificates [SQL Server], exporting
- BACKUP CERTIFICATE statement
- backing up certificates [SQL Server]
- decryption [SQL Server]
- cryptography [SQL Server], certificates
ms.assetid: 509b9462-819b-4c45-baae-3d2d90d14a1c
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: aada31cd31c60c4c0a4cc23ea90f057c0b64f312
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47755989"
---
# <a name="backup-certificate-transact-sql"></a>BACKUP CERTIFICATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdbmi-asdw-pdw-md.md)]

  Exporta un certificado a un archivo.  
  
 ![Icono de vínculo](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server  
  
BACKUP CERTIFICATE certname TO FILE = 'path_to_file'  
    [ WITH PRIVATE KEY   
      (   
        FILE = 'path_to_private_key_file' ,  
        ENCRYPTION BY PASSWORD = 'encryption_password'   
        [ , DECRYPTION BY PASSWORD = 'decryption_password' ]   
      )   
    ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
BACKUP CERTIFICATE certname TO FILE ='path_to_file'  
      WITH PRIVATE KEY   
      (   
        FILE ='path_to_private_key_file',  
        ENCRYPTION BY PASSWORD ='encryption_password'   
      )   
```  
  
## <a name="arguments"></a>Argumentos  
 *path_to_file*  
 Especifica la ruta de acceso completa, incluido el nombre de archivo, al archivo en el que se almacenará el certificado. Esta ruta de acceso puede ser una ruta de acceso local o una ruta UNC a una ubicación de red. La ruta de acceso predeterminada es la carpeta DATA de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *path_to_private_key_file*  
 Especifica la ruta de acceso completa, incluido el nombre de archivo, al archivo en el que se almacenará la clave privada. Esta ruta de acceso puede ser una ruta de acceso local o una ruta UNC a una ubicación de red. La ruta de acceso predeterminada es la carpeta DATA de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

> [!IMPORTANT]
> Azure SQL Database no admite la copia de seguridad de un certificado a un archivo.

  
 *encryption_password*  
 Es la contraseña que se utiliza para cifrar la clave privada antes de escribir la clave en el archivo de copia de seguridad. La contraseña se somete a comprobaciones de complejidad.  
  
 *decryption_password*  
 Es la contraseña que se utiliza para descifrar la clave privada antes de realizar una copia de seguridad de la clave. Este argumento no es necesario si el certificado está cifrado con la clave maestra. 
  
## <a name="remarks"></a>Notas  
 Si la clave privada se cifra con una contraseña en la base de datos, es necesario especificar la contraseña de descifrado.  
  
 Para realizar una copia de seguridad de la clave privada en un archivo es necesario el cifrado. La contraseña utilizada para proteger el certificado no es la misma que la usada para cifrar la clave privada del certificado.  
  
 Para restaurar la copia de seguridad de un certificado utilice la instrucción [CREATE CERTIFICATE](../../t-sql/statements/create-certificate-transact-sql.md).
 
 Al realizar una copia de seguridad, los archivos se agregan a la lista de control de acceso de la cuenta de servicio de la instancia de SQL Server. Si es necesario restaurar el certificado en un servidor que se ejecuta en otra cuenta, deberá ajustar los permisos en los archivos para que la nueva cuenta pueda leerlos. 
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso CONTROL en el certificado y conocimiento de la contraseña que se utiliza para cifrar la clave privada. Si solo se hace una copia de seguridad de la parte pública del certificado, este comando necesita algún permiso en el certificado y que el llamador no haya denegado el permiso VIEW en el certificado.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-exporting-a-certificate-to-a-file"></a>A. Exportar un certificado a un archivo  
 El siguiente ejemplo exporta un certificado a un archivo.  
  
```  
BACKUP CERTIFICATE sales05 TO FILE = 'c:\storedcerts\sales05cert';  
GO  
```  
  
### <a name="b-exporting-a-certificate-and-a-private-key"></a>B. Exportar un certificado y una clave privada  
 En el siguiente ejemplo, la clave privada del certificado del que se realiza una copia de seguridad se cifra con la contraseña `997jkhUbhk$w4ez0876hKHJH5gh`.  
  
```  
BACKUP CERTIFICATE sales05 TO FILE = 'c:\storedcerts\sales05cert'  
    WITH PRIVATE KEY ( FILE = 'c:\storedkeys\sales05key' ,   
    ENCRYPTION BY PASSWORD = '997jkhUbhk$w4ez0876hKHJH5gh' );  
GO  
```  
  
### <a name="c-exporting-a-certificate-that-has-an-encrypted-private-key"></a>C. Exportar un certificado con una clave privada cifrada  
 En el siguiente ejemplo, la clave privada del certificado se cifra en la base de datos. La clave privada debe descifrarse con la contraseña `9875t6#6rfid7vble7r`. Cuando se guarda el certificado en el archivo de copia de seguridad, la clave privada se cifra con la contraseña `9n34khUbhk$w4ecJH5gh`.  
  
```  
BACKUP CERTIFICATE sales09 TO FILE = 'c:\storedcerts\sales09cert'   
    WITH PRIVATE KEY ( DECRYPTION BY PASSWORD = '9875t6#6rfid7vble7r' ,  
    FILE = 'c:\storedkeys\sales09key' ,   
    ENCRYPTION BY PASSWORD = '9n34khUbhk$w4ecJH5gh' );  
GO  
```  
  
## <a name="see-also"></a>Ver también  
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)  
  
  

