---
title: Obtener acceso a la Consola del diseñador CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- accMsDes
ms.assetid: b168c64e-c1b5-42d4-a92a-84de1dd0324e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 57e8a0986fda07fb0850172497f27af2618dd962
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65729128"
---
# <a name="access-the-cdc-designer-console"></a>Obtener acceso a la Consola del diseñador CDC

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Puede obtener acceso a la Consola del diseñador CDC desde el equipo en el que instaló la consola. Para obtener más información acerca de la instalación, vea Instalación.  
  
 Cuando abra la Consola del diseñador CDC, se abrirá el cuadro de diálogo Conectar con SQL Server.  
  
 El inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que tiene acceso al Diseñador CDC necesita tener permisos UPDATE en la base de datos MSXDBCDC. Además, el inicio de sesión debe tener también el rol fijo de servidor `dbcreator` para crear nuevas instancias CDC de Oracle. Se recomienda que el inicio de sesión tenga también acceso SELECT a las bases de datos CDC que se están usando; de lo contrario, el usuario no podrá ver el estado de esas bases de datos.  
  
 Escriba la información siguiente en el cuadro de diálogo Conectar con SQL Server.  
  
### <a name="server-name"></a>Nombre del servidor  
 Escriba el nombre del servidor donde se encuentra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="authentication"></a>Autenticación  
 Seleccione una de las opciones siguientes:  
  
-   **Autenticación de Windows**  
  
-   **Autenticación de SQL Server**: si selecciona esta opción, es necesario que escriba el **inicio de sesión** y la **contraseña** del usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al que se va a conectar.  
  
 El inicio de sesión debe tener un rol de base de datos que permita el acceso a la base de datos MSXCDCDB. Se recomienda que el inicio de sesión tenga acceso también a cualquier base de datos adicional que se esté usando; de lo contrario, el usuario no podrá ver los datos de esas bases de datos.  
  
### <a name="options"></a>Opciones  
 Haga clic en la flecha para ver las opciones disponibles que se pueden configurar. Puede elegir dejar estas opciones con el valor predeterminado. Las opciones disponibles son:  
  
 **Tiempo de espera de la conexión**  
 Escriba el tiempo (en segundos) que el servicio CDC para Oracle espera una conexión con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de agotarse el tiempo de espera. El valor predeterminado es **15**.  
  
 **Tiempo de espera de ejecución**  
 Escriba el tiempo (en segundos) que el servicio de Windows CDC de Oracle espera que se ejecute un comando antes de agotarse el tiempo de espera. El valor predeterminado es **30**.  
  
 **Cifrar conexión**  
 Seleccione **Cifrar conexión** para que la comunicación entre el servicio CDC de Oracle y la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino se realice mediante una conexión cifrada.**Avanzadas**: Haga clic en **Avanzadas** y escriba cualquier propiedad de conexión adicional en el cuadro de diálogo Propiedades avanzadas de conexión, si es necesario.  
  
 **Avanzadas**  
 Haga clic en **Avanzadas** y escriba cualquier propiedad de conexión adicional en el cuadro de diálogo Propiedades avanzadas de conexión, si es necesario.  
  
 Para obtener información sobre el cuadro de diálogo Propiedades avanzadas de conexión, vea [Propiedades avanzadas de conexión](../../integration-services/change-data-capture/advanced-connection-properties.md).  
  
## <a name="see-also"></a>Consulte también  
 [Permisos necesarios de conexión con SQL Server para el Diseñador CDC](../../integration-services/change-data-capture/sql-server-connection-required-permissions-for-the-cdc-designer.md)  
  
  
