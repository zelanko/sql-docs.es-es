---
title: Definir relaciones de atributo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Analysis Services], relationships
- relationships [Analysis Services], attributes
ms.assetid: 9184d344-e96d-4025-ad6f-3f75129746df
author: minewiskan
ms.author: owend
ms.openlocfilehash: d75bf3ec0aa6e7199b1e6f8d31e2602deb8efeff
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544677"
---
# <a name="define-attribute-relationships"></a>Definir relaciones de atributo
  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , los atributos son el bloque de creación fundamental de una dimensión. Una dimensión contiene un conjunto de atributos que se organizan en función de las relaciones de atributo.  
  
 Para cada tabla incluida en una dimensión, hay una relación de atributo que relaciona el atributo clave de la tabla con otros atributos en esa tabla. Esta relación la crea al crear la dimensión.  
  
 Una relación de atributo proporciona las siguientes ventajas:  
  
-   Reduce la cantidad de memoria necesaria para procesar la dimensión. Esto acelera el procesamiento de dimensiones, particiones y consultas.  
  
-   Aumenta el rendimiento de las consultas porque el acceso al almacenamiento es más rápido y se optimizan mejor los planes de ejecución.  
  
-   Hace que los algoritmos de diseños de agregaciones seleccionen agregados más efectivos, siempre y cuando las jerarquías definidas por el usuario se hayan establecido a lo largo de las rutas de acceso de la relación.  
  
    > [!NOTE]  
    >  Para obtener más información acerca de la importancia e implicaciones de definir y configurar las relaciones de atributo, vea la sección "mejorar el rendimiento de las consultas" en la [Guía de rendimiento de SQL Server 2005 Analysis Services](https://docsbay.net/Microsoft-SQL-Server-2005-Analysis-Services-Performance-Guide).  
  
## <a name="attribute-relationship-considerations"></a>Consideraciones sobre las relaciones de atributo  
 Si los datos subyacentes lo permiten, también debería definir relaciones de atributo únicas entre atributos. Para definir relaciones de atributo únicas, utilice la pestaña **Relación de los atributos** del Diseñador de dimensiones.  
  
 Cualquier atributo que tenga una relación de salida debe tener una clave única relativa a su atributo relacionado. En otras palabras, un miembro de un atributo de origen solo debe identificar un único miembro de un atributo relacionado. Por ejemplo, considere la relación, Ciudad -> Estado. En esta relación, el atributo de origen es Ciudad y el atributo relacionado es Estado. El atributo de origen es el lado "varios" y el lado relacionado es el lado "uno" de la relación de varios a uno. La clave para el atributo de origen sería Ciudad + Estado. Para obtener más información, vea [Crear, modificar o eliminar una relación de atributo](attribute-relationships-create-modify-or-delete-relationship.md).  
  
 Para obtener más información sobre las propiedades de una relación de atributo, vea [Configurar propiedades de relación de los atributos](attribute-relationships-configure-attribute-properties.md).  
  
> [!NOTE]  
>  Si las relaciones de atributo no se definen correctamente, puede que los resultados de las consultas no sean válidos.  
  
## <a name="see-also"></a>Consulte también  
 [Relaciones de atributo](../multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)  
  
  
