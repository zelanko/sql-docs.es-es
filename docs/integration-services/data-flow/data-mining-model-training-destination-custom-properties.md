---
title: Propiedades personalizadas del destino de entrenamiento del modelo de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f0a70216-fdac-44ae-af29-35f65626217c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e603b7e7342ee349b885392c43e42f33009700ae
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "71293125"
---
# <a name="data-mining-model-training-destination-custom-properties"></a>Propiedades personalizadas del destino de entrenamiento del modelo de minería de datos

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  El destino de entrenamiento del modelo de minería de datos tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del destino de aprendizaje del modelo de minería de datos. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|ASConnectionId|String|Identificador único del administrador de conexiones.|  
|ASConnectionString|String|Cadena de conexión a una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o a un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|ObjectRef|String|Etiqueta XML que identifica la estructura de minería de datos que la transformación usa:|  
  
 La entrada y las columnas de entrada del destino de entrenamiento del modelo de minería de datos no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [Data Mining Model Training Destination](../../integration-services/data-flow/data-mining-model-training-destination.md).  
  
## <a name="see-also"></a>Consulte también  
 [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
