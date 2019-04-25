---
title: Volver a implementar paquetes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- redeploying packages [Integration Services]
- deploying packages [Integration Services], redeploying
ms.assetid: 86806efb-8cf4-4f9d-9824-1152cb4c495c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 15d41b9c0e31fe4bfd86349888071721b7493661
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62766847"
---
# <a name="redeployment-of-packages"></a>Volver a implementar paquetes
  Después de implementar un proyecto, es posible que necesite actualizar o ampliar las funciones del paquete y después, volver a implementar el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene los paquetes actualizados. Como parte del proceso de volver a implementar paquetes, debe revisar las propiedades de configuración incluidas en la utilidad de implementación. Por ejemplo, es posible que no desee permitir cambios en la configuración después de volver a implementar el paquete.  
  
## <a name="process-for-redeployment"></a>Proceso para volver a implementar  
 Cuando termine de actualizar los paquetes, vuelva a generar el proyecto, copiar la carpeta de implementación al equipo de destino y ejecutar el Asistente para la instalación de paquetes.  
  
 Si solo actualiza unos cuantos paquetes del proyecto, es posible que no desee volver a implementar todo el proyecto. Para implementar solamente algunos paquetes, puede crear un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , agregarle los paquetes actualizados y después, generar e implementar el proyecto. Las configuraciones de paquetes se copian automáticamente junto con el paquete al agregarlo a otro proyecto.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Implementar los paquetes mediante la utilidad de implementación](../../2014/integration-services/deploy-packages-by-using-the-deployment-utility.md)  
  
  
