---
title: Importar desde Analysis Services (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b9a21b23-3a06-4ef8-bc06-9c79cdc54870
caps.latest.revision: 18
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3809963b531dea89c59f6a23ae77eb1fdd11f6e3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37159166"
---
# <a name="import-from-analysis-services-ssas-tabular"></a>Importar desde Analysis Services (SSAS tabular)
  Este tema explica cómo crear un proyecto de modelos tabulares importando los metadatos de un modelo tabular existente mediante la plantilla de proyecto Importar del servidor de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="create-a-new-model-by-importing-metadata-from-an-existing-model-in-analysis-services"></a>Crear un nuevo modelo importando metadatos de un modelo existente de Analysis Services  
 Puede usar la plantilla de proyecto Importar del servidor para crear un nuevo proyecto de modelos tabulares copiando los metadatos de un modelo tabular existente en un servidor de Analysis Services. El nuevo proyecto se creará con las mismas conexiones de origen de datos, tablas, relaciones, medidas, KPI, roles, jerarquías, perspectivas y particiones que el modelo del que se importó. Sin embargo, los datos no se copian del modelo existente al área de trabajo del nuevo modelo. Una vez que el proceso de importación se haya completado, y se haya creado el nuevo proyecto de modelos, deberá ejecutar una operación Procesar todo para cargar los datos de los orígenes de datos en la base de datos del área de trabajo del nuevo proyecto de modelos.  
  
#### <a name="to-create-a-new-model-by-importing-metadata-from-an-existing-model"></a>Para crear un nuevo modelo importando metadatos de un modelo existente  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], en el menú **Archivo** , haga clic en **Nuevo**y, a continuación, en **Proyecto**.  
  
2.  En el cuadro de diálogo **Nuevo proyecto** , debajo de **Plantillas instaladas**, haga clic en **Business Intelligence**y, a continuación, en **Importar del servidor**.  
  
3.  En **Nombre**, escriba un nombre para el proyecto, después especifique una ubicación y un nombre de solución, y haga clic en **Aceptar**.  
  
4.  En el cuadro de diálogo **Importar desde Analysis Services** , en **Nombre de servidor**, especifique el nombre del servidor de Analysis Services que contiene los metadatos del modelo que desea importar.  
  
5.  En **Nombre de la base de datos**, seleccione la base de datos del modelo tabular que contiene los metadatos del modelo que desea importar y, a continuación, haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Las propiedades del proyecto &#40;Tabular de SSAS&#41;](properties-ssas-tabular.md)  
  
  
