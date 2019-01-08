---
title: Propiedades DAX de Analysis Services | Microsoft Docs
ms.date: 10/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 20a6df833f8c525c24abdf3bb51278d0067db951
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2018
ms.locfileid: "53071902"
---
# <a name="dax-properties"></a>Propiedades de DAX
[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

   La sección DAX de msmdsrv.ini contiene la configuración que se usa para controlar ciertos comportamientos de consulta en Analysis Services, como el límite superior en el número de filas devuelto en un conjunto de resultados de consulta DAX.

  Cuando los conjuntos de filas son muy grandes, como los devueltos en los modelos DirectQuery, el valor predeterminado de un millón de filas podría no ser suficiente. Sabrá si el límite debe ajustar si se produce este error: "El conjunto de resultados de una consulta al origen de datos externos superó el tamaño máximo permitido de '1000000' filas".

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
