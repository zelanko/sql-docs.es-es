---
title: "Cambios recientes en las caracter&#237;sticas de Analysis Services en SQL Server 2016 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "principales cambios [Analysis Services]"
  - "actualizar Analysis Services"
ms.assetid: aeb02542-5a6c-458c-a110-13413dd3e9d9
caps.latest.revision: 55
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 53
---
# Cambios recientes en las caracter&#237;sticas de Analysis Services en SQL Server 2016
  Un *cambio brusco* hace que un modelo de datos, el código de aplicación o el script dejen de funcionar después de actualizar el modelo o el servidor.  
  
> [!NOTE]  
>  En cambio, un *cambio de comportamiento* se considera como un cambio de código que no interrumpe un modelo o una aplicación, sino que introduce un compartimiento distinto con respecto a una versión anterior.  Los ejemplos de cambios de comportamiento pueden incluir un valor predeterminado, o bien impedir una configuración de propiedades u opciones que se permitían anteriormente. Para más información sobre los cambios de comportamiento en esta versión, vea [Behavior Changes to Analysis Services Features in SQL Server 2016](../analysis-services/behavior-changes-to-analysis-services-features-in-sql-server-2016.md).  
  
## Actualización de la versión de .NET 4.0  
 Ahora, Objetos de administración de Analysis Services (AMO), ADOMD.NET y las bibliotecas de cliente del modelo de objetos tabulares (TOM) en [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] tienen como destino el tiempo de ejecución de .NET 4.0. Esto puede ser un cambio importante para las aplicaciones que tienen como destino .NET 3.5. Las aplicaciones que usan versiones más recientes de estos ensamblados ahora deben tener como destino .NET 4.0 o versiones posteriores.  
  
## Actualización de la versión de AMO  
 [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] es una actualización de versión para [Objetos de administración de Analysis Services &#40;AMO&#41;](../Topic/Analysis%20Services%20Management%20Objects%20\(AMO\).md) y, en determinadas circunstancias, se trata de un cambio importante.  Los scripts y el código existentes que llaman a AMO seguirán ejecutándose como antes si actualiza desde una versión anterior. Sin embargo, si necesita *recompilar* la aplicación y se dirige a una instancia de [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] , debe agregar el siguiente espacio de nombres para que el código o el script estén operativos:  
  
```  
  
using Microsoft.AnalysisServices;  
using Microsoft.AnalysisServices.Core;  
  
```  
  
 El espacio de nombres [Microsoft.AnalysisServices.Core](../Topic/Microsoft.AnalysisServices.Core.md) ahora es necesario cada vez que se hace referencia al ensamblado Microsoft.AnalysisServices en el código. Los objetos que anteriormente solo se encontraban en el espacio de nombres **Microsoft.AnalysisServices** se mueven al espacio de nombres principal en esta versión si el objeto se usa de la misma forma en los escenarios tabulares y multidimensionales.  Por ejemplo, las API relacionadas con el servidor se reubican en el espacio de nombres principal.  
  
 Aunque ahora hay varios espacios de nombres, ambos existen en el mismo ensamblado (Microsoft.AnalysisServices.dll).  
  
## Cambios en XEvent DISCOVER  
 Para admitir mejor el streaming de XEvent DISCOVER en SSMS para [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], `DISCOVER_XEVENT_TRACE_DEFINITION` se reemplaza por los seguimientos XEvent siguientes:  
  
-   DISCOVER_XEVENT_PACKAGES  
  
-   DISCOVER_XEVENT_OBJECT  
  
-   DISCOVER_XEVENT_OBJECT_COLUMNS  
  
-   DISCOVER_XEVENT_SESSION_TARGETS  
  
## Vea también  
 [Compatibilidad con versiones anteriores de Analysis Services](../analysis-services/analysis-services-backward-compatibility.md)  
  
  