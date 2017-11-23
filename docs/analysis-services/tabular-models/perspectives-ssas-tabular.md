---
title: Perspectivas (SSAS Tabular) | Documentos de Microsoft
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1f78c3a1-ce2c-4e7f-a277-71a657692bea
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 36e28c1211017a46a66ce7c7ef519eb887248c8f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="perspectives"></a>Perspectivas
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
 [Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)   
 [Jerarquías](../../analysis-services/tabular-models/hierarchies-ssas-tabular.md)  
  
  
