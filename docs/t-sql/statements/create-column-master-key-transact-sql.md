---
title: CREAR claves maestras de columna (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/18/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SQL13.SWB.NEWCOLUMNMASTERKEYDEF.GENERAL.F1
- SQL13.SWB.COLUMNMASTERKEYDEF.GENERAL.F1
- CREATE COLUMN MASTER KEY
- COLUMN MASTER KEY
- CREATE_COLUMN_MASTER_KEY_TSQL
- COLUMN_MASTER_KEY_TSQL
- SQL13.SWB.NEWCOLUMNMASTERKEY.GENERAL.F1
- SQL13.SWB.COLUMNMASTERKEY.GENERAL.F1
dev_langs:
- TSQL
helpviewer_keywords:
- column master key definition
- column master key, create
- CREATE COLUMN MASTER KEY statement
- Always Encrypted, create column master key
ms.assetid: f8926b95-e146-4e3f-b56b-add0c0d0a30e
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 871acb46898a9a62b25062f69d4e51bf28658f06
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-column-master-key-transact-sql"></a>CREATE COLUMN MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Crea un objeto de metadatos de la clave maestra de columna en una base de datos. Una entrada de metadatos de clave maestra de columna que representa una clave almacenada en un almacén de claves externo, que se usa para proteger (cifrar) claves de cifrado de columna cuando se usa el [Always Encrypted &#40; motor de base de datos &#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md) característica. Permitir varias claves maestras de columna para la rotación de claves; cambiar periódicamente la clave para mejorar la seguridad. Puede crear una clave maestra de columna en un almacén de claves y su objeto de metadatos correspondiente en la base de datos mediante el Explorador de objetos en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o PowerShell. Para obtener más información, consulte [información general de administración de claves para Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
CREATE COLUMN MASTER KEY key_name   
    WITH (  
        KEY_STORE_PROVIDER_NAME = 'key_store_provider_name',  
        KEY_PATH = 'key_path'   
         )   
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *key_name*  
 Es el nombre por el que se conocerá la clave maestra de columna en la base de datos.  
  
 *key_store_provider_name*  
 Especifica el nombre de un proveedor de almacén de claves, que es un componente de software de cliente que encapsula un almacén de claves que contiene la clave maestra de columna. Un controlador cliente habilitado para Always Encrypted utiliza un nombre de proveedor de almacén de claves para buscar un proveedor de almacén de claves en el registro del controlador de proveedores de almacén de claves. El controlador usa el proveedor para descifrar las claves de cifrado de columna, protegidas por una clave maestra de columna almacenada en el almacén de claves subyacente. Un valor de texto simple de la clave de cifrado de columna, a continuación, se utiliza para cifrar los parámetros de consulta, correspondiente a las columnas de la base de datos cifrada, o para descifrar los resultados de la consulta de las columnas cifradas.  
  
 Las bibliotecas de controlador de Always Encrypted habilitado cliente incluyen proveedores de almacén de claves para los almacenes de claves populares.   
  
Un conjunto de proveedores disponibles dependen del tipo y la versión del controlador de cliente. Consulte la documentación de Always Encrypted para controladores determinados:

[Desarrollar aplicaciones mediante Always Encrypted con el proveedor de .NET Framework para SQL Server](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)


La siguiente tablas captura los nombres de proveedores del sistema:  
  
|Nombre del proveedor de almacén de claves|Almacén de claves subyacente|  
    |-----------------------------|--------------------------|
    |'MSSQL_CERTIFICATE_STORE'|Almacén de certificados de Windows| 
    |'MSSQL_CSP_PROVIDER'|Un almacén, como un módulo de seguridad de hardware (HSM), que es compatible con Microsoft CryptoAPI.|
    |'MSSQL_CNG_STORE'|Un almacén, como un módulo de seguridad de hardware (HSM), que es compatible con Cryptography API: Next Generation.|  
    |'Azure_Key_Vault'|Vea [Introducción a almacén de claves de Azure](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)|  
  

 Puede implementar un proveedor de almacén de claves personalizados, para almacenar claves maestras de columna en un almacén para el que no hay ninguna clave integrada almacene proveedor del controlador cliente habilitado para Always Encrypted.  Tenga en cuenta que los nombres de proveedores de almacén de claves personalizado no pueden comenzar con 'MSSQL_', que es un prefijo reservado para [!INCLUDE[msCoName](../../includes/msconame-md.md)] proveedores de almacén de claves. 

  
 key_path  
 Almacenar la ruta de acceso de la clave en la clave maestra de columna. La ruta de acceso de clave debe ser válido en el contexto de cada aplicación de cliente que se espera para cifrar o descifrar los datos almacenados en una columna (indirectamente) protegida por la clave maestra de columna que se hace referencia y la aplicación cliente necesita para tener acceso a la clave. El formato de la ruta de acceso de clave es específico del proveedor de almacén de claves. En la lista siguiente describe el formato de las rutas de acceso de claves para los proveedores de almacén de claves de sistema de Microsoft determinados.  
  
-   **Nombre del proveedor:** MSSQL_CERTIFICATE_STORE  
  
     **Formato de clave de la ruta de acceso:** *NombreAlmacenamientoCertificados*/*CertificateStoreLocation*/*CertificateThumbprint*  
  
     Donde:  
  
     *CertificateStoreLocation*  
     Ubicación del almacén de certificados, que debe ser el equipo Local o el usuario actual. Para obtener más información, consulte [almacenes de certificados del usuario actual y el equipo Local](https://msdn.microsoft.com/library/windows/hardware/ff548653.aspx).  
  
     *CertificateStore*  
     Nombre del almacén de certificados, por ejemplo "My".  
  
     *CertificateThumbprint*  
     Huella digital del certificado.  
  
     **Ejemplos:**  
  
    ```  
    N'CurrentUser/My/BBF037EC4A133ADCA89FFAEC16CA5BFA8878FB94'  
  
    N'LocalMachine/My/CA5BFA8878FB94BBF037EC4A133ADCA89FFAEC16'  
    ```  
  
-   **Nombre del proveedor:** MSSQL_CSP_PROVIDER  
  
     **Formato de clave de la ruta de acceso:** *ProviderName*/*KeyIdentifier*  
  
     Donde:  
  
     *ProviderName*  
     El nombre de un proveedor de servicios de cifrado (CSP), que implementa CAPI, para el almacén de claves maestras de columna. Si utiliza un HSM como un almacén de claves, debe ser el nombre del CSP al proveedor de HSM proporciona. El proveedor debe estar instalado en un equipo cliente.  
  
     *KeyIdentifier*  
     Identificador de la clave, se utiliza como una clave maestra de columna, en el almacén de claves.  
  
     **Ejemplos:**  
  
    ```  
    N'My HSM CSP Provider/AlwaysEncryptedKey1'  
    ```  
  
-   **Nombre del proveedor:** MSSQL_CNG_STORE  
  
     **Formato de clave de la ruta de acceso:** *ProviderName*/*KeyIdentifier*  
  
     Donde:  
  
     *ProviderName*  
     Nombre del proveedor de almacenamiento de claves (KSP), que implementa la criptografía: API Next Generation (CNG), para el almacén de claves maestras de columna. Si utiliza un HSM como un almacén de claves, debe ser el nombre de lo KSP al proveedor de HSM proporciona. El proveedor debe instalarse en un equipo cliente.  
  
     *KeyIdentifier*  
     Identificador de la clave, se utiliza como una clave maestra de columna, en el almacén de claves.  
  
     **Ejemplos:**  
  
    ```  
    N'My HSM CNG Provider/AlwaysEncryptedKey1'  
    ```  

-   **Nombre del proveedor:** AZURE_KEY_STORE  
  
     **Formato de clave de la ruta de acceso:** *dirección URL de clave*  
  
     Donde:  
  
     *Dirección URL de clave*  
     La dirección URL de la clave en el almacén de claves de Azure


Ejemplo:
 
`N'https://myvault.vault.azure.net:443/keys/MyCMK/4c05f1a41b12488f9cba2ea964b6a700'`  
  
## <a name="remarks"></a>Comentarios  

Es necesario crear una entrada de metadatos de la clave maestra de columna antes de poder crear una entrada de metadatos de la clave de cifrado de columna en la base de datos y antes de cualquier columna de la base de datos se puede cifrar mediante Always Encrypted. Tenga en cuenta que, una entrada de la clave maestra de columna en los metadatos no contiene la clave maestra de columna reales, que deben almacenarse en un almacén de claves de la columna externa (fuera de SQL Server). El nombre del proveedor de almacén de claves y la ruta de acceso de clave maestra de columna en los metadatos deben ser válidos para una aplicación cliente para poder usar la clave maestra de columna que se va a descifrar una clave de cifrado de columna cifrada con la clave maestra de columna, así como consultar columnas cifradas.


  
## <a name="permissions"></a>Permissions  
 Requiere la **ALTER ANY COLUMN MASTER KEY** permiso.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-column-master-key"></a>A. Crear una clave maestra de columna  
 Crear una entrada de metadatos de la clave maestra de columna de una clave maestra de columna almacenada en el almacén de certificados para las aplicaciones cliente que utilizan el proveedor MSSQL_CERTIFICATE_STORE para tener acceso a la clave maestra de columna:  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
     KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',   
     KEY_PATH = 'Current User/Personal/f2260f28d909d21c642a3d8e0b45a830e79a1420'  
   );  
```  
  
 Crear una entrada de metadatos de clave maestra de columna de una clave maestra de columna que se tiene acceso a las aplicaciones cliente que utilizan el proveedor MSSQL_CNG_STORE:  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CNG_STORE',    
    KEY_PATH = N'My HSM CNG Provider/AlwaysEncryptedKey'  
);  
```  
  
 Crear una clave maestra de columna almacenada en el almacén de claves de Azure, para las aplicaciones cliente que utilizan el proveedor AZURE_KEY_VAULT, para tener acceso a la clave maestra de columna.  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',  
    KEY_PATH = N'https://myvault.vault.azure.net:443/keys/  
        MyCMK/4c05f1a41b12488f9cba2ea964b6a700');  
```  
  
 Crear una CMK almacenada en un almacén de claves maestras de columna personalizada:  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = 'CUSTOM_KEY_STORE',    
    KEY_PATH = 'https://contoso.vault/sales_db_tce_key'  
);  
```  
  
## <a name="see-also"></a>Vea también
 
* [ELIMINAR claves maestras de columna &#40; Transact-SQL &#41;](../../t-sql/statements/drop-column-master-key-transact-sql.md)   
* [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)
* [sys.column_master_keys (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
* [Always Encrypted &#40;motor de base de datos&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
* [Overview of Key Management for Always Encrypted (Información general de administración de claves de Always Encrypted)](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
  

