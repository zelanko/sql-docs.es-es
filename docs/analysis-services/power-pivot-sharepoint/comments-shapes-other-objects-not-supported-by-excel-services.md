---
title: Los comentarios, formas, otros objetos no admitidos por Excel Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: df13c3fa92d5439e559e286424438569b3ead86b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68164391"
---
# <a name="comments-shapes-other-objects-not-supported-by-excel-services"></a>Comentarios, formas, otros objetos no admitidos por Excel Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Este error se produce al agregar segmentaciones a un libro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] desde una lista de campos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Se aplica a|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint|  
|Versión del producto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Excel Web Access no puede representar el objeto Forma que se usa para controlar la posición y el formato de las segmentaciones agregadas a un libro de la lista de campos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|  
|Texto del mensaje|Servicios de Excel no admite las siguientes características y puede que no se muestren o se muestren solo parcialmente:<br /><br /> Comentarios, formas o otros objetos<br /><br /> Algunas características, como las consultas de datos externos, muestran datos en caché que solo pueden actualizarse en Microsoft Excel.|  
  
## <a name="explanation"></a>Explicación  
 Excel Web Access muestra este error si abre un libro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en un explorador y hace clic en el botón **Detalles** para el mensaje **Características no admitidas. El libro probablemente no se muestre como está previsto**.  
  
 Este error se produce porque el libro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] contiene segmentaciones cuyo diseño lo controla un objeto Forma oculto en Excel. El objeto Forma controla el formato y la posición de las segmentaciones en la posición horizontal y vertical.  
  
 Servicios de Excel no puede representar un objeto Forma, pero dado que el objeto está oculto, este hecho no constituye un problema.  
  
## <a name="user-action"></a>Acción del usuario  
 Se puede omitir este error. Haga clic en **Aceptar** para cerrar el mensaje de error y continuar utilizar el libro y las segmentaciones sin problema.  
  
  
