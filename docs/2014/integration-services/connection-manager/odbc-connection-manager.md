---
title: Administrador de conexiones ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], ODBC
- ODBC connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], ODBC
ms.assetid: e8c77aa7-6772-485e-918e-cef9eeb18c58
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 701ea85cafc22d9ea850e18310c3c2d06748cb08
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85438362"
---
# <a name="odbc-connection-manager"></a>ODBC, administrador de conexiones
  Un administrador de conexiones ODBC habilita un paquete para conectarse a una serie de sistemas de administración de bases de datos mediante la especificación Conectividad abierta de bases de datos (ODBC).  
  
 Cuando agrega una conexión ODBC a un paquete y establece las propiedades del administrador de conexiones, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un administrador de conexiones y agrega el administrador de conexiones a la `Connections` colección del paquete. En el tiempo de ejecución el administrador de conexiones se resuelve como una conexión ODBC física.  
  
 La propiedad `ConnectionManagerType` del administrador de conexiones se establece en `ODBC`.  
  
 Puede configurar el administrador de conexiones ODBC de las maneras siguientes:  
  
-   Proporcionar una cadena de conexión que haga referencia a un nombre del origen de datos de sistema o usuario.  
  
-   Especificar el servidor al que debe conectarse.  
  
-   Indicar si la conexión se conserva en tiempo de ejecución.  
  
## <a name="configuration-of-the-odbc-connection-manager"></a>Configuración del administrador de conexiones ODBC  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Referencia de la interfaz de usuario del administrador de conexiones ODBC](../odbc-connection-manager-ui-reference.md)  
  
 Para obtener información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Consulte también  
 [Conexiones de Integration Services &#40;SSIS&#41;](integration-services-ssis-connections.md)  
  
  
