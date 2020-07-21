---
title: FeatureSet (DTA, elemento)
description: En la utilidad DTA, el elemento FeatureSet contiene las estructuras de diseño físico que el Asistente para la optimización de motor de base de datos usa durante los análisis.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- FeatureSet element
ms.assetid: f2070c53-4a5c-4c11-ac38-96ee200c84f0
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 1b14578483eca7160cc810ff6bb7e2f04c0638c0
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826509"
---
# <a name="featureset-element-dta"></a>FeatureSet (DTA, elemento)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Contiene las estructuras de diseño físico (índices o vistas indizadas) que desea que utilice el Asistente para la optimización de motor de base de datos durante el análisis.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <FeatureSet>...</FeatureSet>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|**string**, sin longitud máxima.|  
|**Valores permitidos**|**IDX_IV**<br /> Índices y vistas indizadas.<br /><br /> **IDX**<br /> Solo índices.<br /><br /> **IV**<br /> Solo vistas indizadas.<br /><br /> **NCL_IDX**<br /> Solo índices no clúster.<br /><br /> Utilice uno de estos valores con este elemento.|  
|**Valor predeterminado**|**IDX**|  
|**Repetición**|Una obligatoria para cada elemento **TuningOptions** , a menos que se utilice el elemento **DropOnlyMode** . Si se utiliza **DropOnlyMode** , no es posible utilizar **FeatureSet**. Estos elementos son mutuamente exclusivos.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[TuningOptions &#40;DTA, elemento&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Elementos secundarios**|Ninguno.|  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso de este elemento, vea [Ejemplo de archivo de entrada XML simple &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Consulte también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
