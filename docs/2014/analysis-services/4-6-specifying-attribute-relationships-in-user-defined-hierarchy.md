---
title: Especificar relaciones de atributo entre atributos en una jerarquía definida por el usuario | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 456c2a47-d395-45f9-9efa-89f3fa2ac621
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 490d9f6e1cdaeab274290649d2bb7f5c691595ae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66063030"
---
# <a name="specifying-attribute-relationships-between-attributes-in-a-user-defined-hierarchy"></a>Especificar relaciones de atributo entre los atributos de una jerarquía definida por el usuario
  Como ya ha visto en este tutorial, es posible organizar jerarquías de atributo en niveles dentro de jerarquías de usuario para proporcionar rutas de navegación a los usuarios de un cubo. Una jerarquía de usuario puede representar una jerarquía natural, como una ciudad, un estado o un país, o simplemente representar una ruta de navegación, como el nombre de un empleado, su cargo y el nombre de departamento. Para el usuario que navega por una jerarquía, estos dos tipos de jerarquía de usuario son el mismo.  
  
 Con una jerarquía natural, si define relaciones de atributo entre los atributos que forman los niveles, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] puede utilizar una agregación de un atributo para obtener los resultados de un atributo relacionado. Si no hay ninguna relación definida entre los atributos, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] agregará todos los atributos que no sean de clave del atributo de clave. Por lo tanto, si los datos subyacentes lo permiten, debería definir relaciones de atributo entre atributos. La definición de relaciones de atributo mejora el rendimiento del procesamiento de las dimensiones, las particiones y las consultas. Para obtener más información, consulte [Definir relaciones de atributo](multidimensional-models/attribute-relationships-define.md) y [Relaciones de atributo](multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
 Cuando se definen relaciones de atributo, se puede especificar que la relación sea flexible o rígida. Si define una relación rígida, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] retiene las agregaciones cuando se actualiza la dimensión. Si la relación que se define como rígida cambia, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] genera un error durante el proceso, a menos que la dimensión se procese por completo. El rendimiento de la consulta y del procesamiento aumenta si se especifican las relaciones y las propiedades de relación apropiadas. Para obtener más información, consulte [Definir relaciones de atributo](multidimensional-models/attribute-relationships-define.md) y [Propiedades de jerarquía de usuario](multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md).  
  
 En las tareas de este tema, debe definir relaciones de atributo para los atributos de las jerarquías de usuario naturales del proyecto Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Estas jerarquías son la jerarquía **Customer Geography** de la dimensión **Custome**r, la jerarquía **Sales Territory** de la dimensión **Sales Territory** , la jerarquía **Product Model** Lines de la dimensión **Product** y las jerarquías **Fiscal Date** y **Calendar Date** de la dimensión **Date** . Todas estas jerarquías de usuario son jerarquías naturales.  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-customer-geography-hierarchy"></a>Definir relaciones de atributo para atributos de la jerarquía Customer Geography  
  
1.  Cambie al Diseñador de dimensiones para la dimensión Customer y haga clic en la pestaña **Estructura de dimensión** .  
  
     En el panel **Jerarquías** , fíjese en los niveles de la jerarquía definida por el usuario **Customer Geography** . Actualmente, esta jerarquía es simplemente una ruta que permite a los usuarios ver detalles, ya que no se han definido relaciones entre niveles o atributos.  
  
2.  Haga clic en la pestaña **Relación de atributo** .  
  
     Observe las cuatro relaciones de atributo que vinculan los atributos que no son de clave de la tabla **Geography** con el atributo de clave de la tabla **Geography** . El atributo **Geography** está relacionado con el atributo **Full Name** . El atributo **Postal Code** está vinculado de forma indirecta al atributo **Full Name** a través del atributo **Geography** , porque el atributo **Postal Code** está vinculado al atributo **Geography** y el atributo **Geography** está vinculado al atributo **Full Name** . A continuación, cambiaremos las relaciones de atributo para que no usen el atributo **Geography** .  
  
3.  En el diagrama, haga clic con el botón derecho en el atributo **Full Name** y seleccione **Nueva relación de atributo**.  
  
4.  En el cuadro de diálogo **Crear relación de atributo** , el **Atributo de origen** es **Full Name**. Establezca el **Atributo relacionado** en **Postal Code**. En la lista **Tipo de relación**, deje establecido el tipo de relación en **Flexible**, ya que las relaciones entre los miembros pueden cambiar con el tiempo.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     Aparece un icono de advertencia en el diagrama porque la relación es redundante. La relación **Full Name** -> **Geography**-> **Postal Code** ya existía y acaba de crear la relación **Full Name** -> **Postal Code**. Ahora, la relación **Geography**-> **Postal Code** es redundante y la eliminaremos.  
  
6.  En el panel **Relaciones de atributo** , haga clic con el botón derecho en **Geography**-> **Postal Code** y, después, haga clic en **Eliminar**.  
  
7.  Cuando aparezca el cuadro de diálogo **Eliminar objetos**, haga clic en **Aceptar**.  
  
8.  En el diagrama, haga clic con el botón derecho en el atributo **Postal Code** y seleccione **Nueva relación de atributo**.  
  
9. En el cuadro de diálogo **Crear relación de atributo** , el **Atributo de origen** es **Postal Code**. Establezca el **Atributo relacionado** en **City**. En la lista **Tipo de relación** , deje establecido el tipo de relación en **Flexible**.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     Ahora, la relación **Geography**-> **City** es redundante y la eliminaremos.  
  
11. En el panel Relaciones de atributo, haga clic con el botón derecho en **Geography**-> **City** y, después, haga clic en **Eliminar**.  
  
12. Cuando aparezca el cuadro de diálogo **Eliminar objetos** , haga clic en **Aceptar**.  
  
13. En el diagrama, haga clic con el botón derecho en el atributo **City** y seleccione **Nueva relación de atributo**.  
  
14. En el cuadro de diálogo **Crear relación de atributo** , el **Atributo de origen** es **City**. Establezca el **Atributo relacionado** en **State-Province**. En la lista **Tipo de relación** , establezca el tipo de relación en **Rígida** , ya que la relación entre una ciudad y un estado no cambiará en el futuro.  
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
16. Haga clic con el botón derecho en la flecha situada entre **Geography** y **State-Province** y, después, haga clic en **Eliminar**.  
  
17. Cuando aparezca el cuadro de diálogo **Eliminar objetos** , haga clic en **Aceptar**.  
  
18. En el diagrama, haga clic con el botón derecho en el atributo **State-Province** y seleccione **Nueva relación de atributo**.  
  
19. En el cuadro de diálogo **Crear relación de atributo** , el **Atributo de origen** es **State-Province**. Establezca el **Atributo relacionado** en **Country-Region**. En la lista **Tipo de relación** , establezca el tipo de relación en **Rígida** , ya que la relación entre un estado-provincia y un país-región no cambiará con el tiempo.  
  
20. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
21. En el panel Relaciones de atributo, haga clic con el botón derecho en **Geography**-> **Country-Region** y, después, haga clic en **Eliminar**.  
  
22. Cuando aparezca el cuadro de diálogo **Eliminar objetos** , haga clic en **Aceptar**.  
  
23. Haga clic en la pestaña **Estructura de dimensión** .  
  
     Observe que al eliminar la última relación de atributo entre **Geography** y otros atributos, se elimina **Geography** . Esto se debe a que el atributo ya no se usa.  
  
24. En el menú Archivo, haga clic en **Guardar todo**.  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-sales-territory-hierarchy"></a>Definir relaciones de atributo para atributos de la jerarquía Sales Territory  
  
1.  Abra el Diseñador de dimensiones para la dimensión **Sales Territory** y haga clic en la pestaña **Relaciones de atributo** .  
  
2.  En el diagrama, haga clic con el botón derecho en el atributo **Sales Territory Country** y seleccione **Nueva relación de atributo**.  
  
3.  En el cuadro de diálogo **Crear relación de atributo** , el **Atributo de origen** es **Sales Territory Country**. Establezca el **Atributo relacionado** en **Sales Territory Group**. En la lista **Tipo de relación** , deje establecido el tipo de relación en **Flexible**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     **Sales Territory Group** ahora está vinculado a **Sales Territory Country**y **Sales Territory Country** está vinculado a **Sales Territory Region**. La propiedad **RelationshipType** de cada una de estas relaciones se establece en **Flexible** porque las agrupaciones de las regiones dentro de un país y las agrupaciones de los países en grupos pueden cambiar con el tiempo.  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-product-model-lines-hierarchy"></a>Definir relaciones de atributo para atributos de la jerarquía Product Model Lines  
  
1.  Abra el Diseñador de dimensiones para la dimensión **Product** y haga clic en la pestaña **Relaciones de atributo** .  
  
2.  En el diagrama, haga clic con el botón derecho en el atributo **Model Name** y seleccione **Nueva relación de atributo**.  
  
3.  En el cuadro de diálogo **Crear relación de atributo** , el **Atributo de origen** es **Model Name**. Establezca el **Atributo relacionado** en **Product Line**. En la lista **Tipo de relación**, deje establecido el tipo de relación en **Flexible**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-fiscal-date-hierarchy"></a>Definir relaciones de atributo para atributos de la jerarquía Fiscal Date  
  
1.  Cambie al Diseñador de dimensiones para la dimensión **Date** y, después, haga clic en la pestaña **Relaciones de atributo** .  
  
2.  En el diagrama, haga clic con el botón secundario en el atributo **Month Name** y seleccione **Nueva relación de atributo**.  
  
3.  En el cuadro de diálogo **Crear relación de atributo** , el **Atributo de origen** es **Month Name**. Establezca el **Atributo relacionado** en **Fiscal Quarter**. En la lista **Tipo de relación** , establezca el tipo de relación en **Rígida**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  En el diagrama, haga clic con el botón derecho en el atributo **Fiscal Quarter** y seleccione **Nueva relación de atributo**.  
  
6.  En el cuadro de diálogo **Crear relación de atributo** , el **Atributo de origen** es **Fiscal Quarter**. Establezca el **Atributo relacionado** en **Fiscal Semester**. En la lista **Tipo de relación** , establezca el tipo de relación en **Rígida**.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  En el diagrama, haga clic con el botón derecho en el atributo **Fiscal Semester** y seleccione **Nueva relación de atributo**.  
  
9. En el cuadro de diálogo **Crear relación de atributo** , el **Atributo de origen** es **Fiscal Semester**. Establezca el **Atributo relacionado** en **Fiscal Year**. En la lista **Tipo de relación** , establezca el tipo de relación en **Rígida**.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-calendar-date-hierarchy"></a>Definir relaciones de atributo para atributos de la jerarquía Calendar Date  
  
1.  En el diagrama, haga clic con el botón derecho en el atributo **Month Name** y seleccione **Nueva relación de atributo**.  
  
2.  En el cuadro de diálogo **Crear relación de atributo**, el **Atributo de origen** es **Month Name**. Establezca el **Atributo relacionado** en **Calendar Quarter**. En la lista **Tipo de relación** , establezca el tipo de relación en **Rígida**.  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
4.  En el diagrama, haga clic con el botón derecho en el atributo **Calendar Quarter** y seleccione **Nueva relación de atributo**.  
  
5.  En el cuadro de diálogo **Crear relación de atributo** , el **Atributo de origen** es **Calendar Quarter**. Establezca el **Atributo relacionado** en **Calendar Semester**. En la lista **Tipo de relación** , establezca el tipo de relación en **Rígida**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  En el diagrama, haga clic con el botón derecho en el atributo **Calendar Semester** y seleccione **Nueva relación de atributo**.  
  
8.  En el cuadro de diálogo **Crear relación de atributo**, el **Atributo de origen** es **Calendar Semester**. Establezca el **Atributo relacionado** en **Calendar Year**. En la lista **Tipo de relación** , establezca el tipo de relación en **Rígida**.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-geography-hierarchy"></a>Definir relaciones de atributo para atributos de la jerarquía Geography  
  
1.  Abra el Diseñador de dimensiones para la dimensión Geography y haga clic en la pestaña **Relaciones de atributo** .  
  
2.  En el diagrama, haga clic con el botón derecho en el atributo **Postal Code** y seleccione **Nueva relación de atributo**.  
  
3.  En el cuadro de diálogo **Crear relación de atributo** , el **Atributo de origen** es **Postal Code**. Establezca el **Atributo relacionado** en **City**. En la lista **Tipo de relación** , establezca el tipo de relación en **Flexible**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  En el diagrama, haga clic con el botón derecho en el atributo **City** y seleccione **Nueva relación de atributo**.  
  
6.  En el cuadro de diálogo **Crear relación de atributo** , el **Atributo de origen** es **City**. Establezca el **Atributo relacionado** en **State-Province**. En la lista **Tipo de relación** , establezca el tipo de relación en **Rígida**.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  En el diagrama, haga clic con el botón derecho en el atributo **State-Province** y seleccione **Nueva relación de atributo**.  
  
9. En el cuadro de diálogo **Crear relación de atributo** , el **Atributo de origen** es **State-Province**. Establezca el **Atributo relacionado** en **Country-Region**. En la lista **Tipo de relación** , establezca el tipo de relación en **Rígida**.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. En el diagrama, haga clic con el botón derecho en el atributo **Geography Key** y, después, seleccione **Propiedades**.  
  
12. Establezca la propiedad **AttributeHierarchyOptimizedState** en **NotOptimized**, la propiedad **AttributeHierarchyOrdered** en **False**y la propiedad **AttributeHierarchyVisible** en **False**.  
  
13. En el menú **Archivo** , haga clic en **Guardar todo**.  
  
14. En el menú **Generar** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], haga clic en **Implementar Tutorial de Analysis Services**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Definir las propiedades de miembro desconocido y de procesamiento de valores NULL](../analysis-services/lesson-4-7-defining-the-unknown-member-and-null-processing-properties.md)  
  
## <a name="see-also"></a>Vea también  
 [Definir relaciones de atributo](multidimensional-models/attribute-relationships-define.md)   
 [Propiedades de jerarquía de usuario](multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)  
  
  
