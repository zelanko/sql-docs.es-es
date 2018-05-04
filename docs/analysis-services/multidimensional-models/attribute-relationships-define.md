---
title: Definir relaciones de atributo | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4d9032a828b50e9077886bed38707d299176689e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="attribute-relationships---define"></a>Atributo relaciones - definir
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], los atributos son la unidad de creación fundamental de una dimensión. Una dimensión contiene un conjunto de atributos que se organizan en función de las relaciones de atributo.  
  
 Para cada tabla incluida en una dimensión, hay una relación de atributo que relaciona el atributo clave de la tabla con otros atributos en esa tabla. Esta relación la crea al crear la dimensión.  
  
 Una relación de atributo proporciona las siguientes ventajas:  
  
-   Reduce la cantidad de memoria necesaria para procesar la dimensión. Esto acelera el procesamiento de dimensiones, particiones y consultas.  
  
-   Aumenta el rendimiento de las consultas porque el acceso al almacenamiento es más rápido y se optimizan mejor los planes de ejecución.  
  
-   Hace que los algoritmos de diseños de agregaciones seleccionen agregados más efectivos, siempre y cuando las jerarquías definidas por el usuario se hayan establecido a lo largo de las rutas de acceso de la relación.  
  
    > [!NOTE]  
    >  Para obtener más información sobre la importancia y las implicaciones de definir y configurar las relaciones de atributo, vea la sección “Enhancing query performance” (Mejora del rendimiento de las consultas) en [SQL Server 2005 Analysis Services Performance Guide](http://go.microsoft.com/fwlink/?LinkId=81621)(Guía de rendimiento de SQL Server 2005 Analysis Services).  
  
## <a name="attribute-relationship-considerations"></a>Consideraciones sobre las relaciones de atributo  
 Si los datos subyacentes lo permiten, también debería definir relaciones de atributo únicas entre atributos. Para definir relaciones de atributo únicas, utilice la pestaña **Relación de los atributos** del Diseñador de dimensiones.  
  
 Cualquier atributo que tenga una relación de salida debe tener una clave única relativa a su atributo relacionado. En otras palabras, un miembro de un atributo de origen solo debe identificar un único miembro de un atributo relacionado. Por ejemplo, considere la relación, Ciudad -> Estado. En esta relación, el atributo de origen es Ciudad y el atributo relacionado es Estado. El atributo de origen es el lado "varios" y la parte relacionada es el lado "uno" de la relación de varios a uno. La clave para el atributo de origen sería Ciudad + Estado. Para obtener más información, vea [Crear, modificar o eliminar una relación de atributo](../../analysis-services/multidimensional-models/attribute-relationships-create-modify-or-delete-relationship.md).  
  
 Para obtener más información sobre las propiedades de una relación de atributo, vea [Configurar propiedades de relación de los atributos](../../analysis-services/multidimensional-models/attribute-relationships-configure-attribute-properties.md).  
  
> [!NOTE]  
>  Si las relaciones de atributo no se definen correctamente, puede que los resultados de las consultas no sean válidos.  
  
## <a name="see-also"></a>Vea también  
 [Relaciones de atributo](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)  
  
  
