---
title: "Obtener acceso a la consola del diseñador CDC | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- accMsDes
ms.assetid: b168c64e-c1b5-42d4-a92a-84de1dd0324e
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e1266809582119e6316b821c54f93f4217c21316
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="access-the-cdc-designer-console"></a>Obtener acceso a la Consola del diseñador CDC
  Puede obtener acceso a la Consola del diseñador CDC desde el equipo en el que instaló la consola. Para obtener más información acerca de la instalación, vea Instalación.  
  
 Cuando abra la Consola del diseñador CDC, se abrirá el cuadro de diálogo Conectar con SQL Server.  
  
 El inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que tiene acceso al Diseñador CDC necesita tener permisos UPDATE en la base de datos MSXDBCDC. Además, el inicio de sesión debe tener también el rol fijo de servidor `dbcreator` para crear nuevas instancias CDC de Oracle. Se recomienda que el inicio de sesión tenga también acceso SELECT a las bases de datos CDC que se están usando; de lo contrario, el usuario no podrá ver el estado de esas bases de datos.  
  
 Escriba la información siguiente en el cuadro de diálogo Conectar con SQL Server.  
  
### <a name="server-name"></a>Nombre de servidor  
 Escriba el nombre del servidor donde se encuentra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="authentication"></a>Autenticación  
 Seleccione una de las opciones siguientes:  
  
-   **Autenticación de Windows**  
  
-   **Autenticación de SQL Server**: si selecciona esta opción, es necesario que escriba el **Inicio de sesión** y la **Contraseña** del usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al que se conecta.  
  
 El inicio de sesión debe tener un rol de base de datos que permita el acceso a la base de datos MSXCDCDB. Se recomienda que el inicio de sesión tenga acceso también a cualquier base de datos adicional que se esté usando; de lo contrario, el usuario no podrá ver los datos de esas bases de datos.  
  
### <a name="options"></a>Opciones  
 Haga clic en la flecha para ver las opciones disponibles que se pueden configurar. Puede elegir dejar estas opciones con el valor predeterminado. Las opciones disponibles son:  
  
 **Tiempo de espera de la conexión**  
 Escriba el tiempo (en segundos) que el servicio CDC para Oracle espera una conexión con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de agotarse el tiempo de espera. El valor predeterminado es **15**.  
  
 **Tiempo de espera de ejecución**  
 Escriba el tiempo (en segundos) que el servicio de Windows CDC de Oracle espera que se ejecute un comando antes de agotarse el tiempo de espera. El valor predeterminado es **30**.  
  
 **Cifrar conexión**  
 Seleccione **Cifrar conexión** para que la comunicación entre el servicio CDC de Oracle y la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino se realice con una conexión cifrada.**Avanzadas**: haga clic en **Avanzadas** y escriba cualquier propiedad de conexión adicional en el cuadro de diálogo Propiedades avanzadas de conexión, si es necesario.  
  
 **Avanzadas**  
 Haga clic en **Avanzadas** y escriba cualquier propiedad de conexión adicional en el cuadro de diálogo Propiedades avanzadas de conexión, si es necesario.  
  
 Para obtener información sobre el cuadro de diálogo Propiedades avanzadas de conexión, vea [Propiedades avanzadas de conexión](../../integration-services/change-data-capture/advanced-connection-properties.md).  
  
## <a name="see-also"></a>Vea también  
 [Conexión de SQL Server los permisos necesarios para el diseñador CDC](../../integration-services/change-data-capture/sql-server-connection-required-permissions-for-the-cdc-designer.md)  
  
  
