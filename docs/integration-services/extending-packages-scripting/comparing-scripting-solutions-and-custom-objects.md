---
description: Comparar soluciones de scripting y objetos personalizados
title: Comparar soluciones de scripting y objetos personalizados | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- managed tasks [Integration Services]
- Script task [Integration Services], vs. custom managed tasks
- SSIS Script task, vs. custom managed tasks
- custom tasks [Integration Services], scripts
ms.assetid: c0aea822-a21e-44e1-a3d3-8777bd0a1c34
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d0e862da85c7c3c2e2255bbd522045b507b5d471
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88430317"
---
# <a name="comparing-scripting-solutions-and-custom-objects"></a>Comparar soluciones de scripting y objetos personalizados

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Una tarea Script o el componente de script de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] puede implementar casi la misma funcionalidad que implementa una tarea administrada personalizada o componente de flujo de datos. A continuación, se proporcionan algunas consideraciones que le servirán de ayuda para elegir el tipo de tarea adecuado a sus necesidades:  
  
-   Si la configuración o la funcionalidad es específica de un paquete individual, debe usar la tarea Script o el componente de script en lugar de desarrollar un objeto personalizado.  
  
-   Si la funcionalidad es genérica, y se podría usar en el futuro para otros paquetes y a través de otros programadores, debería crear un objeto personalizado en lugar de utilizar una solución de scripting. Puede usar un objeto personalizado en cualquier paquete, mientras que un script únicamente se puede utilizar en el paquete para el que se creó.  
  
-   Si el código se reutiliza dentro del mismo paquete, debería considerar la creación un objeto personalizado. Copiar código de una tarea Script o componente de script a otro lleva a la reducción de mantenimiento que dificulta el mantenimiento y la actualización de varias copias del código.  
  
-   Si la implementación cambia con el tiempo, considere el uso de un objeto personalizado. Los objetos personalizados se pueden desarrollar e implementar independientemente del paquete primario, mientras que una actualización de una solución de scripting requiere volver a implementar todo el paquete.  
  
## <a name="see-also"></a>Consulte también  
 [Ampliar paquetes con objetos personalizados](../../integration-services/extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
  
  
