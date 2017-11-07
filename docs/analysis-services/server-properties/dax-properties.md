---
title: Propiedades DAX | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: aa928dc5-d00d-4f8a-80b9-7e6973d2196c
caps.latest.revision: 6
author: HeidiSteen
ms.author: heidist
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 225c4aea79b880fd85f118d89bae1339e370aa40
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="dax-properties"></a>Propiedades de DAX
   La sección DAX de msmdsrv.ini contiene la configuración usada para controlar ciertos comportamientos de consulta en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], como el límite superior en el número de filas que se devuelve en un conjunto de resultados de consulta DAX. 
  
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

Configuración |Value |Description
--------|-------|-----------
MaxIntermediateRowsetSize | 1000000 | Número máximo de filas devueltas en una consulta DAX. Agregue esta entrada manualmente al archivo msmdsrv.ini y aumente el valor predeterminado si este es demasiado bajo. 
PredicateCheckSpoolCardinalityThreshold| 5000 | Propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de Microsoft.

Para más información sobre otras propiedades de servidor y cómo establecerlas, vea [Configurar las propiedades de servidor en Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md). 

