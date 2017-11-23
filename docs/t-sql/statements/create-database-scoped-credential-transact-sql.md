---
title: "CREAR CREDENCIAL en el ámbito de base de datos (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 02/27/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATABASE SCOPED CREDENTIAL
- DATABASE_SCOPED_CREDENTIAL_TSQL
- SCOPED_TSQL
- CREATE_DATABASE_SCOPED_CREDENTIAL
- CREATE_DATABASE_SCOPED_CREDENTIAL_TSQL
- SCOPED_CREDENTIAL_TSQL
- SCOPED_CREDENTIAL
helpviewer_keywords:
- DATABASE SCOPED CREDENTIAL statement
- credentials [SQL Server], DATABASE SCOPED CREDENTIAL statement
ms.assetid: fe830577-11ca-44e5-953b-2d589d54d045
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4dff68e0c4e50a755ec058602bd61208ccd9b7de
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="create-database-scoped-credential-transact-sql"></a>CREAR CREDENCIAL en el ámbito de base de datos (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Crea una credencial de base de datos. Una credencial de base de datos no está asignada a un usuario de base de datos o de inicio de sesión de servidor. La credencial se utiliza la base de datos para el acceso a la ubicación externa siempre que la base de datos está realizando una operación que requiere acceso.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
 
CREATE DATABASE SCOPED CREDENTIAL credential_name   
WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *credential_name*  
 Especifica el nombre de la credencial de ámbito de la base de datos que se va a crear. *credential_name* no se puede iniciar con el signo de número (#). Las credenciales del sistema comienzan por ##.  
  
 IDENTIDAD **='***identity_name***'**  
 Especifica el nombre de la cuenta que se utilizará para conectarse fuera del servidor. Para importar un archivo de almacenamiento de blobs de Azure, debe ser el nombre de identidad `SHARED ACCESS SIGNATURE`.  Para obtener más información acerca de las firmas de acceso compartido, consulte [firmas de acceso compartido (SAS) usando](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).  
  
 SECRETO **='***secreto***'**  
 Especifica el secreto necesario para la autenticación de salida. `SECRET`es necesario para importar un archivo de almacenamiento de blobs de Azure.   
>  [!WARNING]
>  El valor de clave de SAS debería comenzar con un '?' (signo de interrogación). Cuando se usa la clave SAS, debe quitar el interlineado '?'. En caso contrario, podrían bloquearse sus esfuerzos.  
  
## <a name="remarks"></a>Comentarios  
 Una credencial de ámbito de la base de datos es un registro que contiene la información de autenticación necesaria para conectarse a un recurso fuera de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La mayoría de las credenciales incluyen un usuario y una contraseña de Windows.  
  
 Antes de crear una base de datos de credencial con ámbito, la base de datos debe tener una clave maestra para proteger las credenciales. Para obtener más información, vea [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md).  
  
 Si IDENTITY es un usuario de Windows, el secreto puede ser la contraseña. El secreto se cifra usando la clave maestra de servicio. Si se vuelve a generar la clave maestra de servicio, el secreto se vuelve a cifrar con la nueva clave maestra de servicio.  
   
 Información sobre las credenciales de ámbito de la base de datos está visible en el [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) vista de catálogo.  
  
 
 Hereare credenciales con ámbito de algunas aplicaciones de base de datos:  
  
- [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]utiliza una credencial de ámbito de la base de datos para tener acceso a almacenamiento de blobs de Azure no público o clústeres de Hadoop protegido con Kerberos con PolyBase. Para obtener más información, consulte [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md).  

- [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]utiliza una credencial de ámbito de la base de datos al almacenamiento de blobs de Azure no públicos de acceso con PolyBase. Para obtener más información, consulte [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md).
  
- [!INCLUDE[ssSDS](../../includes/sssds-md.md)]usa las credenciales de ámbito para su característica de consulta global de la base de datos. Esto es la capacidad para consultar en varias particiones de base de datos.  
  
- [!INCLUDE[ssSDS](../../includes/sssds-md.md)]usa las credenciales de ámbito de la base de datos para escribir archivos de eventos extendidos en el almacenamiento de blobs de Azure.  
  
- [!INCLUDE[ssSDS](../../includes/sssds-md.md)]usa las credenciales de ámbito para grupos elásticos de la base de datos. Para obtener más información, vea [dominar drástico crecimiento con bases de datos elásticas](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)  

- [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) y [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) credenciales para tener acceso a datos desde el almacenamiento de blobs de Azure con ámbito de base de datos de uso. Para obtener más información, consulte [ejemplos de forma masiva acceso a los datos en almacenamiento de blobs de Azure](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md). 
  
## <a name="permissions"></a>Permissions  
 Requiere **CONTROL** permiso en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
### <a name="a-creating-a-database-scoped-credential-for-your-application"></a>A. Crear una base de datos con ámbito de credencial para la aplicación.
 En el ejemplo siguiente se crea la credencial de ámbito de la base de datos denominada `AppCred`. La credencial de ámbito de la base de datos contiene el usuario de Windows `Mary5` y una contraseña.  
  
```tsql  
-- Create a db master key if one does not already exist, using your own password.  
CREATE MASTER KEY ENCRYPTION BY PASSWORD='<EnterStrongPasswordHere>';  
  
-- Create a database scoped credential.  
CREATE DATABASE SCOPED CREDENTIAL AppCred WITH IDENTITY = 'Mary5',   
    SECRET = '<EnterStrongPasswordHere>';  
GO  
```  

### <a name="b-creating-a-database-scoped-credential-for-a-shared-access-signature"></a>B. Crear una base de datos con ámbito de credencial para la firma de acceso compartido.   
En el ejemplo siguiente se crea una credencial de ámbito de la base de datos que puede usarse para crear un [origen de datos externo](../../t-sql/statements/create-external-data-source-transact-sql.md), que puede realizar las operaciones masivas, como [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) y [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md). No se puede usar firmas de acceso compartido con PolyBase en SQL Server, puntos de acceso o almacenamiento de datos de SQL.
```tsql
CREATE DATABASE SCOPED CREDENTIAL MyCredentials  
WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
SECRET = 'QLYMgmSXMklt%2FI1U6DcVrQixnlU5Sgbtk1qDRakUBGs%3D';
```
  
### <a name="c-creating-a-database-scoped-credential-for-polybase-connectivity-to-azure-data-lake-store"></a>C. Crear una base de datos con ámbito de credencial para la conectividad de PolyBase a almacén de Azure Data Lake.  
En el ejemplo siguiente se crea una credencial de ámbito de la base de datos que puede usarse para crear un [origen de datos externo](../../t-sql/statements/create-external-data-source-transact-sql.md), que puede utilizarse por PolyBase en el almacén de datos de SQL Azure.

Almacén de Azure Data Lake usa una aplicación de Azure Active Directory para la autenticación de servicio a servicio.
Por favor, [crear una aplicación AAD](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory) y documentar el client_id, la OAuth_2.0_Token_EndPoint y la clave antes de intentar crear una credencial de ámbito de la base de datos.

```tsql
CREATE DATABASE SCOPED CREDENTIAL ADL_User
WITH
    IDENTITY = '<client_id>@\<OAuth_2.0_Token_EndPoint>'
    SECRET = '<key>'
;
```  
  
  
  
## <a name="more-information"></a>Más información  
 [Credenciales &#40; motor de base de datos &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [ALTER CREDENTIAL en el ámbito de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [ELIMINAR CREDENCIALES en el ámbito de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [Sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
