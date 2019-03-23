---
title: Obtener acceso a la Consola del diseñador CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- accMsDes
ms.assetid: b168c64e-c1b5-42d4-a92a-84de1dd0324e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c552ef16cc2f9502a365ba09c7f8868eccd53396
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58377173"
---
# <a name="access-the-cdc-designer-console"></a>Obtener acceso a la Consola del diseñador CDC
  Puede obtener acceso a la Consola del diseñador CDC desde el equipo en el que instaló la consola. Para obtener más información acerca de la instalación, vea Instalación.  
  
 Cuando abra la Consola del diseñador CDC, se abrirá el cuadro de diálogo Conectar con SQL Server.  
  
 El inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que tiene acceso al Diseñador CDC necesita tener permisos UPDATE en la base de datos MSXDBCDC. Además, el inicio de sesión debe tener también el rol fijo de servidor `dbcreator` para crear nuevas instancias CDC de Oracle. Se recomienda que el inicio de sesión tenga también acceso SELECT a las bases de datos CDC que se están usando; de lo contrario, el usuario no podrá ver el estado de esas bases de datos.  
  
 Escriba la información siguiente en el cuadro de diálogo Conectar con SQL Server.  
  
### <a name="server-name"></a>Nombre del servidor  
 Escriba el nombre del servidor donde se encuentra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="authentication"></a>Autenticación  
 Seleccione una de las opciones siguientes:  
  
-   **Autenticación de Windows**  
  
-   **Autenticación de SQL Server**: Si selecciona esta opción, debe escribir el **inicio de sesión** y **contraseña** para el usuario en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se conecta.  
  
 El inicio de sesión debe tener un rol de base de datos que permita el acceso a la base de datos MSXCDCDB. Se recomienda que el inicio de sesión tenga acceso también a cualquier base de datos adicional que se esté usando; de lo contrario, el usuario no podrá ver los datos de esas bases de datos.  
  
### <a name="options"></a>Opciones  
 Haga clic en la flecha para ver las opciones disponibles que se pueden configurar. Puede elegir dejar estas opciones con el valor predeterminado. Las opciones disponibles son:  
  
 **Tiempo de espera de la conexión**  
 Escriba el tiempo (en segundos) que el servicio CDC para Oracle espera una conexión con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de agotarse el tiempo de espera. El valor predeterminado es **15**.  
  
 **Tiempo de espera de ejecución**  
 Escriba el tiempo (en segundos) que el servicio de Windows CDC de Oracle espera que se ejecute un comando antes de agotarse el tiempo de espera. El valor predeterminado es **30**.  
  
 **Cifrar conexión**  
 Seleccione **cifrar conexión** para la comunicación entre el servicio CDC de Oracle y el destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia mediante una conexión cifrada. **Advanced**: Haga clic en **Avanzadas** y escriba cualquier propiedad de conexión adicional en el cuadro de diálogo Propiedades avanzadas de conexión, si es necesario.  
  
 **Avanzadas**  
 Haga clic en **Avanzadas** y escriba cualquier propiedad de conexión adicional en el cuadro de diálogo Propiedades avanzadas de conexión, si es necesario.  
  
 Para obtener información sobre el cuadro de diálogo Propiedades avanzadas de conexión, vea [Propiedades avanzadas de conexión](advanced-connection-properties.md).  
  
## <a name="see-also"></a>Vea también  
 [Permisos necesarios de conexión con SQL Server para el Diseñador CDC](sql-server-connection-required-permissions-for-the-cdc-designer.md)  
  
  
