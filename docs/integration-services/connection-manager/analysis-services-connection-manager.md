---
title: Administrador de conexiones de Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: connection-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], Analysis Services
- connection managers [Integration Services], Analysis Services
- Analysis Services connection manager
ms.assetid: 9f9cadad-a1d0-4db5-98f5-df5dbbec1be4
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ae8da583d883bbcaf3665f647495ed3e016a9cb1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="analysis-services-connection-manager"></a>administrador de conexiones de Analysis Services
  Un administrador de conexiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] permite que un paquete se conecte con un servidor que se ejecuta en una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o con un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que proporciona acceso a datos de cubo y dimensiones. Solo puede conectarse a un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mientras desarrolla paquetes en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Durante el tiempo de ejecución, los paquetes se conectan al servidor y la base de datos en la que se implementó el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Ambas tareas, como la tarea Ejecutar DDL de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y la tarea Procesamiento de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , y los destinos como el destino de Entrenamiento del modelo de minería de datos, usan un administrador de conexiones de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Para obtener más información sobre las bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vea [Bases de datos de modelos multidimensionales &#40;SSAS&#41;](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md).  
  
## <a name="configuration-of-the-analysis-services-connection-manager"></a>Configuración del administrador de conexiones de Analysis Services  
 Cuando agrega un administrador de conexiones de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a un paquete, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un administrador de conexiones que se resuelve como una conexión de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el tiempo de ejecución, establece las propiedades del administrador de conexiones y agrega el administrador de conexiones a la colección **Conexiones** del paquete. La propiedad **ConnectionManagerType** del administrador de conexiones se establece en **MSOLAP100**.  
  
 Puede configurar el administrador de conexiones de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de las maneras siguientes:  
  
-   Proporcionar una cadena de conexión configurada para cumplir con los requisitos del Proveedor Microsoft OLE DB para Analysis Services.  
  
-   Especificar la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] con el que desea conectarse.  
  
-   Si se está conectando a una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], especifique el modo de autenticación.  
  
-   Indicar si la conexión creada desde el administrador de conexiones se conserva en el tiempo de ejecución.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Referencia de la interfaz de usuario del cuadro de diálogo Agregar administrador de conexiones con Analysis Services](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 Para obtener información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
  
