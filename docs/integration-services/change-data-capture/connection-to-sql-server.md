---
title: "Conexión a SQL Server | Documentos de Microsoft"
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
ms.assetid: 5bb582f9-68d3-4c1e-ab02-6fc16807f1a5
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2f2c0ec017651177fe6bb78d7aef5df35a27b5b6
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="connection-to-sql-server"></a>Conexión con SQL Server
  Cuando un inicio de sesión sin un rol de base de datos que incluye el permiso de escritura (por ejemplo, el rol **db_owner** ) para la base de datos MSXDBCDC intenta crear una instancia CDC de Oracle, se muestra el cuadro de diálogo Conectar con SQL Server.  
  
 En este cuadro de diálogo tiene que especificar las credenciales para un inicio de sesión que tenga permiso de escritura en la base de datos MSXDBCDC, como el rol de base de datos **db_owner** , para crear una instancia CDC de Oracle.  
  
 Escriba la información siguiente en el cuadro de diálogo Conectar con SQL Server.  
  
### <a name="server-name"></a>Nombre de servidor  
 Escriba el nombre del servidor donde se encuentra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="authentication"></a>Autenticación  
 Seleccione una de las opciones siguientes:  
  
-   Autenticación de Windows  
  
-   **Autenticación de SQL Server**: si selecciona esta opción, es necesario que escriba el **Inicio de sesión** y la **Contraseña** del usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al que se conecta.  
  
### <a name="options"></a>Opciones  
 Haga clic en la flecha para ver las opciones disponibles que se pueden configurar. Puede elegir dejar estas opciones con el valor predeterminado. Las opciones disponibles son:  
  
-   **Tiempo de espera de la conexión**: escriba el tiempo (en segundos) que el programa espera hasta que se establezca una conexión con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de producir un error de tiempo de espera. El valor predeterminado es **15**.  
  
-   **Tiempo de espera de ejecución**: escriba el tiempo (en segundos) que el programa espera hasta que finalice la ejecución de un comando SQL antes de producir un error de tiempo de espera. El valor predeterminado es **30**.  
  
-   **Cifrar conexión**: seleccione **Cifrar conexión** para asegurarse de que la conexión con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se establece está cifrada para garantizar la privacidad.  
  
-   **Avanzadas**: haga clic en **Avanzadas** y escriba cualquier propiedad de conexión adicional en el cuadro de diálogo Propiedades avanzadas de conexión, si es necesario.  
  
## <a name="see-also"></a>Vea también  
 [Conexión de SQL Server los permisos necesarios para el servicio CDC](../../integration-services/change-data-capture/sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
  

