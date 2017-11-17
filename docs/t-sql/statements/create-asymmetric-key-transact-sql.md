---
title: "Crear clave ASIMÉTRICA (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 08/07/2017
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
- ASYMMETRIC_KEY_TSQL
- CREATE ASYMMETRIC KEY
- CREATE_ASYMMETRIC_KEY_TSQL
- ASYMMETRIC KEY
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], creating
- encryption [SQL Server], asymmetric keys
- CREATE ASYMMETRIC KEY statement
- asymmetric keys [SQL Server]
- cryptography [SQL Server], asymmetric keys
ms.assetid: 141bc976-7631-49f6-82bd-a235028645b1
caps.latest.revision: 51
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f39a31a9b2de4cd8153fa617b9cab1c1235f2a7a
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-asymmetric-key-transact-sql"></a>CREATE ASYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Crea una clave asimétrica en la base de datos.  
  
 Esta función no es compatible con la exportación de la base de datos con el Marco de trabajo de la aplicación de capa de datos (DACFx). Debe quitar todas las claves asimétricas antes de exportar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
CREATE ASYMMETRIC KEY Asym_Key_Name   
   [ AUTHORIZATION database_principal_name ]  
   [ FROM <Asym_Key_Source> ]  
   [ WITH <key_option> ] 
   [ ENCRYPTION BY <encrypting_mechanism> ] 
   [ ; ]
  
<Asym_Key_Source>::=  
     FILE = 'path_to_strong-name_file'  
   | EXECUTABLE FILE = 'path_to_executable_file'  
   | ASSEMBLY Assembly_Name  
   | PROVIDER Provider_Name  
  
<key_option> ::=  
   ALGORITHM = <algorithm>  
      |  
   PROVIDER_KEY_NAME = 'key_name_in_provider'  
      |  
      CREATION_DISPOSITION = { CREATE_NEW | OPEN_EXISTING }  
  
<algorithm> ::=  
      { RSA_4096 | RSA_3072 | RSA_2048 | RSA_1024 | RSA_512 }   
  
<encrypting_mechanism> ::=  
    PASSWORD = 'password'   
```  
  
## <a name="arguments"></a>Argumentos  
 DE *Asym_Key_Source*  
 Especifica el origen desde el que se carga el par de claves asimétricas.  
  
 AUTORIZACIÓN *database_principal_name*  
 Especifica el propietario de la clave asimétrica. El propietario no puede ser un rol ni un grupo. Si se omite esta opción, el propietario será el usuario actual.  
  
 ARCHIVO ='*path_to_strong name_file*'  
 Especifica la ruta de acceso a un archivo de nombre seguro desde el que se carga el par de claves.  
  
> [!NOTE]  
>  Esta opción no está disponible en las bases de datos independientes.  
  
 ARCHIVO ejecutable ='*path_to_executable_file*'  
 Especifica un archivo de ensamblado desde el que se carga la clave pública. Limitado a 260 caracteres por MAX_PATH de la API de Windows.  
  
> [!NOTE]  
>  Esta opción no está disponible en las bases de datos independientes.  
  
 ENSAMBLADO *Assembly_Name*  
 Especifica el nombre de un ensamblado desde el que se carga la clave pública.  
  
ENCRYPTION BY  *\<key_name_in_provider >* especifica cómo se cifra la clave. Puede ser un certificado, una contraseña o una clave asimétrica.  
  
 KEY_NAME ='*key_name_in_provider*'  
 Especifica el nombre de la clave del proveedor externo. Para obtener más información acerca de la administración de claves externas, vea [administración Extensible de claves &#40; EKM &#41; ](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
 CREATION_DISPOSITION = CREATE_NEW  
 Crea una nueva clave en el dispositivo de Administración extensible de claves. Debe utilizarse PROV_KEY_NAME para especificar el nombre de clave en el dispositivo. Si ya existe una clave en el dispositivo, se producirá un error en la instrucción.  
  
 CREATION_DISPOSITION = OPEN_EXISTING  
 Se asigna un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] clave asimétrica a una clave existente de administración Extensible de claves. Debe utilizarse PROV_KEY_NAME para especificar el nombre de clave en el dispositivo. Si no se proporciona CREATION_DISPOSITION = OPEN_EXISTING, el valor predeterminado es CREATE_NEW.  
  
 ALGORITMO = \<algoritmo >  
 Se pueden proporcionar cinco algoritmos; RSA_4096, RSA_3072, RSA_2048, RSA_1024 y RSA_512.  
  
 RSA_1024 y RSA_512 están en desuso. Usar RSA_1024 o RSA_512 (no recomendado) debe establecer el nivel de compatibilidad de base de datos a la base de datos 120 o inferior.  
  
 CONTRASEÑA = '*contraseña*'  
 Especifica la contraseña con la que se cifra la clave privada. Si no está presente esta cláusula, la clave privada se cifrará con la clave maestra de la base de datos. *contraseña* es un máximo de 128 caracteres. *contraseña* debe cumplir los requisitos de directiva de contraseñas de Windows del equipo que ejecuta la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="remarks"></a>Comentarios  
 Un *clave asimétrica* es una entidad protegible en el nivel de base de datos. De manera predeterminada, esta entidad contiene una clave pública y otra privada. Si se ejecuta sin la cláusula FROM, CREATE ASYMMETRIC KEY genera un nuevo par de claves. Si se ejecuta con la cláusula FROM, CREATE ASYMMETRIC KEY importa un par de claves desde un archivo o importa una clave pública desde un ensamblado.  
  
 De manera predeterminada, la clave privada está protegida por la clave maestra de la base de datos. Si no se ha creado una clave maestra de base de datos, se necesita una contraseña para proteger la clave privada. Si hay una clave maestra de base de datos, la contraseña es opcional.  
  
 La clave privada puede ser de 512, 1.024 o 2.048 bits.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso CREATE ASYMMETRIC KEY en la base de datos. Si se especifica la cláusula AUTHORIZATION, es necesario el permiso IMPERSONATE en la entidad de seguridad de la base de datos o el permiso ALTER en el rol de aplicación. Solo Windows inicios de sesión, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los inicios de sesión y los roles de aplicación pueden poseer claves asimétricas. Los grupos y roles no pueden poseer claves asimétricas.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-an-asymmetric-key"></a>A. Crear una clave asimétrica  
 En el siguiente ejemplo se crea una clave asimétrica con el nombre `PacificSales09` mediante el algoritmo `RSA_2048` y se protege la clave privada con una contraseña.  
  
```  
CREATE ASYMMETRIC KEY PacificSales09   
    WITH ALGORITHM = RSA_2048   
    ENCRYPTION BY PASSWORD = '<enterStrongPasswordHere>';   
GO  
```  
  
### <a name="b-creating-an-asymmetric-key-from-a-file-giving-authorization-to-a-user"></a>B. Crear una clave asimétrica desde un archivo, concediendo autorización a un usuario  
 En el siguiente ejemplo se crea la clave asimétrica `PacificSales19` a partir de un par de claves almacenadas en un archivo y, a continuación, se autoriza al usuario `Christina` a utilizar la clave asimétrica.   
  
```  
CREATE ASYMMETRIC KEY PacificSales19 AUTHORIZATION Christina   
    FROM FILE = 'c:\PacSales\Managers\ChristinaCerts.tmp'    
    ENCRYPTION BY PASSWORD = '<enterStrongPasswordHere>';  
GO  
```  
  
### <a name="c-creating-an-asymmetric-key-from-an-ekm-provider"></a>C. Crear una clave asimétrica de un proveedor de EKM  
 En el ejemplo siguiente se crea la clave asimétrica `EKM_askey1` a partir de un par de claves almacenadas en un archivo. A continuación, lo cifra mediante un proveedor de Administración extensible de claves llamado `EKMProvider1` y una clave en dicho proveedor llamada `key10_user1`.  
  
```  
CREATE ASYMMETRIC KEY EKM_askey1   
    FROM PROVIDER EKM_Provider1  
    WITH   
        ALGORITHM = RSA_2048,   
        CREATION_DISPOSITION = CREATE_NEW  
        , PROVIDER_KEY_NAME  = 'key10_user1' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Elegir un algoritmo de cifrado](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Administración extensible de claves con el Almacén de claves de Azure &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  

