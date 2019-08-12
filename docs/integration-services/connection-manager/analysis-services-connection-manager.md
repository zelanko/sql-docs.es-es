---
title: Administrador de conexiones de Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 01/25/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], Analysis Services
- connection managers [Integration Services], Analysis Services
- Analysis Services connection manager
ms.assetid: 9f9cadad-a1d0-4db5-98f5-df5dbbec1be4
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 7cecf0294e1225dcb8f9476c1f0f3c85a0b6ab47
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892975"
---
# <a name="analysis-services-connection-manager"></a>administrador de conexiones de Analysis Services

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Un administrador de conexiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] permite que un paquete se conecte con un servidor que se ejecuta en una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o con un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que proporciona acceso a datos de cubo y dimensiones. Solo puede conectarse a un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mientras desarrolla paquetes en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Durante el tiempo de ejecución, los paquetes se conectan al servidor y la base de datos en la que se implementó el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Ambas tareas, como la tarea Ejecutar DDL de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y la tarea Procesamiento de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , y los destinos como el destino de Entrenamiento del modelo de minería de datos, usan un administrador de conexiones de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Para obtener más información sobre las bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vea [Bases de datos de modelos multidimensionales &#40;SSAS&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/multidimensional-model-databases-ssas).  
  
## <a name="configuration-of-the-analysis-services-connection-manager"></a>Configuración del administrador de conexiones de Analysis Services  
 Cuando agrega un administrador de conexiones de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a un paquete, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un administrador de conexiones que se resuelve como una conexión de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el tiempo de ejecución, establece las propiedades del administrador de conexiones y agrega el administrador de conexiones a la colección **Conexiones** del paquete. La propiedad **ConnectionManagerType** del administrador de conexiones se establece en **MSOLAP100**.  
  
 Puede configurar el administrador de conexiones de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de las maneras siguientes:  
  
-   Proporcionar una cadena de conexión configurada para cumplir con los requisitos del Proveedor Microsoft OLE DB para Analysis Services.  
  
-   Especificar la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] con el que desea conectarse.  
  
-   Si se está conectando a una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], especifique el modo de autenticación.  

> [!NOTE]    
>  Si usa SSIS en Azure Data Factory (ADF) y quiere conectarse a una instancia de Azure Analysis Services (AAS), no puede usar una cuenta con Multi-Factor Authentication (MFA) habilitado, sino que debe usar una cuenta que no requiera ninguna interactividad o MFA o una entidad de servicio en su lugar. Para usar esta última, [aquí](https://docs.microsoft.com/azure/analysis-services/analysis-services-service-principal) puede ver cómo crear una y asignarle el rol de administrador del servidor, luego seleccione **Use a specific user name and password** (Usar un nombre de usuario y una contraseña concretos) para iniciar sesión en el servidor en el administrador de conexiones y, por último, escriba `User name: app:YourApplicationID` y `Password: YourAuthorizationKey`.
  
-   Indicar si la conexión creada desde el administrador de conexiones se conserva en el tiempo de ejecución.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Referencia de la interfaz de usuario del cuadro de diálogo Agregar administrador de conexiones con Analysis Services](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 Para obtener información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
  
