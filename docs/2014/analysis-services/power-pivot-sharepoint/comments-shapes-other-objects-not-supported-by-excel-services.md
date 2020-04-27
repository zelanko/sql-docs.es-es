---
title: 'Los servicios de Excel no admiten las siguientes características y es posible que no se muestren o se muestren solo parcialmente: comentarios, formas u otros objetos | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: ade92e15-dfbf-496b-9378-a00bd83ba750
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 03411134eb1350adcd37badd458e7f7a0198a9ec
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66071917"
---
# <a name="the-following-features-are-not-supported-by-excel-services-and-may-not-display-or-may-display-only-partially-comments-shapes-or-other-objects"></a>Las siguientes características no se admiten en Servicios de Excel y puede que no se muestren o que se muestren solo parcialmente: comentarios, formas u otros objetos
  Este error se produce al agregar segmentaciones a un libro PowerPivot desde una lista de campos de PowerPivot.  
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Aplicable a|PowerPivot para SharePoint|  
|Versión del producto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Excel Web Access no puede representar el objeto Forma que se usa para controlar la posición y el formato de las segmentaciones agregadas a un libro de la lista de campos de PowerPivot.|  
|Texto del mensaje|Servicios de Excel no admite las siguientes características y puede que no se muestren o se muestren solo parcialmente:<br /><br /> Comentarios, formas o otros objetos<br /><br /> Algunas características, como las consultas de datos externos, muestran datos en caché que solo pueden actualizarse en Microsoft Excel.|  
  
## <a name="explanation"></a>Explicación  
 Excel Web Access muestra este error al abrir un libro PowerPivot en un explorador y hacer clic en el botón **detalles** del mensaje, **es posible que no se muestren las características no admitidas de este libro como se pretende**.  
  
 Este error se produce porque el libro PowerPivot contiene segmentaciones cuyo diseño es controlado por un objeto Forma oculto en Excel. El objeto Forma controla el formato y la posición de las segmentaciones en la posición horizontal y vertical.  
  
 Servicios de Excel no puede representar un objeto Forma, pero dado que el objeto está oculto, este hecho no constituye un problema.  
  
## <a name="user-action"></a>Acción del usuario  
 Se puede omitir este error. Haga clic en **Aceptar** para cerrar el mensaje de error y continuar utilizar el libro y las segmentaciones sin problema.  
  
  
