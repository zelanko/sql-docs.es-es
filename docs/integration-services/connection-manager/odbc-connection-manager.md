---
description: ODBC, administrador de conexiones
title: Administrador de conexiones ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.odbcconnection.f1
helpviewer_keywords:
- connections [Integration Services], ODBC
- ODBC connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], ODBC
ms.assetid: e8c77aa7-6772-485e-918e-cef9eeb18c58
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7fe63ad503b49a760823635902b3744a1ae2d85a
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/26/2020
ms.locfileid: "91719645"
---
# <a name="odbc-connection-manager"></a>ODBC, administrador de conexiones

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Un administrador de conexiones ODBC habilita un paquete para conectarse a una serie de sistemas de administración de bases de datos mediante la especificación Conectividad abierta de bases de datos (ODBC).  
  
 Cuando agrega una conexión ODBC a un paquete y establece las propiedades de administrador de conexiones, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un administrador de conexiones y lo agrega a la colección **Connections** del paquete. En el tiempo de ejecución el administrador de conexiones se resuelve como una conexión ODBC física.  
  
 La propiedad **ConnectionManagerType** del administrador de conexiones se establece en **ODBC**.  
  
 Puede configurar el administrador de conexiones ODBC de las maneras siguientes:  
  
-   Proporcionar una cadena de conexión que haga referencia a un nombre del origen de datos de sistema o usuario.  
  
-   Especificar el servidor al que debe conectarse.  
  
-   Indicar si la conexión se conserva en tiempo de ejecución.  
  
## <a name="configuration-of-the-odbc-connection-manager"></a>Configuración del administrador de conexiones ODBC  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Referencia de la interfaz de usuario del administrador de conexiones ODBC]()  
  
 Para obtener información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="odbc-connection-manager-ui-reference"></a>Referencia de la interfaz de usuario del administrador de conexiones ODBC
  Utilice el cuadro de diálogo **Configurar el administrador de conexiones ODBC** para agregar una conexión a un origen de datos ODBC.  
  
 Para obtener más información acerca del administrador de conexiones ODBC, vea [ODBC Connection Manager](../../integration-services/connection-manager/odbc-connection-manager.md).  
  
### <a name="options"></a>Opciones  
 **Conexiones de datos**  
 Seleccione un administrador de conexiones ODBC existente en la lista.  
  
 **Propiedades de conexión de datos**  
 Muestra las propiedades y valores del administrador de conexiones ODBC seleccionado.  
  
 **Nuevo**  
 Crea un administrador de conexiones ODBC mediante el cuadro de diálogo **Administrador de conexiones** . Este cuadro de diálogo también permite crear un nuevo origen de datos ODBC si es necesario.  
  
 **Eliminar**  
 Seleccione una conexión y elimínela con el botón **Eliminar** .  
## <a name="see-also"></a>Vea también  
 [Conexiones de Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
