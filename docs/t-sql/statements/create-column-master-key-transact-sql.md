---
title: CREATE COLUMN MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 81fd7b18058430b3132471f67a8b94e4444873e7
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52393048"
---
# <a name="create-column-master-key-transact-sql"></a>CREATE COLUMN MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Crea un objeto de metadatos de clave maestra de columna en una base de datos. Una entrada de metadatos de clave maestra de columna que representa una clave almacenada en un almacén de claves externo, que se usa para proteger (cifrar) claves de cifrado de columna cuando se usa la característica [Always Encrypted &#40;motor de base de datos&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md). Varias claves maestras de columna permiten la rotación de claves; cambie periódicamente la clave para mejorar la seguridad. Puede crear una clave maestra de columna en un almacén de claves y su objeto de metadatos correspondiente en la base de datos mediante el Explorador de objetos en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o PowerShell. Para más detalles, vea [Información general de administración de claves de Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
 

> [!IMPORTANT]
> Si desea crear claves habilitadas para enclaves (con ENCLAVE_COMPUTATIONS) se requiere [Always Encrypted con enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves.md).

## <a name="syntax"></a>Sintaxis  

```  
CREATE COLUMN MASTER KEY key_name   
    WITH (  
        KEY_STORE_PROVIDER_NAME = 'key_store_provider_name',  
        KEY_PATH = 'key_path'   
        [,ENCLAVE_COMPUTATIONS (SIGNATURE = signature)]
         )   
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *key_name*  
 Es el nombre por el que se conocerá la clave maestra de columna en la base de datos.  
  
 *key_store_provider_name*  
 Especifica el nombre de un proveedor de almacenamiento de claves, que es un componente de software del lado cliente que encapsula un almacén de claves que contiene la clave maestra de columna. Un controlador cliente compatible con Always Encrypted usa un nombre de proveedor de almacenamiento de claves para buscar un proveedor de almacenamiento de claves en el Registro de proveedores de almacenamiento de claves del controlador. El controlador usa el proveedor para descifrar las claves de cifrado de columna, protegidas por una clave maestra de columna almacenada en el almacén de claves subyacente. Después se usa un valor de texto simple de la clave de cifrado de columna para cifrar los parámetros de consulta correspondientes a las columnas de la base de datos cifrada, o para descifrar los resultados de la consulta a partir de columnas cifradas.  
  
 Las bibliotecas de controladores cliente compatibles con Always Encrypted incluyen proveedores de almacenamiento de claves para los almacenes de claves populares.   
  
Un conjunto de proveedores disponibles depende del tipo y la versión del controlador cliente. Vea información sobre controladores determinados en la documentación de Always Encrypted:

[Desarrollar aplicaciones mediante Always Encrypted con el proveedor de datos .NET Framework para SQL Server](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)


En las tablas de abajo se recopilan los nombres de proveedores del sistema:  
  
|Nombre de proveedor de almacenamiento de claves|Almacén de claves subyacente|  
    |-----------------------------|--------------------------|
    |'MSSQL_CERTIFICATE_STORE'|Almacén de certificados de Windows| 
    |'MSSQL_CSP_PROVIDER'|Un almacén, como por ejemplo un módulo de seguridad de hardware (HSM), que es compatible con Microsoft CryptoAPI.|
    |'MSSQL_CNG_STORE'|Un almacén, como un módulo de seguridad de hardware (HSM), que es compatible con la API de Cryptography Next Generation.|  
    |'Azure_Key_Vault'|Vea [Introducción a Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)|  
  

 Puede implementar un proveedor de almacenamiento de claves personalizado para almacenar claves maestras de columna en un almacén para el que no haya ningún proveedor de almacenamiento de claves integrado en el controlador cliente compatible con Always Encrypted.  Tenga en cuenta que los nombres de proveedores de almacenamiento de claves personalizados no pueden empezar por 'MSSQL_', ya que es un prefijo reservado para proveedores de almacenamiento de claves de [!INCLUDE[msCoName](../../includes/msconame-md.md)]. 

  
 key_path  
 La ruta de acceso de la clave en el almacén de claves maestras de columna. La ruta de la clave debe ser válida en el contexto de cada aplicación cliente que se espera que cifre o descifre los datos almacenados en una columna protegida (indirectamente) por la clave maestra de columna a la que se hace referencia; además, la aplicación cliente necesita permiso para acceder a la clave. El formato de la ruta de acceso de la clave es específico del proveedor de almacenamiento de claves. En esta lista se describe el formato de las rutas de acceso de claves para determinados proveedores de almacenamiento de claves del sistema de Microsoft.  
  
-   **Nombre de proveedor:** MSSQL_CERTIFICATE_STORE  
  
     **Formato de ruta de acceso de la clave:** *CertificateStoreName*/*CertificateStoreLocation*/*CertificateThumbprint*  
  
     Donde:  
  
     *CertificateStoreLocation*  
     Ubicación del almacén de certificados, que debe ser Usuario actual o Máquina local. Para más información, vea [Local Machine and Current User Certificate Stores](https://msdn.microsoft.com/library/windows/hardware/ff548653.aspx) (Almacenes de certificados Máquina local y Usuario actual).  
  
     *CertificateStore*  
     Nombre del almacén de certificados, como por ejemplo, 'My'.  
  
     *CertificateThumbprint*  
     Huella digital del certificado.  
  
     **Ejemplos:**  
  
    ```  
    N'CurrentUser/My/BBF037EC4A133ADCA89FFAEC16CA5BFA8878FB94'  
  
    N'LocalMachine/My/CA5BFA8878FB94BBF037EC4A133ADCA89FFAEC16'  
    ```  
  
-   **Nombre de proveedor:** MSSQL_CSP_PROVIDER  
  
     **Formato de ruta de acceso de la clave:** *ProviderName*/*KeyIdentifier*  
  
     Donde:  
  
     *ProviderName*  
     El nombre de un Cryptographic Service Provider (CSP), que implementa CAPI para el almacén de claves maestras de columna. Si usa un HSM como un almacén de claves, debe ser el nombre del CSP proporcionado por el proveedor de HSM. El proveedor debe estar instalado en un equipo cliente.  
  
     *KeyIdentifier*  
     Identificador de la clave, usado como una clave maestra de columna en el almacén de claves.  
  
     **Ejemplos:**  
  
    ```  
    N'My HSM CSP Provider/AlwaysEncryptedKey1'  
    ```  
  
-   **Nombre de proveedor:** MSSQL_CNG_STORE  
  
     **Formato de ruta de acceso de la clave:** *ProviderName*/*KeyIdentifier*  
  
     Donde:  
  
     *ProviderName*  
     Nombre del proveedor de almacenamiento de claves (KSP) que implementa la API de Cryptography Next Generation (CNG) para el almacén de claves maestras de columna. Si usa un HSM como almacén de claves, debe ser el nombre del CSP que el proveedor de HSM proporciona. El proveedor debe instalarse en un equipo cliente.  
  
     *KeyIdentifier*  
     Identificador de la clave, usado como una clave maestra de columna en el almacén de claves.  
  
     **Ejemplos:**  
  
    ```  
    N'My HSM CNG Provider/AlwaysEncryptedKey1'  
    ```  

-   **Nombre del proveedor:** AZURE_KEY_STORE  
  
     **Formato de clave de la ruta de acceso:** *KeyUrl*  
  
     Donde:  
  
     *KeyUrl*  
     La dirección URL de la clave en Azure Key Vault.

ENCLAVE_COMPUTATIONS  
Especifica que la clave maestra de columna está habilitado para enclaves, lo que significa que todas las claves de cifrado de columna cifradas con esta clave maestra de columna pueden compartirse con un enclave seguro del lado servidor y usarse para realizar cálculos dentro el enclave. Para más información, consulte [Always Encrypted con enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves.md).

 *signature*  
Un literal binario que se genera por firmar digitalmente la *ruta de acceso clave* y la configuración de ENCLAVE_COMPUTATIONS con la clave maestra de columna (la firma refleja si ENCLAVE_COMPUTATIONS se ha especificado o no). La firma evita que los usuarios no autorizados modifiquen los valores firmados. Un controlador cliente habilitado para Always Encrypted puede comprobar la firma y devolver un error a la aplicación si la firma no es válida. La firma debe haberse generada utilizando herramientas de cliente. Para más información, consulte [Always Encrypted con enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves.md).
  
  
## <a name="remarks"></a>Notas  

Es necesario crear primero una entrada de metadatos de la clave maestra de columna para poder crear una entrada de metadatos de la clave de cifrado de columna en la base de datos y para poder cifrar cualquier columna de la base de datos mediante Always Encrypted. Tenga en cuenta que una entrada de la clave maestra de columna en los metadatos no contiene la clave maestra de columna real, sino que esta debe almacenarse en un almacén de claves de columnas externas (fuera de SQL Server). El nombre del proveedor de almacenamiento de claves y la ruta de acceso de la clave maestra de columna en los metadatos deben ser válidos para que una aplicación cliente pueda usar la clave maestra de columna a efectos de descifrar una clave de cifrado de columna que esté cifrada con la clave maestra de columna y para consultar columnas cifradas.


  
## <a name="permissions"></a>Permisos  
 Necesita el permiso **ALTER ANY COLUMN MASTER KEY**.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-column-master-key"></a>A. Crear una clave maestra de columna  
 Crear una entrada de metadatos de la clave maestra de columna para una clave maestra de columna que está almacenada en el almacén de certificados, para las aplicaciones cliente que usan el proveedor MSSQL_CERTIFICATE_STORE para acceder a la clave maestra de columna:  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
     KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',   
     KEY_PATH = 'Current User/Personal/f2260f28d909d21c642a3d8e0b45a830e79a1420'  
   );  
```  
  
 Crear una entrada de metadatos de clave maestra de columna para una clave maestra de columna a la que tienen acceso las aplicaciones cliente que usan el proveedor MSSQL_CNG_STORE:  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CNG_STORE',    
    KEY_PATH = N'My HSM CNG Provider/AlwaysEncryptedKey'  
);  
```  
  
 Crear una entrada de metadatos de clave maestra de columna para una clave maestra de columna almacenada en Azure Key Vault, para las aplicaciones cliente que usan el proveedor AZURE_KEY_VAULT con el fin de acceder a la clave maestra de columna.  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',  
    KEY_PATH = N'https://myvault.vault.azure.net:443/keys/  
        MyCMK/4c05f1a41b12488f9cba2ea964b6a700');  
```  
  
 Crear una entrada de metadatos de clave maestra de columna para una clave maestra de columna almacenada en un almacén de claves maestras de columna personalizado:  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = 'CUSTOM_KEY_STORE',    
    KEY_PATH = 'https://contoso.vault/sales_db_tce_key'  
);  
```  
### <a name="b-creating-an-enclave-enabled-column-master-key"></a>B. Crear una clave maestra de columna habilitada para enclaves  
 Crear una entrada de metadatos de la clave maestra de columna para una clave maestra de columna habilitada para enclaves que está almacenada en el almacén de certificados, para las aplicaciones cliente que usan el proveedor MSSQL_CERTIFICATE_STORE con el fin de acceder a la clave maestra de columna:  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
     KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',   
     KEY_PATH = 'Current User/Personal/f2260f28d909d21c642a3d8e0b45a830e79a1420'  
     ENCLAVE_COMPUTATIONS (SIGNATURE = 0xA80F5B123F5E092FFBD6014FC2226D792746468C901D9404938E9F5A0972F38DADBC9FCBA94D9E740F3339754991B6CE26543DEB0D094D8A2FFE8B43F0C7061A1FFF65E30FDDF39A1B954F5BA206AAC3260B0657232020542419990261D878318CC38EF4E853970ED69A8D4A306693B8659AAC1C4E4109DE5EB148FD0E1FDBBC32F002C1D8199D313227AD689279D8DEEF91064DF122C19C3767C463723AB663A6F8412AE17E745922C0E3A257EAEF215532588ACCBD440A03C7BC100A38BD0609A119E1EF7C5C6F1B086C68AB8873DBC6487B270340E868F9203661AFF0492CEC436ABF7C4713CE64E38CF66C794B55636BFA55E5B6554AF570CF73F1BE1DBD)
  );  
```  
  
 Crear una entrada de metadatos de clave maestra de columna para una clave maestra de columna habilitada para enclaves almacenada en Azure Key Vault, para las aplicaciones cliente que usan el proveedor AZURE_KEY_VAULT con el fin de acceder a la clave maestra de columna.  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',  
    KEY_PATH = N'https://myvault.vault.azure.net:443/keys/MyCMK/4c05f1a41b12488f9cba2ea964b6a700');
    ENCLAVE_COMPUTATIONS (SIGNATURE = 0xA80F5B123F5E092FFBD6014FC2226D792746468C901D9404938E9F5A0972F38DADBC9FCBA94D9E740F3339754991B6CE26543DEB0D094D8A2FFE8B43F0C7061A1FFF65E30FDDF39A1B954F5BA206AAC3260B0657232020582413990261D878318CC38EF4E853970ED69A8D4A306693B8659AAC1C4E4109DE5EB148FD0E1FDBBC32F002C1D8199D313227AD689279D8DEEF91064DF122C19C3767C463723AB663A6F8412AE17E745922C0E3A257EAEF215532588ACCBD440A03C7BC100A38BD0609A119E1EF7C5C6F1B086C68AB8873DBC6487B270340E868F9203661AFF0492CEC436ABF7C4713CE64E38CF66C794B55636BFA55E5B6554AF570CF73F1BE1DBD)
  );
```  
  
## <a name="see-also"></a>Ver también
 
* [DROP COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-master-key-transact-sql.md)   
* [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)
* [sys.column_master_keys (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
* [Always Encrypted &#40;motor de base de datos&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
* [Información general de administración de claves de Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
  
