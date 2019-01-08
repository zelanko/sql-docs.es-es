---
title: Orígenes de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- data sources [Integration Services], about data sources
ms.assetid: 7ac81612-9822-470f-8d0f-a1dc96142fe3
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 52ea0f6e30832e285b10b3b0f284f73bb345eb65
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52823909"
---
# <a name="data-sources"></a>Orígenes de datos
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] incluye un objeto de tiempo de diseño que puede usar en los paquetes de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] : el origen de datos.  
  
 Un objeto de origen de datos es una referencia a una conexión y, como mínimo, incluye una cadena de conexión y un identificador de origen de datos. También puede incluir metadatos adicionales tales como descripción, nombre, nombre de usuario y contraseña.  
  
> [!NOTE]  
>  Puede agregar orígenes de datos solo a los proyectos configurados para utilizar el modelo de implementación de paquetes. Si se configura un proyecto para utilizar el modelo de implementación de proyectos, los administradores de conexiones creados en el nivel de proyecto se usan para compartir las conexiones, en lugar de usar orígenes de datos.  
>   
>  Para obtener más información acerca de los modelos de implementación, vea [Deployment of Projects and Packages](../packages/deploy-integration-services-ssis-projects-and-packages.md). Para obtener más información sobre cómo convertir un proyecto al modelo de implementación de proyectos, vea [Deploy Projects to Integration Services Server](../deploy-projects-to-integration-services-server.md).  
  
 Estas son algunas de las ventajas de usar orígenes de datos en paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] :  
  
-   Un origen de datos tiene ámbito de proyecto, lo que significa que un origen de datos creado en un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] está disponible para todos los paquetes del proyecto. Un origen de datos se puede definir una vez y que los administradores de conexión hagan referencia a él en varios paquetes.  
  
-   Un origen de datos ofrece sincronización entre el objeto de origen de datos y sus referencias de paquete. Si el origen de datos y los paquetes que hacen referencia a él residen en el mismo proyecto, la propiedad de la cadena de conexión de las referencias del origen de datos se actualiza automáticamente cuando se modifica el origen de datos.  
  
## <a name="reference-data-sources"></a>Hacer referencia a los orígenes de datos  
 Para agregar un objeto de origen de datos en un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , haga clic con el botón derecho en la carpeta **Orígenes de datos** y, después, haga clic en **Explorador de soluciones** y en **Nuevo origen de datos**. El elemento se agrega a la carpeta **Orígenes de datos** . Si desea usar los objetos de origen de datos que se crearon en otros proyectos, en primer lugar debe agregarlos al proyecto.  
  
 Para utilizar un objeto de origen de datos en un paquete, agregue un administrador de conexiones que haga referencia al objeto de origen de datos en el paquete. Puede agregarlo al paquete antes de crear el flujo de control y el flujo de datos del paquete, o como paso en la construcción del flujo de control o del flujo de datos.  
  
 Un objeto de origen de datos representa una simple conexión a un origen de datos y proporciona acceso a los objetos en el almacén de datos al que hace referencia. Por ejemplo, un objeto de origen de datos que se conecta a la base de datos de ejemplo AdventureWorks de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]incluye las 60 tablas de la base de datos.  
  
 No existe dependencia entre un origen de datos y los administradores de conexión que hacen referencia a él. Si el origen de datos ya no forma parte de un proyecto, los paquetes siguen siendo válidos, porque la información sobre el origen de datos, como, por ejemplo, su tipo de conexión y cadena de conexión, se incluye en la definición de paquete.  
  
  
