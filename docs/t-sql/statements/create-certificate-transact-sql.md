---
title: Crear certificado (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CERTIFICATE
- CREATE_CERTIFICATE_TSQL
- sql13.swb.createcertificate.f1
- CERTIFICATE_TSQL
- CREATE CERTIFICATE
- sql13.swb.certificateproperties.f1
dev_langs:
- TSQL
helpviewer_keywords:
- encryption [SQL Server], certificates
- certificates [SQL Server], adding
- certificates [SQL Server]
- adding certificates
- cryptography [SQL Server], certificates
- CREATE CERTIFICATE statement
ms.assetid: a4274b2b-4cb0-446a-a956-1c8e6587515d
caps.latest.revision: 74
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8753e820278eb04fff6f12e405d766fff5292e58
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-certificate-transact-sql"></a>CREATE CERTIFICATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Agrega un certificado a una base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Esta función no es compatible con la exportación de la base de datos con el Marco de trabajo de la aplicación de capa de datos (DACFx). Debe quitar todos los certificados antes de exportar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
CREATE CERTIFICATE certificate_name [ AUTHORIZATION user_name ]   
    { FROM <existing_keys> | <generate_new_keys> }  
    [ ACTIVE FOR BEGIN_DIALOG =  { ON | OFF } ]  
  
<existing_keys> ::=   
    ASSEMBLY assembly_name  
    | {   
        [ EXECUTABLE ] FILE = 'path_to_file'  
        [ WITH PRIVATE KEY ( <private_key_options> ) ]   
      }  
    | {   
        BINARY = asn_encoded_certificate  
        [ WITH PRIVATE KEY ( <private_key_options> ) ]  
      }  
<generate_new_keys> ::=   
    [ ENCRYPTION BY PASSWORD = 'password' ]   
    WITH SUBJECT = 'certificate_subject_name'   
    [ , <date_options> [ ,...n ] ]   
  
<private_key_options> ::=  
      {   
        FILE = 'path_to_private_key'  
         [ , DECRYPTION BY PASSWORD = 'password' ]  
         [ , ENCRYPTION BY PASSWORD = 'password' ]    
      }  
    |  
      {   
        BINARY = private_key_bits  
         [ , DECRYPTION BY PASSWORD = 'password' ]  
         [ , ENCRYPTION BY PASSWORD = 'password' ]    
      }  
  
<date_options> ::=  
    START_DATE = 'datetime' | EXPIRY_DATE = 'datetime'  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE CERTIFICATE certificate_name   
    { <generate_new_keys> | FROM <existing_keys> }  
    [ ; ]  
  
<generate_new_keys> ::=   
    WITH SUBJECT ='certificate_subject_name'   
    [ , <date_options> [ ,...n ] ]   
  
<existing_keys> ::=   
    {   
      FILE ='path_to_file'  
      WITH PRIVATE KEY   
         (   
           FILE ='path_to_private_key'  
           , DECRYPTION BY PASSWORD ='password'   
         )  
    }  
  
<date_options> ::=  
    START_DATE ='datetime' | EXPIRY_DATE ='datetime'  
```  
  
## <a name="arguments"></a>Argumentos  
 *nombre_de_certificado*  
 Es el nombre para el certificado en la base de datos.  
  
 AUTORIZACIÓN *user_name*  
 Es el nombre del usuario que posee este certificado.  
  
 ENSAMBLADO *assembly_name*  
 Especifica un ensamblado firmado que se ha cargado en la base de datos.  
  
 [EJECUTABLE] ARCHIVO ='*ruta_de_acceso_al_archivo*'  
 Especifica la ruta completa, incluido el nombre de archivo, de acceso a un archivo codificado con DER que contiene el certificado. Si se usa la opción EXECUTABLE, el archivo es una DLL firmada por el certificado. *ruta_de_acceso_al_archivo* puede ser una ruta de acceso local o una ruta UNC a una ubicación de red. Se tiene acceso a los archivos en el contexto de seguridad de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta de servicio. Esta cuenta debe disponer de los necesarios permisos de sistema de archivos.  
  
 WITH PRIVATE KEY  
 Especifica que la clave privada del certificado se ha cargado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta cláusula solo es válida si se crea el certificado desde un archivo. Para cargar la clave privada de un ensamblado, utilice [ALTER CERTIFICATE](../../t-sql/statements/alter-certificate-transact-sql.md).  
  
 ARCHIVO ='*path_to_private_key*'  
 Especifica la ruta de acceso completa a la clave privada, incluido el nombre de archivo. *path_to_private_key* puede ser una ruta de acceso local o una ruta UNC a una ubicación de red. Se tiene acceso a los archivos en el contexto de seguridad de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta de servicio. Esta cuenta debe disponer de los necesarios permisos de sistema de archivos.  
  
> [!NOTE]  
>  Esta opción no está disponible en las bases de datos independientes.  
  
 asn_encoded_certificate  
 Bits de certificado codificados por ASN especificados como una constante binaria.  
  
 BINARIO =*private_key_bits*  
 **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Bits de clave privada especificados como una constante binaria. Estos bits pueden estar en forma cifrada. Si están cifrados, el usuario debe proporcionar una contraseña de descifrado. No se realizan comprobaciones de directiva de contraseña en esta contraseña. Los bits de clave privada deben tener el formato de archivo PVK.  
  
 DECRYPTION BY PASSWORD ='*key_password*'  
 Especifica la contraseña necesaria para descifrar una clave privada recuperada de un archivo. La cláusula es opcional si la clave privada está protegida por una contraseña NULL. No se recomienda guardar una clave privada de un archivo sin protección de contraseña. Si se requiere una contraseña, pero no se especifica, se produce un error en la instrucción.  
  
 ENCRYPTION BY PASSWORD ='*contraseña*'  
 Especifica la contraseña utilizada para cifrar la clave privada. Utilice esta opción solo si desea cifrar el certificado con una contraseña. Si se omite esta cláusula, la clave privada se cifra con la clave maestra de base de datos. *contraseña* debe cumplir los requisitos de directiva de contraseñas de Windows del equipo que ejecuta la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Password Policy](../../relational-databases/security/password-policy.md).  
  
 SUJETO ='*nombre_asunto_certificado*'  
 El término *asunto* hace referencia a un campo en los metadatos del certificado como se define en el estándar X.509. El firmante debe ser no más de 64 caracteres, y este límite se aplica para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en Linux. Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en Windows, el sujeto puede tener hasta 128 caracteres. Los asuntos que superen los 128 caracteres se truncan cuando se almacenan en el catálogo, pero el objeto binario grande (BLOB) que contiene el certificado conserva el nombre del sujeto completo.  
  
 Start_date ='*datetime*'  
 Es la fecha en la que el certificado comienza a ser válido. Si no se especifica, START_DATE está establecida en la fecha actual. START_DATE se especifica en hora UTC y en cualquier formato que se pueda convertir a una fecha y hora.  
  
 EXPIRY_DATE ='*datetime*'  
 Es la fecha en la que expira el certificado. Si no se especifica, EXPIRY_DATE se establece en una fecha un año después de la fecha_inicial. EXPIRY_DATE se especifica en hora UTC y en cualquier formato que se pueda convertir a una fecha y hora. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Service Broker comprueba la fecha de expiración. Sin embargo, no se exige la expiración cuando el certificado se utiliza para el cifrado.  
  
 ACTIVE FOR BEGIN_DIALOG = { **ON** | {OFF}  
 Hace que el certificado esté disponible para el iniciador de una conversación de diálogo de [!INCLUDE[ssSB](../../includes/sssb-md.md)]. El valor predeterminado es ON.  
  
## <a name="remarks"></a>Comentarios  
 Un certificado es un elemento protegible de nivel de base de datos que sigue el estándar X.509 y admite los campos V1 de X.509. CREATE CERTIFICATE puede cargar un certificado desde un archivo o ensamblado. Esta instrucción también puede generar un par de claves y crear un certificado con firma personal.  
  
 La clave privada debe ser \<= 2500 bytes en formato cifrado. Las claves privadas generadas por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] son 1024 bits larga mediante [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y longitud de 2048 bits comienza con [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Las claves privadas importadas de un origen externo presentan una longitud mínima de 384 bits y una máxima de 4.096 bits. La longitud de una clave privada importada debe ser un entero múltiplo de 64 bits. Los certificados que se usan para TDE tienen un límite de tamaño de clave privada de 3456 bits.  
  
 Se almacena todo el número de serie del certificado, pero solo los primeros 16 bytes aparecen en la vista de catálogo sys.certificates.  
  
 Se almacena todo el campo del emisor del certificado, pero solo los primeros bytes 884 en el sys.certificates la vista de catálogo.  
  
 La clave privada debe corresponder a la clave pública especificada por *nombre_de_certificado*.  
  
 Cuando se crea un certificado desde un contenedor, es opcional cargar la clave privada. Pero cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera un certificado con firma personal, siempre se creará la clave privada. De manera predeterminada, la clave privada se cifra con la clave maestra de base de datos. Si no existe la clave maestra de base de datos y no se especifica, se produce un error en la instrucción.  
  
 La opción de cifrado por contraseña no es necesaria cuando la clave privada se cifra con la clave maestra de base de datos. Use esta opción solo si la clave privada está cifrada con una contraseña. Si no se especifica una contraseña, la clave privada del certificado se cifrará con la clave maestra de base de datos. Si no se puede abrir la clave maestra de la base de datos, si se omite esta cláusula produce un error.  
  
 No es necesario especificar una contraseña de descifrado si se cifra la clave privada con la clave maestra de base de datos.  
  
> [!NOTE]  
>  Las funciones integradas para el cifrado y firma no comprueban las fechas de expiración de los certificados. Los usuarios de estas funciones deben decidir cuándo comprobar la expiración de los certificados.  
  
 Se puede crear una descripción binaria de un certificado mediante el [CERTENCODED &#40; Transact-SQL &#41; ](../../t-sql/functions/certencoded-transact-sql.md) y [CERTPRIVATEKEY &#40; Transact-SQL &#41; ](../../t-sql/functions/certprivatekey-transact-sql.md) funciones. Para obtener un ejemplo que usa **CERTPRIVATEKEY** y **CERTENCODED** para copiar un certificado en otra base de datos, vea el ejemplo B en el tema [CERTENCODED &#40; Transact-SQL &#41; ](../../t-sql/functions/certencoded-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso CREATE CERTIFICATE en la base de datos. Solo Windows inicios de sesión, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicios de sesión y roles de aplicación pueden poseer certificados. Los grupos y roles no pueden poseer los certificados.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-self-signed-certificate"></a>A. Crear un certificado autofirmado  
 En el siguiente ejemplo se crea un certificado denominado `Shipping04`. La clave privada de este certificado está protegida con una contraseña.  
  
```  
CREATE CERTIFICATE Shipping04   
   ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
   WITH SUBJECT = 'Sammamish Shipping Records',   
   EXPIRY_DATE = '20201031';  
GO  
```  
  
### <a name="b-creating-a-certificate-from-a-file"></a>B. Crear un certificado desde un archivo  
 En el ejemplo siguiente se crea un certificado en la base de datos y se carga el par de claves desde los archivos.  
  
```  
CREATE CERTIFICATE Shipping11   
    FROM FILE = 'c:\Shipping\Certs\Shipping11.cer'   
    WITH PRIVATE KEY (FILE = 'c:\Shipping\Certs\Shipping11.pvk',   
    DECRYPTION BY PASSWORD = 'sldkflk34et6gs%53#v00');  
GO   
```  
  
### <a name="c-creating-a-certificate-from-a-signed-executable-file"></a>C. Crear un certificado desde un archivo ejecutable firmado  
  
```  
CREATE CERTIFICATE Shipping19   
    FROM EXECUTABLE FILE = 'c:\Shipping\Certs\Shipping19.dll';  
GO  
```  
  
 Como alternativa, puede crear un ensamblado desde el archivo `dll` y crear un certificado desde el ensamblado.  
  
```  
CREATE ASSEMBLY Shipping19   
    FROM ' c:\Shipping\Certs\Shipping19.dll'   
    WITH PERMISSION_SET = SAFE;  
GO  
CREATE CERTIFICATE Shipping19 FROM ASSEMBLY Shipping19;  
GO  
```  
  
### <a name="d-creating-a-self-signed-certificate"></a>D. Crear un certificado autofirmado  
 En el ejemplo siguiente se crea un certificado denominado `Shipping04` sin especificar una contraseña de cifrado. En este ejemplo puede usarse con [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].
  
```  
CREATE CERTIFICATE Shipping04   
   WITH SUBJECT = 'Sammamish Shipping Records';  
GO  
```  
  
  
## <a name="see-also"></a>Vea también  
 [ALTER CERTIFICATE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [Eliminar certificado &#40; Transact-SQL &#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [CERTENCODED &#40; Transact-SQL &#41;](../../t-sql/functions/certencoded-transact-sql.md)   
 [CERTPRIVATEKEY &#40; Transact-SQL &#41;](../../t-sql/functions/certprivatekey-transact-sql.md)  
  
  



