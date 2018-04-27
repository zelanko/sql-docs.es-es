---
title: Conexión de SQL Server para la creación de instancias | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: change-data-capture
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 81d0e7e2-d8f0-4bd9-9565-218ce996f28e
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 72521e3cbe7057b80c89c24b82440b7b2cacd7ad
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="sql-server-connection-for-instance-creation"></a>Conexión de SQL Server para la creación de instancias
  Uno de los primeros pasos para crear una instancia CDC de Oracle es la creación de una base de datos CDC en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino. Esta base de datos CDC está habilitada para CDC de SQL Server y esta habilitación necesita un inicio de sesión que sea miembro del rol fijo de servidor `sysadmin` .  
  
 Cuando un usuario que inicia el asistente **Crear una instancia CDC de Oracle** no es miembro del rol fijo de servidor `sysadmin` , se abre el cuadro de diálogo **Conectar con SQL Server** , que pide las credenciales para un miembro del rol `sysadmin` para realizar la tarea Habilitar la base de datos para CDC de SQL Server. Cuando se crea la base de datos CDC, el inicio de sesión `sysadmin` se descarta y se reanuda el trabajo con el inicio de sesión original de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado cuando se entró en la Consola del diseñador de Oracle.  
  
## <a name="task-list"></a>Lista de tareas  
 Escriba la información siguiente en el cuadro de diálogo **Conectar con SQL Server** .  
  
 **Nombre de servidor**  
 Escriba el nombre del servidor donde se encuentra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Autenticación**  
 Seleccione una de las opciones siguientes:  
  
-   **Autenticación de Windows**  
  
-   **Autenticación de SQL Server**: si selecciona esta opción, es necesario que escriba el **Inicio de sesión** y la **Contraseña** del usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al que se conecta.  
  
 El inicio de sesión debe tener un rol de base de datos que permita el acceso a la base de datos MSXCDCDB. Se recomienda que el inicio de sesión tenga acceso también a cualquier base de datos adicional que se esté usando; de lo contrario, el usuario no podrá ver los datos de esas bases de datos.  
  
 **Opciones**  
 Haga clic en la flecha para ver las opciones disponibles que se pueden configurar. Puede elegir dejar estas opciones con el valor predeterminado. Las opciones disponibles son:  
  
-   **Tiempo de espera de la conexión**: escriba el tiempo (en segundos) que el servicio CDC para Oracle espera una conexión con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de agotarse el tiempo de espera. El valor predeterminado es **15**.  
  
-   **Tiempo de espera de ejecución**: escriba el tiempo (en segundos) que el servicio de Windows CDC de Oracle espera la ejecución de un comando antes de agotarse el tiempo de espera. El valor predeterminado es **30**.  
  
-   **Cifrar conexión**: seleccione **Cifrar conexión** para que la comunicación entre el servicio CDC de Oracle y la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino se realice mediante una conexión cifrada.  
  
-   **Avanzadas**: haga clic en **Avanzadas** y escriba cualquier propiedad de conexión adicional en el cuadro de diálogo Propiedades avanzadas de conexión, si es necesario.  
  
     Para más información sobre el cuadro de diálogo Propiedades avanzadas de conexión, vea [Propiedades avanzadas de conexión](../../integration-services/change-data-capture/advanced-connection-properties.md).  
  
## <a name="see-also"></a>Ver también  
 [Crear la base de datos de cambios de SQL Server](../../integration-services/change-data-capture/create-the-sql-server-change-database.md)   
 [Permisos necesarios de conexión con SQL Server para el Diseñador CDC](../../integration-services/change-data-capture/sql-server-connection-required-permissions-for-the-cdc-designer.md)  
  
  
