---
title: Comparar soluciones de scripting y objetos personalizados | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: extending-packages-scripting
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- managed tasks [Integration Services]
- Script task [Integration Services], vs. custom managed tasks
- SSIS Script task, vs. custom managed tasks
- custom tasks [Integration Services], scripts
ms.assetid: c0aea822-a21e-44e1-a3d3-8777bd0a1c34
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e3c579607108bd98afc5b214c4069b750cdf4420
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="comparing-scripting-solutions-and-custom-objects"></a>Comparar soluciones de scripting y objetos personalizados
  Una tarea Script o el componente de script de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] puede implementar casi la misma funcionalidad que implementa una tarea administrada personalizada o componente de flujo de datos. A continuación, se proporcionan algunas consideraciones que le servirán de ayuda para elegir el tipo de tarea adecuado a sus necesidades:  
  
-   Si la configuración o la funcionalidad es específica de un paquete individual, debe usar la tarea Script o el componente de script en lugar de desarrollar un objeto personalizado.  
  
-   Si la funcionalidad es genérica, y se podría usar en el futuro para otros paquetes y a través de otros programadores, debería crear un objeto personalizado en lugar de utilizar una solución de scripting. Puede usar un objeto personalizado en cualquier paquete, mientras que un script únicamente se puede utilizar en el paquete para el que se creó.  
  
-   Si el código se reutiliza dentro del mismo paquete, debería considerar la creación un objeto personalizado. Copiar código de una tarea Script o componente de script a otro lleva a la reducción de mantenimiento que dificulta el mantenimiento y la actualización de varias copias del código.  
  
-   Si la implementación cambia con el tiempo, considere el uso de un objeto personalizado. Los objetos personalizados se pueden desarrollar e implementar independientemente del paquete primario, mientras que una actualización de una solución de scripting requiere volver a implementar todo el paquete.  
  
## <a name="see-also"></a>Ver también  
 [Ampliar paquetes con objetos personalizados](../../integration-services/extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
  
  
