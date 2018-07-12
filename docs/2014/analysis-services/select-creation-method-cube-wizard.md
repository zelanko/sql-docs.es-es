---
title: Seleccionar método de creación (Asistente para cubos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubewizard.cubedefinition.f1
ms.assetid: 985d3b5b-7891-465b-862d-f7e75431b342
caps.latest.revision: 28
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e3a623381738e4d2f96222aaa193cf09ec619889
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37259431"
---
# <a name="select-creation-method-cube-wizard"></a>Seleccionar método de creación (Asistente para cubos)
  Use la página **Seleccionar método de creación** para especificar cómo se crea el cubo.  
  
## <a name="options"></a>Opciones  
 **Usar tablas existentes**  
 Seleccione esta opción para crear un cubo utilizando tablas existentes en el origen de datos. El asistente le guiará a través del proceso de selección y definición de grupos y dimensiones de medida basados en tablas existentes para generar el nuevo cubo.  
  
 **Crear un cubo vacío**  
 Seleccione esta opción para crear un cubo vacío. Esta opción resulta útil cuando desee crear todo de forma manual o cuando todos los grupos de medida en el cubo son grupos de medida vinculados.  
  
> [!NOTE]  
>  Esta opción solo está disponible cuando trabaja con un proyecto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y no está disponible cuando está conectado directamente a una base de datos [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 **Generar tablas en el origen de datos**  
 Seleccione esta opción para crear en primer lugar un cubo primero y, a continuación, generar nuevas tablas en el origen de datos basado** en la definición de cubo.  
  
> [!NOTE]  
>  Para usar esta opción, debe tener permiso para crear objetos en el origen de datos subyacente.  
  
 Si selecciona esta opción, se habilitará la opción **Plantilla** .  
  
 **Plantilla**  
 Seleccione la plantilla que desea usar para crear el cubo. Las plantillas proporcionan un conjunto de definiciones orientadas para un motivo** profesional específico.  
  
> [!NOTE]  
>  Esta opción solo está disponible cuando se ha activado la opción **Generar tablas en el origen de datos** .  
  
## <a name="see-also"></a>Vea también  
 [Objetos de cubo &#40;Analysis Services - datos multidimensionales&#41;](multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)   
 [Cubos en modelos multidimensionales](multidimensional-models/cubes-in-multidimensional-models.md)   
 [Dimensiones en modelos multidimensionales](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
