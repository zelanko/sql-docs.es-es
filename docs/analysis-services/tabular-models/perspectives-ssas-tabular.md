---
title: Las perspectivas | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3e687116fa1f388da3b59884c29526cb9e7dd629
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="perspectives"></a>Perspectivas
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  En los modelos tabulares, las perspectivas definen subconjuntos visibles de un modelo que ofrecen puntos de vista centrados, específicos del negocio o específicos de la aplicación del modelo.  
  
##  <a name="bkmk_understanding"></a> Ventajas  
 Los modelos tabulares pueden ser muy complejos para que los usuarios los exploren. Un solo modelo puede representar el contenido de un almacenamiento de datos completo, con muchas tablas, medidas y dimensiones. Esta complejidad puede resultar desalentadora para los usuarios que solo necesitan interactuar con una pequeña parte del modelo para satisfacer sus requisitos de informes y de Business Intelligence.  
  
 En una perspectiva, se definen tablas, columnas y medidas (incluidos los KPI) como objetos de campo. Puede seleccionar los campos visibles para cada perspectiva. Por ejemplo, un único modelo puede contener datos de productos, ventas, financieros, de empleados y geográficos. Si bien un departamento de ventas necesita datos de productos, ventas, promociones y geográficos, probablemente no necesitarán datos de empleados ni financieros. Del mismo modo, un departamento de recursos humanos no necesita datos sobre promociones de ventas ni geográficos.  
  
 Cuando un usuario se conecta a un modelo (como un origen de datos) que tiene perspectivas definidas, dicho usuario puede seleccionar la perspectiva que desea usar. Por ejemplo, al conectarse a un origen de datos de modelo en Excel, los usuarios de recursos humanos pueden seleccionar la perspectiva Recursos humanos en la página Seleccionar tablas y vistas del Asistente para la conexión de datos. En la lista de campos de la tabla dinámica solo se verán los campos (tablas, columnas y medidas) definidos para la perspectiva Recursos humanos.  
  
 Las perspectivas no están diseñadas para usarse como mecanismo de seguridad, sino como una herramienta para proporcionar una mejor experiencia para el usuario. Toda la seguridad de una determinada perspectiva se hereda del modelo subyacente. Las perspectivas no pueden proporcionar acceso a objetos de modelo a los que el usuario no tiene acceso. La seguridad de la base de datos de modelos se debe resolver antes de dar acceso a los objetos del modelo mediante una perspectiva. Los roles de seguridad se pueden usar para proteger los datos y los metadatos de los modelos. Para obtener más información, consulte [Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md).  
  
##  <a name="bkmk_testpersp"></a> Testing perspectives  
 Al crear un modelo, puede usar la característica Analizar en Excel del diseñador de modelos para probar la eficacia de las perspectivas que ha definido. En el menú **Modelo** del diseñador de modelos, al hacer clic en **Analizar en Excel**, y antes de que se inicie Excel, aparecerá el cuadro de diálogo **Elegir credenciales y perspectivas** . En este cuadro de diálogo, puede especificar el nombre de usuario actual, otro usuario, un rol y una perspectiva que usará para conectar con la base de datos del área de trabajo del modelo como origen de datos y para ver los datos.  
  
##  <a name="bkmk_related_tasks"></a> Related tasks  
  
|Tema|Description|  
|-----------|-----------------|  
|[Crear y administrar perspectivas](../../analysis-services/tabular-models/create-and-manage-perspectives-ssas-tabular.md)|Describe cómo crear y administrar perspectivas mediante el cuadro de diálogo Perspectivas del diseñador de modelos.|  
  
## <a name="see-also"></a>Vea también  
 [roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)   
 [Jerarquías](../../analysis-services/tabular-models/hierarchies-ssas-tabular.md)  
  
  
