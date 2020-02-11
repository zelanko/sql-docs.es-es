---
title: cross db ownership chaining (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- cross-database ownership chaining
- cross db ownership chaining option
- chaining ownership
ms.assetid: 7b2d49f2-b91c-4aee-a52b-6cc49bed03af
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5630579e787a3bfcb5d64ee3bcf0ec5bee368611
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62782402"
---
# <a name="cross-db-ownership-chaining-server-configuration-option"></a>cross db ownership chaining (opción de configuración del servidor)
  Use la opción **Encadenamiento de propiedad entre bases de datos** para configurar el encadenamiento de propiedad entre bases de datos para una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Esta opción del servidor permite controlar el encadenamiento de propiedad entre bases de datos en el nivel de base de datos o para todas las bases de datos:  
  
-   Cuando la opción **Encadenamiento de propiedad entre bases de datos** está desactivada (0) para la instancia, el encadenamiento de propiedad entre bases de datos se deshabilita para todas las bases de datos.  
  
-   Cuando la opción **Encadenamiento de propiedad entre bases de datos** está activada (1) para la instancia, el encadenamiento de propiedad entre bases de datos se habilita para todas las bases de datos.  
  
-   Puede establecer el encadenamiento de propiedad entre bases de datos para bases de datos específicas mediante la cláusula SET de la instrucción ALTER DATABASE. Si está creando una base de datos, puede establecer la opción de encadenamiento de propiedad entre bases de datos para la nueva base de datos mediante la instrucción CREATE DATABASE.  
  
     No se recomienda establecer la opción **Encadenamiento de propiedad entre bases de datos** en 1, a menos que todas las bases de datos hospedadas por la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] participen en el encadenamiento de propiedad entre bases de datos y sepa las implicaciones de seguridad de esta opción.  
  
## <a name="controlling-cross-database-ownership-chaining"></a>Controlar el encadenamiento de propiedad entre bases de datos  
 Antes de activar o desactivar el encadenamiento de propiedad entre bases de datos, tenga en cuenta lo siguiente:  
  
-   Debe ser miembro del rol fijo de servidor **sysadmin** para activar o desactivar el encadenamiento de propiedad entre bases de datos.  
  
-   Antes de desactivar el encadenamiento de propiedad entre bases de datos en un servidor de producción, compruebe totalmente todas las aplicaciones, incluidas las aplicaciones de otros fabricantes, para asegurarse de que los cambios no afectan a la funcionalidad de las aplicaciones.  
  
-   Puede cambiar la opción **Encadenamiento de propiedad entre bases de datos** mientras el servidor se está ejecutando si especifica RECONFIGURE con **sp_configure**.  
  
-   Si tiene bases de datos que necesitan el encadenamiento de propiedad entre bases de datos, se recomienda desactivar la opción **Encadenamiento de propiedad entre bases de datos** para la instancia mediante **sp_configure**; después, active el encadenamiento de propiedad entre bases de datos para bases de datos específicas que requieran su uso mediante la instrucción ALTER DATABASE.  
  
## <a name="see-also"></a>Consulte también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)  
  
  
