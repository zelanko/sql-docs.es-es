---
title: ALTER CERTIFICATE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 04/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_CERTIFICATE_TSQL
- ALTER CERTIFICATE
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTION BY PASSWORD option
- encryption [SQL Server], certificates
- modifying certificates
- private keys [SQL Server]
- ALTER CERTIFICATE statement
- certificates [SQL Server], modifying
ms.assetid: da4dc25e-72e0-4036-87ce-22de83160836
caps.latest.revision: 46
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: da51e41cc5adf4fa9f4f57cfe094fe5a72119c70
ms.contentlocale: es-es
ms.lasthandoff: 10/24/2017

---
# <a name="alter-certificate-transact-sql"></a>ALTER CERTIFICATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Cambia la clave privada que se utiliza para cifrar un certificado o agrega una si no existe. Cambia la disponibilidad de un certificado a [!INCLUDE[ssSB](../../includes/sssb-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
ALTER CERTIFICATE certificate_name   
      REMOVE PRIVATE KEY  
    | WITH PRIVATE KEY ( <private_key_spec> [ ,... ] )  
    | WITH ACTIVE FOR BEGIN_DIALOG = [ ON | OFF ]  
  
<private_key_spec> ::=   
      FILE = 'path_to_private_key'   
    | DECRYPTION BY PASSWORD = 'key_password'   
    | ENCRYPTION BY PASSWORD = 'password'   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER CERTIFICATE certificate_name   
{  
      REMOVE PRIVATE KEY  
    | WITH PRIVATE KEY (   
        FILE = '<path_to_private_key>',  
        DECRYPTION BY PASSWORD = '<key password>' )
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *nombre_de_certificado*  
 Nombre único por el que se conoce al certificado en la base de datos.  
  
 ARCHIVO **='***path_to_private_key***'**  
 Especifica la ruta de acceso completa a la clave privada, incluido el nombre de archivo. Este parámetro puede ser una ruta de acceso local o una ruta de acceso UNC a una ubicación de red. Se obtiene acceso a este archivo dentro del contexto de seguridad de la cuenta del servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando utilice esta opción, asegúrese de que la cuenta de servicio tenga acceso al archivo especificado.  
  
 DECRYPTION BY PASSWORD **='***key_password***'**  
 Especifica la contraseña necesaria para descifrar la clave privada.  
  
 ENCRYPTION BY PASSWORD **='***contraseña***'**  
 Especifica la contraseña que se usa para cifrar la clave privada del certificado en la base de datos. *contraseña* debe cumplir los requisitos de directiva de contraseñas de Windows del equipo que ejecuta la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Password Policy](../../relational-databases/security/password-policy.md).  
  
 REMOVE PRIVATE KEY  
 Indica que no debe seguir manteniéndose la clave privada en la base de datos.  
  
 ACTIVE FOR BEGIN_DIALOG  **=**  {ON | {OFF}  
 Hace que el certificado esté disponible para el iniciador de una conversación de diálogo de [!INCLUDE[ssSB](../../includes/sssb-md.md)].  
  
## <a name="remarks"></a>Comentarios  
 La clave privada debe corresponder a la clave pública especificada por *nombre_de_certificado*.  
  
 Puede omitir la cláusula DECRYPTION BY PASSWORD si la contraseña del archivo está protegida mediante una contraseña NULL.  
  
 Cuando la clave privada de un certificado que ya existe en la base de datos se importa desde un archivo, esta clave privada se protegerá automáticamente mediante la clave maestra de la base de datos. Para proteger la clave privada con una contraseña, utilice la frase ENCRYPTION BY PASSWORD.  
  
 La opción REMOVE PRIVATE KEY eliminará de la base de datos la clave privada del certificado. Puede hacer esto cuando el certificado se utilice para comprobar firmas o en escenarios de [!INCLUDE[ssSB](../../includes/sssb-md.md)] que no necesiten una clave privada. No elimine la clave privada de un certificado que proteja una clave simétrica.  
  
 No es necesario especificar una contraseña de descifrado cuando la clave privada se ha cifrado mediante la clave maestra de la base de datos.  
  
> [!IMPORTANT]  
>  Haga siempre una copia de archivo de una clave privada antes de quitarla de una base de datos. Para obtener más información, vea [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md).  
  
 La opción WITH PRIVATE KEY no está disponible en una base de datos independiente.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER en el certificado.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-changing-the-password-of-a-certificate"></a>A. Cambiar la contraseña de un certificado  
  
```  
ALTER CERTIFICATE Shipping04   
    WITH PRIVATE KEY (DECRYPTION BY PASSWORD = 'pGF$5DGvbd2439587y',  
    ENCRYPTION BY PASSWORD = '4-329578thlkajdshglXCSgf');  
GO  
```  
  
### <a name="b-changing-the-password-that-is-used-to-encrypt-the-private-key"></a>B. Cambiar la contraseña utilizada para cifrar una clave privada  
  
```  
ALTER CERTIFICATE Shipping11   
    WITH PRIVATE KEY (ENCRYPTION BY PASSWORD = '34958tosdgfkh##38',  
    DECRYPTION BY PASSWORD = '95hkjdskghFDGGG4%');  
GO  
```  
  
### <a name="c-importing-a-private-key-for-a-certificate-that-is-already-present-in-the-database"></a>C. Importar una clave privada para un certificado que ya existe en la base de datos  
  
```  
ALTER CERTIFICATE Shipping13   
    WITH PRIVATE KEY (FILE = 'c:\\importedkeys\Shipping13',  
    DECRYPTION BY PASSWORD = 'GDFLKl8^^GGG4000%');  
GO  
```  
  
### <a name="d-changing-the-protection-of-the-private-key-from-a-password-to-the-database-master-key"></a>D. Cambiar la protección de una clave privada, desde una contraseña a la clave maestra de la base de datos  
  
```  
ALTER CERTIFICATE Shipping15   
    WITH PRIVATE KEY (DECRYPTION BY PASSWORD = '95hk000eEnvjkjy#F%');  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [Eliminar certificado &#40; Transact-SQL &#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  


