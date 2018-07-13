---
title: Comparar soluciones de scripting y objetos personalizados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- managed tasks [Integration Services]
- Script task [Integration Services], vs. custom managed tasks
- SSIS Script task, vs. custom managed tasks
- custom tasks [Integration Services], scripts
ms.assetid: c0aea822-a21e-44e1-a3d3-8777bd0a1c34
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2e104afbc404b6889b75066490e536863d8d9408
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37152396"
---
# <a name="comparing-scripting-solutions-and-custom-objects"></a>Comparar soluciones de scripting y objetos personalizados
  Una tarea Script o el componente de script de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] puede implementar casi la misma funcionalidad que implementa una tarea administrada personalizada o componente de flujo de datos. A continuación, se proporcionan algunas consideraciones que le servirán de ayuda para elegir el tipo de tarea adecuado a sus necesidades:  
  
-   Si la configuración o la funcionalidad es específica de un paquete individual, debe usar la tarea Script o el componente de script en lugar de desarrollar un objeto personalizado.  
  
-   Si la funcionalidad es genérica, y se podría usar en el futuro para otros paquetes y a través de otros programadores, debería crear un objeto personalizado en lugar de utilizar una solución de scripting. Puede usar un objeto personalizado en cualquier paquete, mientras que un script únicamente se puede utilizar en el paquete para el que se creó.  
  
-   Si el código se reutiliza dentro del mismo paquete, debería considerar la creación un objeto personalizado. Copiar código de una tarea Script o componente de script a otro lleva a la reducción de mantenimiento que dificulta el mantenimiento y la actualización de varias copias del código.  
  
-   Si la implementación cambia con el tiempo, considere el uso de un objeto personalizado. Los objetos personalizados se pueden desarrollar e implementar independientemente del paquete primario, mientras que una actualización de una solución de scripting requiere volver a implementar todo el paquete.  
  
![Icono de Integration Services (pequeño)](../media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services** <br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Vea también  
 [Ampliar paquetes con objetos personalizados](../extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
  
  
