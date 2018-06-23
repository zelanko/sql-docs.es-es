---
title: Administrador de conexiones ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- connections [Integration Services], ODBC
- ODBC connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], ODBC
ms.assetid: e8c77aa7-6772-485e-918e-cef9eeb18c58
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9453dc6e402fce60e1f4f440d84f882e513abea7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112735"
---
# <a name="odbc-connection-manager"></a>ODBC, administrador de conexiones
  Un administrador de conexiones ODBC habilita un paquete para conectarse a una serie de sistemas de administración de bases de datos mediante la especificación Conectividad abierta de bases de datos (ODBC).  
  
 Al agregar una conexión ODBC a un paquete y establecer la conexión de propiedades del administrador, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una conexión de administrador y agrega el Administrador de conexiones para el `Connections` recopilación del paquete. En el tiempo de ejecución el administrador de conexiones se resuelve como una conexión ODBC física.  
  
 El `ConnectionManagerType` propiedad del Administrador de conexiones se establece en `ODBC`.  
  
 Puede configurar el administrador de conexiones ODBC de las maneras siguientes:  
  
-   Proporcionar una cadena de conexión que haga referencia a un nombre del origen de datos de sistema o usuario.  
  
-   Especificar el servidor al que debe conectarse.  
  
-   Indicar si la conexión se conserva en tiempo de ejecución.  
  
## <a name="configuration-of-the-odbc-connection-manager"></a>Configuración del administrador de conexiones ODBC  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Referencia de interfaz de usuario de administrador de conexiones de ODBC](../odbc-connection-manager-ui-reference.md)  
  
 Para obtener información acerca de cómo configurar un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [agregar conexiones mediante programación](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Vea también  
 [Servicios de integración &#40;SSIS&#41; conexiones](integration-services-ssis-connections.md)  
  
  