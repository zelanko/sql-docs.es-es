---
title: Características desactivado de forma predeterminada (Analysis Services) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bb6abe864cd3ff8b63fefde07c9b70e98696bab4
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="features-off-by-default-analysis-services"></a>Características desactivadas de manera predeterminada (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] está diseñada para que sea segura de forma predeterminada. Por lo tanto, las características que comprometen la seguridad se deshabilitan de forma predeterminada. Las siguientes características están instaladas en estado deshabilitado y deben habilitarse específicamente si se desean utilizar.  
  
## <a name="feature-list"></a>Lista de características  
 Para habilitar las siguientes características, conéctese a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Haga clic con el botón derecho en el nombre de la instancia y seleccione **Facetas**. También puede habilitar estas características utilizando las propiedades del servidor, como se describe en la sección siguiente.  
  
-   Consultas ad hoc de minería de datos (OpenRowset)  
  
-   Objetos vinculados (a)  
  
-   Objetos vinculados (desde)  
  
-   Escuchar solo en conexiones locales  
  
-   Funciones definidas por el usuario  
  
## <a name="server-properties"></a>Propiedades del servidor  
 Otras características que están deshabilitadas de manera predeterminada se pueden habilitar mediante las propiedades del servidor. Conéctese a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Haga clic con el botón derecho en el nombre de la instancia y seleccione **Propiedades**. Haga clic en **General**y, a continuación, haga clic en **Mostrar avanzadas** para visualizar una lista de propiedades más extensa.  
  
-   Consultas ad hoc de minería de datos (OpenRowset)  
  
-   Permitir modelos de minería de datos de sesión (minería de datos)  
  
-   Objetos vinculados (a)  
  
-   Objetos vinculados (desde)  
  
-   Funciones definidas por el usuario basadas en COM  
  
-   Definición de seguimiento de la Caja negra (plantillas).  
  
-   Registro de consultas  
  
-   Escuchar solo en conexiones locales  
  
-   XML binario  
  
-   Compresión  
  
-   Afinidad del grupo. Para obtener información detallada, vea [Thread Pool Properties](../../analysis-services/server-properties/thread-pool-properties.md) .  
  
  
