---
title: Grupos de medida vinculados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- linked measure groups [Analysis Services]
- referencing measure groups
- Linked Measure Group Wizard
- measure groups [Analysis Services], linked
- linked dimensions [Analysis Services]
ms.assetid: 7f838452-8669-4194-8e15-7afdc7f15251
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a1377552b3e50fe5c536ae0d7d854346ccb062d1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48140355"
---
# <a name="linked-measure-groups"></a>Grupos de medida vinculados
  Un grupo de medida vinculado está basado en otro grupo de medida de un cubo diferente dentro de la misma base de datos o en una base de datos de Analysis Services diferente. Puede usar un grupo de medida vinculada si desea reutilizar un conjunto de medidas, y los valores de datos correspondientes, en varios cubos.  
  
 Microsoft recomienda que los grupos de medida vinculados y originales residan en soluciones que se ejecuten en el mismo servidor. Vincular a un grupo de medida en un servidor remoto está programada para desuso en una versión futura (vea [en desuso características de Analysis Services en SQL Server 2014](../deprecated-analysis-services-features-in-sql-server-2014.md)).  
  
> [!IMPORTANT]  
>  Los grupos de medida vinculados son de solo lectura. Para reflejar los últimos cambios, debe eliminar y volver a crear todos los grupos de medida vinculados basados en el objeto de origen modificado. Por esta razón, copiar y pegar grupos de medida entre distintos proyectos es un método alternativo que debe tener en cuenta en caso de que se necesiten modificaciones futuras al grupo de medida.  
  
## <a name="usage-limitations"></a>Limitaciones de uso  
 Como se ha indicado anteriormente, una restricción importante del uso de medidas vinculadas es la incapacidad de personalizar una medida vinculada directamente. Las modificaciones al tipo de datos, el formato, el enlace de datos y la visibilidad, así como la pertenencia de los elementos del grupo de medida propiamente dicho, son cambios que se deben realizar en el grupo de medida original.  
  
 Desde el punto de vista operativo, los grupos de medida vinculada son idénticos a otros grupos de medida a los que las aplicaciones cliente tienen acceso y se consultan de la misma manera que otros grupos de medida.  
  
 Cuando se realiza una consulta en un cubo que contiene un grupo de medida vinculado, el vínculo se establece y se resuelve durante el primer cálculo del cubo de destino. Debido a este comportamiento, los cálculos que se almacenan en el grupo de medida vinculado no se pueden resolver antes de evaluar la consulta. Dicho de otro modo, las medidas calculadas y las celdas calculadas se deben volver a crear en el cubo de destino en lugar de heredarse del cubo de origen.  
  
 En la lista siguiente se resumen las limitaciones de uso.  
  
-   No se puede crear un grupo de medida vinculado a partir de otro grupo de medida vinculado.  
  
-   No puede agregar o quitar medidas de un grupo de medida vinculada. La pertenencia solo se define en el grupo de medida original.  
  
-   No se admite la reescritura en grupos de medida vinculados.  
  
-   Los grupos de medida vinculada no se pueden usar en diversas relaciones varios a varios, especialmente cuando estas relaciones están en distintos cubos. Si lo hace, puede producir agregaciones ambiguas. Para más información, vea [Incorrect Amounts for Linked Measures in Cubes containing Many-to-Many Relationships](http://social.technet.microsoft.com/wiki/contents/articles/22911.incorrect-amounts-for-linked-measures-in-cubes-containing-many-to-many-relationships-ssas-troubleshooting.aspx)(Cantidades incorrectas para medidas vinculadas en cubos que contienen relaciones varios a varios).  
  
 Las medidas contenidas en un grupo de medida vinculado solamente se pueden organizar directamente en dimensiones vinculadas recuperadas de la misma base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . No obstante, puede usar miembros calculados para relacionar la información de grupos de medida vinculados con las otras dimensiones no vinculadas del cubo. También puede usar una relación indirecta, como una referencia o una relación de varios a varios, para relacionar dimensiones no vinculadas con un grupo de medida vinculado.  
  
## <a name="create-or-modify-a-linked-measure"></a>Crear o modificar una medida vinculada  
 Use [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] para crear un grupo de medida vinculada.  
  
1.  Concluya ahora las modificaciones al grupo de medida original, en el cubo de origen, de modo que no tenga que volver a crear los grupos de medida vinculada más adelante en cubos posteriores. Puede cambiar el nombre de un objeto vinculado, pero no puede cambiar otras propiedades.  
  
2.  En el Explorador de soluciones, haga doble clic en el cubo al que desea agregar al grupo de medida vinculada. Este paso abre el cubo en el Diseñador de cubos.  
  
3.  En el Diseñador de cubos, en el panel Medidas o en el panel Dimensiones, haga clic con el botón derecho y seleccione **Nuevo objeto vinculado**. Esto inicia el Asistente para objetos vinculados.  
  
4.  En la primera página, especifique el origen de datos. Este paso establece la ubicación del grupo de medida original. El valor predeterminado es el cubo actual de la base de datos actual, pero también puede elegir otra base de datos de Analysis Services.  
  
5.  En la página siguiente, elija el grupo de medida o la dimensión que desea vincular. Los objetos de dimensiones y de cubo, como los grupos de medida, se muestran por separado. Solo están disponibles esos objetos que no están ya presentes en el cubo actual.  
  
6.  Haga clic en **Finalizar** para crear el objeto vinculado. Los objetos vinculados aparecen en los paneles Medidas y Dimensiones con el icono del vínculo.  
  
## <a name="secure-a-linked-measure"></a>Proteger una medida vinculada  
 Una vez definido este vínculo, el acceso a las medidas de un grupo de medida vinculado se administra de la misma manera que el acceso a otros grupos de medida. Un objeto vinculado aparece junto con sus homólogos no vinculados en el Diseñador de roles. Para más información sobre cómo administrar la seguridad de un grupo de medida, vea [Otorgar permisos para cubos o modelos &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md).  
  
 Para definir o usar un grupo de medida vinculado, el Windows cuenta de servicio de la [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia debe pertenecer a un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] rol de base de datos que tiene `ReadDefinition` y `Read` derechos en el origen de acceso [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia a la cubo y grupo de medida de origen, o debe pertenecer a la [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] función Administradores para el origen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia.  
  
## <a name="see-also"></a>Vea también  
 [Definir dimensiones vinculadas](define-linked-dimensions.md)  
  
  
