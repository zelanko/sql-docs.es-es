---
title: Change Data Capture Service para Oracle de Attunity | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 22ec8a5c-9550-4d38-8a4a-485ec3e53ea8
caps.latest.revision: "21"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5438d58a852f5f61cd45b3f9b74a7a7ed5383c47
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="change-data-capture-service-for-oracle-by-attunity"></a>Servicio de captura de datos modificados para Oracle de Attunity
  El servicio CDC para Oracle es un servicio de Windows que examina los registros de transacciones de Oracle y captura los cambios a las tablas de Oracle deseadas en tablas de cambios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Las tablas de cambios de SQL donde se almacenan los cambios capturados de Oracle son el mismo tipo de tablas de cambios empleadas en la característica de captura de datos modificados nativa de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esto hace que el uso de estos cambios sea tan sencillo como el de los cambios realizados a las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="installation"></a>Installation  
 El servicio y el diseñador de captura de datos modificados para Oracle de Attunity de Microsoft® para Microsoft SQL Server® 2016 forman parte del Feature Pack de SQL Server 2016. Descargue los componentes del Feature Pack, en la [página web de SQL Server 2016 Feature Pack](http://go.microsoft.com/fwlink/?LinkId=746297).  
  
 El servicio CDC para Oracle se puede instalar en cualquier equipo compatible con Windows que tenga acceso a las bases de datos de origen de Oracle que se van a capturar y a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino donde reside la base de datos CDC de destino. El servicio CDC no necesita ninguna instalación local de la base de datos de Oracle ni de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , solo sus clientes compatibles. Para obtener información acerca de dónde instalar los componentes de base de datos necesarios, vea **Requisitos previos de la base de datos** en este tema.  
  
 La instalación del servicio CDC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para Oracle coloca la interfaz de usuario de configuración del servicio y el programa de servicio en la ubicación seleccionada. El servicio CDC para Oracle se configura de forma independiente mediante la Consola de configuración del servicio CDC de Oracle. Para obtener más información acerca de cómo configurar el servicio CDC de Oracle, vea [Change Data Capture Service for Oracle by Attunity F1 Help](../../integration-services/change-data-capture/change-data-capture-service-for-oracle-by-attunity-f1-help.md).  
  
 El servicio CDC para Oracle se puede instalar en cualquier equipo compatible con Windows donde esté instalado [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client; no es necesario instalarlo en el mismo equipo donde está instalado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino.  
  
## <a name="supported-windows-environments"></a>Entornos de Windows admitidos  
 El Servicio de captura de datos modificados para Oracle de Attunity se puede ejecutar en los entornos de Windows siguientes:  
  
-   Windows 8 y 8.1  
-   Windows 10  
-   Windows Server 2012 y 2012 R2
-   Windows Server 2016
  
## <a name="database-prerequisites"></a>Requisitos previos de la base de datos  
 Para trabajar con el servicio CDC para Oracle debe instalar el software de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client Oracle. Se trata de un requisito previo que se debe obtener de Oracle e instalar antes de instalar el servicio CDC de Oracle. Además, debe instalar el cliente ODBC de SQL Server mediante el programa de instalación de SQL Server.  
  
 El servicio CDC para Oracle admite las versiones siguientes:  
  
### <a name="source-oracle-database"></a>Base de datos de Oracle de origen  
  
-   Oracle Database 10g versión 2
-   Oracle Database 11g versión 1 y versión 2
-   Oracle Database 12C en instalación clásica. (La instalación de tipo multiinquilino no es compatible).  
  
### <a name="target-sql-server-database"></a>Base de datos de SQL Server de destino  
 Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
## <a name="running-the-installation-program"></a>Ejecutar el programa de instalación  
 Para instalar el servicio CDC para Oracle, abra el asistente para la instalación para la plataforma Windows que esté usando (32 o 64 bits) y siga las instrucciones de la pantalla.  
  
## <a name="uninstalling-change-data-capture-service-for-oracle-by-attunity"></a>Desinstalar el servicio de captura de datos modificados para Oracle de Attunity  
 La desinstalación del servicio CDC para Oracle se realiza mediante Panel de control, Programas y características.  
  
 Al desinstalar el servicio CDC no se eliminan las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creadas. Para quitar completamente la herramienta, debe quitar la base de datos MSXDBCDC y las bases de datos CDC específicas que se crearon en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino con la que trabajó.  
  
 Si desinstala el software del servicio CDC de un equipo y lo instala en otro equipo, solo tiene que proporcionar las definiciones siguientes:  
  
-   Cuenta de servicio  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Cadena de conexión y credenciales  
  
-   La contraseña maestra  
  
 Todas las demás definiciones están almacenadas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y están disponibles de la instalación anterior en el otro equipo.  
  
## <a name="in-this-documentation"></a>En esta documentación  
  
-   [Servicio de captura de datos modificados para Oracle de Attunity (Arquitectura del sistema)](../../integration-services/change-data-capture/change-data-capture-service-for-oracle-by-attunity-system-architecture.md)  
  
-   [El servicio CDC de Oracle](../../integration-services/change-data-capture/the-oracle-cdc-service.md)  
  
-   [Change Data Capture Service for Oracle by Attunity F1 Help](../../integration-services/change-data-capture/change-data-capture-service-for-oracle-by-attunity-f1-help.md)  
  
-   [Servicio de captura de datos modificados para Oracle de Attunity (Guía de procedimientos)](../../integration-services/change-data-capture/change-data-capture-service-for-oracle-by-attunity-how-to-guide.md)  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con el servicio CDC de Oracle](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md)  
  
  
