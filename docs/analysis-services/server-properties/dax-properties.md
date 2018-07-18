---
title: Propiedades DAX | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9150eb13b6c39f74f1e65743b6a79aca0a07676a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38033535"
---
# <a name="dax-properties"></a>Propiedades de DAX
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

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

Parámetro |Valor |Descripción
--------|-------|-----------
MaxIntermediateRowsetSize | 1000000 | Número máximo de filas devueltas en una consulta DAX. Agregue esta entrada manualmente al archivo msmdsrv.ini y aumente el valor predeterminado si este es demasiado bajo.
PredicateCheckSpoolCardinalityThreshold| 5000 | Propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de Microsoft.

Para más información sobre otras propiedades de servidor y cómo establecerlas, vea [Configurar las propiedades de servidor en Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).
