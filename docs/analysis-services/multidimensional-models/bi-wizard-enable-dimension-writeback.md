---
title: Habilitar reescritura en la dimensión | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 561dc878302afe7636a2660a9e194ac14a35c7f1
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="bi-wizard---enable-dimension-writeback"></a>Asistente de BI - Habilitar reescritura en la dimensión
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Agregar la mejora de reescritura de dimensiones a un cubo o dimensión para permitir que los usuarios modifiquen manualmente la estructura y los miembros de la dimensión. Las actualizaciones de una dimensión habilitada para escritura se registran directamente en la tabla de dimensiones. Esta mejora cambia la configuración de la propiedad **WriteEnabled** para una dimensión.  
  
 Para agregar la reescritura de dimensiones, se usa el Asistente de Business Intelligence y se selecciona la opción **Habilitar reescritura en la dimensión** en la página **Elegir mejora** . Este asistente le guía por los pasos para seleccionar la dimensión a la que desee aplicar la reescritura de dimensiones y establecer esta opción para la dimensión seleccionada.  
  
> [!NOTE]  
>  La reescritura solo es compatible para bases de datos relacionales de SQL Server y data marts.  
  
## <a name="selecting-a-dimension"></a>Seleccionar una dimensión  
 En la primera página **Habilitar reescritura en la dimensión** del asistente, se especifica la dimensión a la que se desea aplicar la reescritura. La mejora de reescritura de dimensiones agregada a esta dimensión seleccionada produce cambios en la dimensión. Estos cambios son heredados por todos los cubos que incluyan la dimensión seleccionada.  
  
## <a name="setting-dimension-writeback-capability"></a>Establecer la capacidad de reescritura de dimensiones  
 En la segunda página **Habilitar reescritura en la dimensión** del asistente se establece la opción **Habilitar reescritura en la dimensión** . Al seleccionar esta opción se establece automáticamente la propiedad **WriteEnabled** de la dimensión como **True**. Al eliminar la selección de esta opción, se establece automáticamente la propiedad como **False**.  
  
## <a name="remarks"></a>Comentarios  
 Al crear un nuevo miembro, debe incluir todos los atributos en una dimensión. No puede insertar un miembro sin especificar un valor para el atributo clave de la dimensión. Por lo tanto, la creación de miembros está sujeta a las restricciones (como los valores de clave no nulos) definidas en la tabla de la dimensión. También debe tener en cuenta las columnas especificadas opcionalmente por las propiedades de la dimensión, como las columnas especificadas en las propiedades de la dimensión **CustomRollupColumn**, **CustomRollupPropertiesColumn** o **UnaryOperatorColumn** .  
  
> [!WARNING]  
>  Si usa SQL Azure como origen de datos para realizar la reescritura en una base de datos de Analysis Services, se produce un error en la operación. Esto es así por cuestiones de diseño, porque la opción del proveedor que permite que haya varios conjuntos de resultados (MARS) activos no está activada de forma predeterminada.  
>   
>  La solución es agregar el valor siguiente en la cadena de conexión, para admitir MARS y habilitar la reescritura:  
>   
>  `"MultipleActiveResultSets=True"`  
>   
>  Para más información, vea [Utilizar conjuntos de resultados activos múltiples &#40;MARS&#41;](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md).  
  
## <a name="see-also"></a>Vea también  
 [Dimensiones habilitadas para escritura](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
