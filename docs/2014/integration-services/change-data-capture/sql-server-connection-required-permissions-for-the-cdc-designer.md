---
title: Permisos necesarios de conexión con SQL Server para el Diseñador CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 80334de2-17c1-43c9-951e-21a9f864e9cb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 567ee5d4c6f57d4b4eb08cbd4ecac7aef999aa55
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62835421"
---
# <a name="sql-server-connection-required-permissions-for-the-cdc-designer"></a>Permisos necesarios de conexión con SQL Server para el Diseñador CDC
  La Consola del diseñador CDC necesita información de conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para realizar sus tareas. En este tema se describe la información que se puede proporcionar en el cuadro de diálogo **Conectar con SQL Server** para configurar la conexión con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 El cuadro de diálogo **Conectar con SQL Server** se abre cuando es necesario, como cuando la información de conexión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no está disponible o si existe la información pero la conexión no tiene los permisos necesarios.  
  
 En la tabla siguiente se describen las diversas tareas en las que se necesita una conexión con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y los permisos que necesita el inicio de sesión o el usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Tarea|Permisos mínimos|  
|----------|-------------------------|  
|Ver la lista de servicios e instancias CDC usando la instancia asociada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|`db_datareader` en MSXDBCDC|  
|Iniciar y detener instancias CDC|`db_datareader` y `db_datawriter` en MSXDBCDC|  
|Ver el estado de la instancia CDC.|`db_owner` en la base de datos de la instancia CDC|  
|Crear una nueva base de datos de instancia CDC de Oracle.|`dbcreator` Rol fijo de servidor|  
|Crear una nueva instancia CDC de Oracle.|`db_datareader` en MSXDBCDC<br /><br /> `db_owner` en la base de datos CDC creada.|  
|Obtener scripts de implementación.|`db_datareader` y `db_datawriter` en MSXDBCDC<br /><br /> `db_owner` en la base de datos CDC relacionada|  
|Cambiar la configuración y agregar o quitar instancias de captura.|`db_datareader` y `db_datawriter` en MSXDBCDC<br /><br /> `db_owner` en la base de datos CDC relacionada|  
  
## <a name="see-also"></a>Consulte también  
 [Obtener acceso a la Consola del diseñador CDC](access-the-cdc-designer-console.md)   
 [Conexión de SQL Server para la creación de instancias](sql-server-connection-for-instance-creation.md)  
  
  
