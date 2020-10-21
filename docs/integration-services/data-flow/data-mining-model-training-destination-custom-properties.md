---
description: Propiedades personalizadas del destino de entrenamiento del modelo de minería de datos
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
ms.openlocfilehash: 8ed5f1b09cbbaa4d20c891a03d9846949eedc8bc
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196451"
---
# <a name="data-mining-model-training-destination-custom-properties"></a>Propiedades personalizadas del destino de entrenamiento del modelo de minería de datos

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  El destino de entrenamiento del modelo de minería de datos tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del destino de aprendizaje del modelo de minería de datos. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|ASConnectionId|String|Identificador único del administrador de conexiones.|  
|ASConnectionString|String|Cadena de conexión a una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o a un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|ObjectRef|String|Etiqueta XML que identifica la estructura de minería de datos que la transformación usa:|  
  
 La entrada y las columnas de entrada del destino de entrenamiento del modelo de minería de datos no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [Data Mining Model Training Destination](../../integration-services/data-flow/data-mining-model-training-destination.md).  
  
## <a name="see-also"></a>Vea también  
 [Common Properties](./set-the-properties-of-a-data-flow-component.md)  
  
