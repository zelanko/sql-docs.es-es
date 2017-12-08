---
title: Objeto de base de datos (TMSL) | Documentos de Microsoft
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: ae5c046b-8242-4046-ae76-2c070503fd93
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 239c6e21a7c0e05f52fa00c17d11c5ff81d8a216
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="database-object-tmsl"></a>Objeto de base de datos (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  Define una base de datos Tabular en el nivel de compatibilidad 1200 o superior, en función de un modelo del mismo nivel. Este tema documenta la definición del objeto de una base de datos, proporcionando la carga para las solicitudes que crean, modificar, eliminarán y realizan tareas de administración de base de datos.  
  
> [!NOTE]  
>  En los scripts, puede hacer referencia a una base de datos en el momento. Para cualquier objeto que no sea la propia base de datos, la propiedad de base de datos es opcional si especifica el modelo. Hay una asignación uno a uno entre un modelo y una base de datos que puede usarse para deducir el nombre de la base de datos si explícitamente no se proporciona.   
> De forma similar, puede dejar al margen modelo, establecer sus propiedades en la base de datos.  
  
## <a name="object-definition"></a>Definición del objeto  
 Todos los objetos tienen un conjunto común de propiedades, incluidos el nombre, tipo, descripción, una colección de propiedades y las anotaciones. **Base de datos** objetos también tienen las siguientes propiedades.  
  
 nivel de compatibilidad  
 Actualmente, los valores válidos son 1200, 1400. Niveles de compatibilidad inferiores utilizan un motor de metadatos diferentes.  
  
 readwritemode  
 Enumera el modo de la base de datos. Es habitual que una base de datos de solo lectura en alta disponibilidad o escalabilidad configuraciones. Los valores válidos son de lectura y escritura,  
                readOnly,  
                o readOnlyExclusive. Vea [alta disponibilidad y escalabilidad en Analysis Services](../../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md) y [cambiar una base de datos de Analysis Services entre los modos ReadOnly y ReadWrite](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md) para obtener más información acerca de cuándo se utiliza esta propiedad.  
  
## <a name="usage"></a>Uso  
 **Base de datos** objetos se utilizan en casi todos los comandos. Vea [comandos de Tabular modelo de lenguaje de Scripting &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/tmsl-reference-commands.md) para obtener una lista. A **base de datos** objeto es un elemento secundario de un objeto de servidor.  
  
 Al crear, reemplazar o modificar un objeto de base de datos, especifique todas las propiedades de lectura y escritura de la definición del objeto. Omisión de una propiedad de lectura y escritura se considera una operación de eliminación.  
  
## <a name="partial-syntax"></a>Sintaxis parcial  
 Dado que esta definición de objeto es tan grande, se muestran solo las propiedades directa. El **modelo** objeto proporciona la mayor parte de la definición de la base de datos. Vea [modelo objeto &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/model-object-tmsl.md) a cómo se define el objeto.  
  
```  
    "database": {  
      "type": "object",  
      "properties": {  
        "name": {  
          "type": "string"  
        },  
        "id": {  
          "type": "string"  
        },  
        "description": {  
          "type": "string"  
        },  
        "compatibilityLevel": {  
          "type": "integer"  
        },  
        "readWriteMode": {  
          "enum": [  
            "readWrite",  
            "readOnly",  
            "readOnlyExclusive"  
          ]  
        },  
        "model": {  
          "type": "object",  
          ...  
        }  
    }  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Tabular Model Scripting Language &#40;TMSL&#41; Reference (Referencia de Tabular Model Scripting Language [TMSL])](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Alta disponibilidad y escalabilidad en Analysis Services](../../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md)  
  
  
