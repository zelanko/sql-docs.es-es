---
title: Reimplementación de paquetes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- redeploying packages [Integration Services]
- deploying packages [Integration Services], redeploying
ms.assetid: 86806efb-8cf4-4f9d-9824-1152cb4c495c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4c5286d406d96f62fc74eb619f7e7a6064fde2a3
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85423052"
---
# <a name="redeployment-of-packages"></a>Volver a implementar paquetes
  Después de implementar un proyecto, es posible que necesite actualizar o ampliar las funciones del paquete y después, volver a implementar el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene los paquetes actualizados. Como parte del proceso de volver a implementar paquetes, debe revisar las propiedades de configuración incluidas en la utilidad de implementación. Por ejemplo, es posible que no desee permitir cambios en la configuración después de volver a implementar el paquete.  
  
## <a name="process-for-redeployment"></a>Proceso para volver a implementar  
 Cuando termine de actualizar los paquetes, vuelva a generar el proyecto, copiar la carpeta de implementación al equipo de destino y ejecutar el Asistente para la instalación de paquetes.  
  
 Si solo actualiza unos cuantos paquetes del proyecto, es posible que no desee volver a implementar todo el proyecto. Para implementar solamente algunos paquetes, puede crear un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , agregarle los paquetes actualizados y después, generar e implementar el proyecto. Las configuraciones de paquetes se copian automáticamente junto con el paquete al agregarlo a otro proyecto.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Implementar los paquetes mediante la utilidad de implementación](../../2014/integration-services/deploy-packages-by-using-the-deployment-utility.md)  
  
  
