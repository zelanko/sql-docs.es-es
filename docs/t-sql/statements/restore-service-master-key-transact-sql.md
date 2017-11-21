---
title: "CLAVE maestra de servicio de restauración (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RESTORE SERVICE MASTER KEY
- RESTORE_SERVICE_MASTER_KEY_TSQL
- LOAD SERVICE MASTER KEY
- LOAD_SERVICE_MASTER_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- importing Service Master Keys
- copying Service Master Keys
- service master key [SQL Server], importing
- RESTORE SERVICE MASTER KEY statement
- transferring Service Master Keys
ms.assetid: a68fd0ee-70ce-4104-aca0-fcae5f41fc38
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1af070097c6c2581901eb92eaa5d6292439b91e7
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="restore-service-master-key-transact-sql"></a>RESTORE SERVICE MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Importa una clave maestra de servicio desde un archivo de copia de seguridad.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RESTORE SERVICE MASTER KEY FROM FILE = 'path_to_file'   
    DECRYPTION BY PASSWORD = 'password' [FORCE]  
```  
  
## <a name="arguments"></a>Argumentos  
 ARCHIVO **='***ruta_de_acceso_al_archivo***'**  
 Especifica la ruta completa, incluido el nombre de archivo, de acceso a la clave maestra del servicio almacenado. *ruta_de_acceso_al_archivo* puede ser una ruta de acceso local o una ruta UNC a una ubicación de red.  
  
 CONTRASEÑA **='***contraseña***'**  
 Especifica la contraseña necesaria para descifrar la clave maestra de servicio que se va a importar desde un archivo.  
  
 FORCE  
 Fuerza el reemplazo de la clave maestra de servicio, a pesar del riesgo de pérdida de datos.  
  
## <a name="remarks"></a>Comentarios  
 Al restaurar la clave maestra de servicio, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] descifra todas las claves y secretos cifrados con la clave maestra de servicio actual y, a continuación, los cifra con la clave maestra de servicio cargada desde el archivo de copia de seguridad.  
  
 Si se producen errores durante cualquier descifrado, se producirán errores en la restauración. Puede utilizar la opción FORCE para omitir los errores, pero esta opción provocará la pérdida de los datos que no sea posible descifrar.  
  
> [!CAUTION]  
>  La clave maestra de servicio es la raíz de la jerarquía de cifrado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La clave maestra de servicio protege directa o indirectamente las demás claves del árbol. Si no es posible descifrar una clave dependiente durante una restauración forzada, se perderán los datos que protege la clave.  
  
 La regeneración de la jerarquía de cifrado es una operación que requiere un uso intensivo de recursos. Debe programarla durante un período de baja demanda.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso CONTROL SERVER en el servidor.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se restaura la clave maestra de servicio desde un archivo de copia de seguridad.  
  
```  
RESTORE SERVICE MASTER KEY   
    FROM FILE = 'c:\temp_backups\keys\service_master_key'   
    DECRYPTION BY PASSWORD = '3dH85Hhk003GHk2597gheij4';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Clave maestra de servicio](../../relational-databases/security/encryption/service-master-key.md)   
 [Modificar clave maestra de servicio &#40; Transact-SQL &#41;](../../t-sql/statements/alter-service-master-key-transact-sql.md)   
 [CLAVE maestra de servicio de copia de seguridad &#40; Transact-SQL &#41;](../../t-sql/statements/backup-service-master-key-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

