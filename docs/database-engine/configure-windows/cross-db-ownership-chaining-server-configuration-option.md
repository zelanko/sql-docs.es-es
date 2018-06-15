---
title: cross db ownership chaining (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 08/15/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cross-database ownership chaining
- cross db ownership chaining option
- chaining ownership
ms.assetid: 7b2d49f2-b91c-4aee-a52b-6cc49bed03af
caps.latest.revision: 27
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1dc3e15b62eddfc2b573119c5b7bccfe45cb3ff9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32863860"
---
# <a name="cross-db-ownership-chaining-server-configuration-option"></a>cross db ownership chaining (opción de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Use la opción **Encadenamiento de propiedad entre bases de datos** para configurar el encadenamiento de propiedad entre bases de datos para una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Esta opción del servidor permite controlar el encadenamiento de propiedad entre bases de datos en el nivel de base de datos o para todas las bases de datos:  
  
-   Cuando la opción **Encadenamiento de propiedad entre bases de datos** está desactivada (0) para la instancia, el encadenamiento de propiedad entre bases de datos se deshabilita para todas las bases de datos.  
  
-   Cuando la opción **Encadenamiento de propiedad entre bases de datos** está activada (1) para la instancia, el encadenamiento de propiedad entre bases de datos se habilita para todas las bases de datos.  
  
-   Puede establecer el encadenamiento de propiedad entre bases de datos para bases de datos específicas mediante la cláusula SET de la instrucción ALTER DATABASE. Si está creando una base de datos, puede establecer la opción de encadenamiento de propiedad entre bases de datos para la nueva base de datos mediante la instrucción CREATE DATABASE.  
  
     No se recomienda establecer la opción **Encadenamiento de propiedad entre bases de datos** en 1, a menos que todas las bases de datos hospedadas por la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] participen en el encadenamiento de propiedad entre bases de datos y sepa las implicaciones de seguridad de esta opción.  

Para determinar el estado actual del encadenamiento de propiedad entre bases de datos, ejecute la siguiente consulta:  
```sql
SELECT is_db_chaining_on, name FROM sys.databases;
```  
Un resultado de 1 indica que el encadenamiento de propiedad entre bases de datos está habilitado.

## <a name="controlling-cross-database-ownership-chaining"></a>Controlar el encadenamiento de propiedad entre bases de datos  
 Antes de activar o desactivar el encadenamiento de propiedad entre bases de datos, tenga en cuenta lo siguiente:  
  
-   Debe ser miembro del rol fijo de servidor **sysadmin** para activar o desactivar el encadenamiento de propiedad entre bases de datos.  
  
-   Antes de desactivar el encadenamiento de propiedad entre bases de datos en un servidor de producción, compruebe totalmente todas las aplicaciones, incluidas las aplicaciones de otros fabricantes, para asegurarse de que los cambios no afectan a la funcionalidad de las aplicaciones.  
  
-   Puede cambiar la opción **Encadenamiento de propiedad entre bases de datos** mientras el servidor se está ejecutando si especifica RECONFIGURE con **sp_configure**.  
  
-   Si tiene bases de datos que necesitan el encadenamiento de propiedad entre bases de datos, se recomienda desactivar la opción **Encadenamiento de propiedad entre bases de datos** para la instancia mediante **sp_configure**; después, active el encadenamiento de propiedad entre bases de datos para bases de datos específicas que requieran su uso mediante la instrucción ALTER DATABASE.  
  
## <a name="see-also"></a>Ver también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  
