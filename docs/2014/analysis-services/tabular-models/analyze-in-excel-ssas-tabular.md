---
title: Analizar en Excel (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2f17b4df-eea2-48c7-a1f2-a3fb7748c15f
author: minewiskan
ms.author: owend
ms.openlocfilehash: 429245f875ce6d13ef3818cf7bae874f72c500ed
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939946"
---
# <a name="analyze-in-excel-ssas-tabular"></a>Analizar en Excel (SSAS tabular)
  La característica Analizar en Excel, de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], proporciona a los autores de modelos tabulares una manera de analizar rápidamente proyectos de modelos durante el desarrollo. Esta característica abre Microsoft Excel, crea una conexión de origen de datos con la base de datos del área de trabajo del modelo y agrega automáticamente una tabla dinámica a la hoja de cálculo. Los objetos de la base de datos del área de trabajo (tablas, columnas y medidas) aparecen como campos en la lista de campos de la tabla dinámica. De esta forma, los objetos y los datos se podrán ver en el contexto del usuario o del rol vigente y de la perspectiva.  
  
 En este tema se supone que ya sabe cómo usar Microsoft Excel, las tablas dinámicas y los gráficos dinámicos. Para obtener más información acerca del uso de Excel, vea la Ayuda de Excel.  
  
 Secciones de este tema:  
  
-   [Ventajas](#bkmk_benefits)  
  
-   [Tareas relacionadas](#bkmk_rt)  
  
##  <a name="benefits"></a><a name="bkmk_benefits"></a> Ventajas  
 La característica Analizar en Excel proporciona a los autores de modelos la capacidad de probar la eficacia de un proyecto de modelos mediante el uso de la aplicación de análisis de datos comunes Microsoft Excel. Para usar la característica Analizar en Excel, tiene que tener instalado Microsoft Office 2003 o posterior en el mismo equipo que [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
> [!NOTE]  
>  Si Office no está instalado en el mismo equipo que [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], puede usar Excel en otro equipo para conectarse a la base de datos del área de trabajo como un origen de datos. A continuación, podrá agregar manualmente una tabla dinámica a la hoja de cálculo.  
  
 La característica Analizar en Excel abre Excel y crea un libro de Excel (.xls). Se creará una conexión de datos desde el libro a la base de datos del área de trabajo del modelo. Asimismo, se agregará una tabla dinámica en blanco a la hoja de cálculo y se rellenarán los metadatos del objeto del modelo en la lista de campos de la tabla dinámica. A continuación, podrá agregar datos visibles y segmentaciones de datos a la tabla dinámica.  
  
 De forma predeterminada, cuando se usa la característica Analizar en Excel, el usuario vigente es la cuenta de usuario que ha iniciado sesión actualmente. Normalmente, esta cuenta es un administrador sin restricciones de vista para los objetos del modelo o los datos. No obstante, puede especificar otro nombre de usuario o rol vigente diferente. Esto permite examinar un proyecto de modelos en Excel en el contexto de un usuario o un rol específico. La especificación del usuario vigente incluye las opciones siguientes:  
  
 **Usuario de Windows actual**  
 Usa la cuenta de usuario con la que ha iniciado sesión actualmente.  
  
 **Otro usuario de Windows**  
 Usa un nombre de usuario de Windows específico en lugar del usuario que ha iniciado sesión actualmente. El uso de otro usuario de Windows no requiere una contraseña. Los objetos y los datos solo se pueden ver en Excel dentro del contexto del nombre de usuario vigente. En Excel no se puede realizar ninguna modificación en los objetos ni en los datos del modelo.  
  
 **Role**  
 Los roles se usan para definir permisos de usuario en los metadatos y datos de objeto. Generalmente, los roles se definen para un usuario o un grupo de usuarios de Windows determinado. Algunos roles pueden incluir filtros adicionales en el nivel de fila definidos en una fórmula de DAX. Cuando se usa la característica Analizar en Excel, se puede seleccionar de forma opcional el rol que se va a usar. Los metadatos del objeto y las vistas de datos estarán limitados por los permisos y los filtros definidos para el rol. Para obtener más información, vea [Crear y administrar roles &#40;SSAS tabular&#41;](roles-ssas-tabular.md).  
  
 Además del usuario o el rol vigente, se puede especificar una perspectiva. Las perspectivas permiten a los autores de modelos definir vistas específicas de escenario empresarial de los objetos del modelo y los datos. De forma predeterminada, no se usa ninguna perspectiva. Para usar una perspectiva con la característica Analizar en Excel, es necesario que se hayan definido antes las perspectivas mediante el cuadro de diálogo Perspectivas de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Si se especifica una perspectiva, la lista de campos de la tabla dinámica solo incluirá los objetos seleccionados en dicha perspectiva. Para obtener más información, vea [crear y administrar perspectivas &#40;&#41;tabular de SSAS ](perspectives-ssas-tabular.md).  
  
##  <a name="related-tasks"></a><a name="bkmk_rt"></a> Tareas relacionadas  
  
|**Tema**|**Descripción**|  
|---------------|---------------------|  
|[Analizar un modelo tabular en Excel &#40;SSAS tabular&#41;](analyze-a-tabular-model-in-excel-ssas-tabular.md)|En este tema se describe cómo usar la característica Analizar en Excel del diseñador de modelos para abrir Excel, crear una conexión de origen de datos con la base de datos del área de trabajo del modelo y agregar una tabla dinámica a la hoja de cálculo.|  
  
## <a name="see-also"></a>Consulte también  
 [Analizar un modelo tabular en Excel &#40;SSAS tabular&#41;](analyze-a-tabular-model-in-excel-ssas-tabular.md)   
 [Roles &#40;SSAS tabular&#41;](roles-ssas-tabular.md)   
 [Perspectivas &#40;SSAS tabular&#41;](perspectives-ssas-tabular.md)  
  
  
