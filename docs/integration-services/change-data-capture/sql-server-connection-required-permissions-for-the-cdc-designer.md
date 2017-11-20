---
title: "Conexión de SQL Server los permisos necesarios para el diseñador CDC | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 80334de2-17c1-43c9-951e-21a9f864e9cb
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bdcee015ce6c936b3fc8b8653b21208bdee31074
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

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
|Crear una nueva base de datos de instancia CDC de Oracle.|`dbcreator` rol fijo de servidor|  
|Crear una nueva instancia CDC de Oracle.|`db_datareader` en MSXDBCDC<br /><br /> `db_owner` en la base de datos CDC creada.|  
|Obtener scripts de implementación.|`db_datareader` y `db_datawriter` en MSXDBCDC<br /><br /> `db_owner` en la base de datos CDC relacionada|  
|Cambiar la configuración y agregar o quitar instancias de captura.|`db_datareader` y `db_datawriter` en MSXDBCDC<br /><br /> `db_owner` en la base de datos CDC relacionada|  
  
## <a name="see-also"></a>Vea también  
 [Obtener acceso a la consola del diseñador CDC](../../integration-services/change-data-capture/access-the-cdc-designer-console.md)   
 [Conexión de SQL Server para la instancia de creación](../../integration-services/change-data-capture/sql-server-connection-for-instance-creation.md)  
  
  

