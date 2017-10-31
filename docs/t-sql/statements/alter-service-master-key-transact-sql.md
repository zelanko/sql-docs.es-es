---
title: ALTER SERVICE MASTER KEY (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_SERVICE_MASTER_KEY_TSQL
- ALTER SERVICE MASTER KEY
dev_langs:
- TSQL
helpviewer_keywords:
- REGENERATE phrase
- FORCE option
- ALTER SERVICE MASTER KEY statement
- cryptography [SQL Server], Service Master Key
- modifying Service Master Key
- decryption [SQL Server], Service Master Key
- encryption [SQL Server], Service Master Key
- service master key [SQL Server], modifying
ms.assetid: a1e9be0e-4115-47d8-9d3a-3316d876a35e
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4ee9fd8a888ed796b4d01b007aec5f8217cce5d9
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="alter-service-master-key-transact-sql"></a>ALTER SERVICE MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia la clave maestra de servicio de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ALTER SERVICE MASTER KEY   
    [ { <regenerate_option> | <recover_option> } ] [;]  
  
<regenerate_option> ::=  
    [ FORCE ] REGENERATE  
  
<recover_option> ::=  
    { WITH OLD_ACCOUNT = 'account_name' , OLD_PASSWORD = 'password' }  
    |      
    { WITH NEW_ACCOUNT = 'account_name' , NEW_PASSWORD = 'password' }  
```  
  
## <a name="arguments"></a>Argumentos  
 FORCE  
 Indica que la clave maestra de servicio debe volver a generarse, a pesar del riesgo de perder datos. Para obtener más información, consulte [cambiar la cuenta de servicio de SQL Server](#_changing) más adelante en este tema.  
  
 REGENERATE  
 Indica que la clave maestra de servicio debe volver a generarse.  
  
 OLD_ACCOUNT **='***account_name***'**  
 Especifica el nombre de la antigua cuenta de servicio de Windows.  
  
> [!WARNING]  
>  Esta opción es obsoleta. No debe usarse. Utilice el administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en su lugar.  
  
 Contraseña_anterior **='***contraseña***'**  
 Especifica la contraseña de la antigua cuenta de servicio de Windows.  
  
> [!WARNING]  
>  Esta opción es obsoleta. No debe usarse. Utilice el administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en su lugar.  
  
 NEW_ACCOUNT **='***account_name***'**  
 Especifica el nombre de la nueva cuenta de servicio de Windows.  
  
> [!WARNING]  
>  Esta opción es obsoleta. No debe usarse. Utilice el administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en su lugar.  
  
 Nuevacontraseña **='***contraseña***'**  
 Especifica la contraseña de la nueva cuenta de servicio de Windows.  
  
> [!WARNING]  
>  Esta opción es obsoleta. No debe usarse. Utilice el administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en su lugar.  
  
## <a name="remarks"></a>Comentarios  
 La clave maestra de servicio se vuelve a generar automáticamente la primera vez que se necesita para cifrar una contraseña de servidor vinculado, una credencial o una clave maestra de base de datos. La clave maestra del servicio se cifra mediante la clave del equipo local o la API de protección de datos de Windows. Esta API usa una clave derivada de las credenciales de Windows de la cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] usa el algoritmo de cifrado AES para proteger la clave maestra de servicio (SMK) y la clave maestra de la base de datos (DMK). AES es un algoritmo de cifrado más reciente que el algoritmo 3DES empleado en versiones anteriores. Después de actualizar una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], se deben volver a generar las claves SMK y DMK para actualizar las claves maestras al algoritmo AES. Para obtener más información sobre cómo volver a generar la DMK, vea [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md).  
  
##  <a name="_changing"></a>Cambiar la cuenta de servicio SQL Server  
 Para cambiar la cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para administrar un cambio de la cuenta de servicio, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] almacena una copia redundante de la clave maestra de servicio protegida por la cuenta de equipo que tenga los permisos necesarios concedidos al grupo de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si se vuelve a generar el equipo, el mismo usuario de dominio que la cuenta de servicio utilizaba previamente puede recuperar la clave maestra de servicio. Esto no funciona con cuentas locales o las cuentas del sistema Local, servicio Local o servicio de red. Cuando vaya a mover [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a otro equipo, migrar la clave maestra de servicio mediante la copia de seguridad y restauración.  
  
 La frase REGENERATE vuelve a generar la clave maestra de servicio. Si se vuelve a generar la clave maestra de servicio, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] descifra todas las claves cifradas con ella y, a continuación, vuelve a cifrarlas con la nueva clave maestra de servicio. Es una operación que requiere un uso intensivo de los recursos. Por ello, debe programarse durante un período de poco uso, a menos que la clave se encuentre en peligro. Si se producen errores durante alguno de los descifrados, se producirán errores en toda la instrucción.  
  
 La opción FORCE hace que el proceso para volver a generar la clave continúe aunque no pueda recuperar la clave maestra actual o no pueda descifrar todas las claves privadas cifradas con ella. Utilice FORCE solo si se produce un error en la regeneración y no se puede restaurar la clave maestra de servicio mediante el uso de la [RESTORE SERVICE MASTER KEY](../../t-sql/statements/restore-service-master-key-transact-sql.md) instrucción.  
  
> [!CAUTION]  
>  La clave maestra de servicio es la raíz de la jerarquía de cifrado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La clave maestra de servicio protege directa o indirectamente las demás claves y secretos del árbol. Si no es posible descifrar una clave dependiente durante una regeneración forzada, se perderán los datos que protege la clave.  
  
 Si mueve SQL a otro equipo, tiene que usar la misma cuenta de servicio para descifrar la SMK; SQL Server corregirá el cifrado de la cuenta de equipo automáticamente.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso CONTROL SERVER en el servidor.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se vuelve a generar la clave maestra de servicio.  
  
```  
ALTER SERVICE MASTER KEY REGENERATE;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [RESTAURAR la clave maestra de servicio &#40; Transact-SQL &#41;](../../t-sql/statements/restore-service-master-key-transact-sql.md)   
 [CLAVE maestra de servicio de copia de seguridad &#40; Transact-SQL &#41;](../../t-sql/statements/backup-service-master-key-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

