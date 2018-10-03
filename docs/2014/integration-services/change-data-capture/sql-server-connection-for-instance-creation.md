---
title: Conexión de SQL Server para la creación de instancias | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 81d0e7e2-d8f0-4bd9-9565-218ce996f28e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2a5cff935637ed8f95aaf05d4d369286e679f511
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48164811"
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
  
     Para más información sobre el cuadro de diálogo Propiedades avanzadas de conexión, vea [Propiedades avanzadas de conexión](advanced-connection-properties.md).  
  
## <a name="see-also"></a>Vea también  
 [Crear la base de datos de cambio SQL Server](create-the-sql-server-change-database.md)   
 [Permisos necesarios de conexión con SQL Server para el Diseñador CDC](sql-server-connection-required-permissions-for-the-cdc-designer.md)  
  
  
