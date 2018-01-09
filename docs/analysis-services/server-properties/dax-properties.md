---
title: Propiedades DAX | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: aa928dc5-d00d-4f8a-80b9-7e6973d2196c
caps.latest.revision: "6"
author: HeidiSteen
ms.author: heidist
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 76ffc0da4e8d56b4bb37b0be5278e458ac6fb043
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="dax-properties"></a>Propiedades de DAX
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]La sección DAX de msmdsrv.ini contiene valores utilizados para controlar ciertos comportamientos de consulta en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], como el límite superior en el número de filas devuelto en un conjunto de resultados de consulta DAX. 
  
  Cuando los conjuntos de filas son muy grandes, como los devueltos en los modelos DirectQuery, el valor predeterminado de un millón de filas podría no ser suficiente. Sabrá si el límite tiene que ajustarse si recibe este error: "El conjunto de resultados de una consulta de origen de datos externo superó el tamaño máximo permitido de '1000000' filas".
 
Para aumentar el límite superior, especifique la configuración **MaxIntermediateRowSize** . Deberá agregar manualmente el elemento completo a la sección DAX del archivo de configuración. La configuración no estará presente en el archivo hasta que lo agregue.
  
## <a name="configuration-snippet"></a>Fragmento de código de la configuración

```
<ConfigurationSettings>
. . .
<DAX>   
  <PredicateCheckSpoolCardinalityThreshold>5000
  </PredicateCheckSpoolCardinalityThreshold>
  <DQ>
     <MaxIntermediateRowsetSize>1000000
     </MaxIntermediateRowsetSize>
  </DQ>
</DAX>
. . . 
```

## <a name="property-descriptions"></a>Descripciones de las propiedades

Configuración |Valor |Description
--------|-------|-----------
MaxIntermediateRowsetSize | 1000000 | Número máximo de filas devueltas en una consulta DAX. Agregue esta entrada manualmente al archivo msmdsrv.ini y aumente el valor predeterminado si este es demasiado bajo. 
PredicateCheckSpoolCardinalityThreshold| 5000 | Propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de Microsoft.

Para más información sobre otras propiedades de servidor y cómo establecerlas, vea [Configurar las propiedades de servidor en Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md). 
