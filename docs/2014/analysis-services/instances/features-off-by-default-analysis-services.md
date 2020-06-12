---
title: Características desactivadas de forma predeterminada (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a9529edf-337e-4fdd-9a13-99cfe96b4fa1
author: minewiskan
ms.author: owend
ms.openlocfilehash: a71a43eaced5100d48a386c60d39254b1266aaef
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84543927"
---
# <a name="features-off-by-default-analysis-services"></a>Características desactivadas de manera predeterminada (Analysis Services)
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
  
-   Afinidad del grupo. Para obtener información detallada, vea [Thread Pool Properties](../server-properties/thread-pool-properties.md) .  
  
  
