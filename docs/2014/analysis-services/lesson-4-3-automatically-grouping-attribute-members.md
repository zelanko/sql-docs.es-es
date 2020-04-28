---
title: Agrupar miembros de atributo automáticamente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9fb2cda3-a122-4a4c-82e0-3454865eef04
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7fc8bed16488f1688576d6c5b265811cdc9705a1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175344"
---
# <a name="automatically-grouping-attribute-members"></a>Agrupar miembros de atributo automáticamente
  Cuando se examina un cubo, generalmente se dimensionan los miembros de una jerarquía de atributo según los miembros de otra jerarquía de atributo. Por ejemplo, puede agrupar las ventas de cliente por ciudad, producto comprado o género. Sin embargo, con ciertos tipos de atributos, resulta útil [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] crear automáticamente agrupaciones de miembros de atributos en función de la distribución de los miembros dentro de una jerarquía de atributo. Por ejemplo, puede hacer que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cree grupos de valores de ingresos anuales de los clientes. Al hacerlo, los usuarios que examinen la jerarquía de atributo verán los nombres y los valores de los grupos en lugar de los miembros propiamente dichos. Esto limita el número de niveles que se presentan a los usuarios, lo que puede resultar más útil para el análisis.

 La propiedad **DiscretizationMethod** determina si [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] crea agrupaciones, así como el tipo de agrupación que se lleva a cabo. De forma predeterminada, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no realiza agrupaciones. Si habilita las agrupaciones automáticas, puede permitir que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] determine automáticamente el mejor método de agrupación en función de la estructura del atributo, o puede elegir uno de los algoritmos de agrupación de la lista siguiente para especificar el método de agrupación:

 **EqualAreas** [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] crea intervalos de grupos de modo que la población total de los miembros de dimensión quede distribuida de forma homogénea en los grupos.

 Los **clústeres** [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] crean grupos mediante la agrupación en clústeres unidimensionales en los valores de entrada mediante el método de agrupación en clústeres K-means con distribuciones gaussiano. Esta opción solo es válida para columnas numéricas.

 Una vez que haya especificado un método de agrupación, debe especificar el número de grupos mediante la propiedad **DiscretizationBucketCount** . Para obtener más información, vea [Group Attribute members &#40;discretización&#41;](multidimensional-models/attribute-properties-group-attribute-members.md)

 En las tareas de este tema, habilitará distintos tipos de agrupaciones para lo siguiente: valores de los ingresos anuales en la dimensión **Customer** , número de horas de baja por enfermedad del empleado en la dimensión **Employees** , y número de horas de vacaciones del empleado en la dimensión **Employees** . A continuación procesará y examinará el cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para ver el efecto de los grupos de miembro. Por último, modificará las propiedades del grupo de miembro para ver el efecto del cambio en el tipo de agrupación.

## <a name="grouping-attribute-hierarchy-members-in-the-customer-dimension"></a>Agrupar miembros de la jerarquía de atributo en la dimensión Customer

1.  En el Explorador de soluciones, haga doble clic en **Customer** en la carpeta **Dimensiones** para abrir el Diseñador de dimensiones para la dimensión Customer.

2.  En el panel **Vista del origen de datos** , haga clic con el botón derecho en la tabla **Customer** y luego haga clic en **Explorar datos**.

     Observe el intervalo de valores de la columna **YearlyIncome** . Estos valores pasan a ser miembros de la jerarquía de atributo **Yearly Income** , a menos que habilite la agrupación de miembro.

3.  Cierre la pestaña **Explorar la tabla Customer** .

4.  En el panel **Atributos** , seleccione **Yearly Income**.

5.  En el ventana Propiedades, cambie el valor de la propiedad **DiscretizationMethod** a **automático** y cambie el valor de la propiedad **DiscretizationBucketCount** a `5`.

     En la imagen siguiente se muestran las propiedades modificadas para **Yearly Income**.

     ![Propiedades modificadas de Yearly Income](../../2014/tutorials/media/l4-discretizationmethod-1.gif "Propiedades modificadas de Yearly Income")

## <a name="grouping-attribute-hierarchy-members-in-the-employee-dimension"></a>Agrupar miembros de la jerarquía de atributo en la dimensión Employee

1.  Cambie al Diseñador de dimensiones para la dimensión Employee.

2.  En el panel **Vista del origen de datos** , haga clic con el botón derecho en la tabla **Employee** y luego haga clic en **Explorar datos**.

     Fíjese en los valores de las columnas **SickLeaveHours** y **VacationHours** .

3.  Cierre la pestaña **Explorar la tabla Employee** .

4.  En el panel **Atributos** , seleccione **Sick Leave Hours**.

5.  En el ventana Propiedades, cambie el valor de la propiedad **DiscretizationMethod** a **clusters** y cambie el valor de la propiedad **DiscretizationBucketCount** a `5`.

6.  En el panel **Atributos** , seleccione **Vacation Hours**.

7.  En el ventana Propiedades, cambie el valor de la propiedad **DiscretizationMethod** a **áreas iguales** y cambie el valor de la propiedad **DiscretizationBucketCount** a `5`.

## <a name="browsing-the-modified-attribute-hierarchies"></a>Examinar las jerarquías de atributo modificadas

1.  En el menú **Generar** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], haga clic en **Implementar Tutorial de Analysis Services**.

2.  Cuando la implementación se haya completado correctamente, cambie al Diseñador de cubos para el cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y haga clic en **Volver a conectar** en la pestaña **Explorador** .

3.  Haga clic en el icono de Excel y, a continuación, haga clic en **Habilitar**.

4.  Arrastre la medida **Internet Sales-Sales Amount** hasta el área Valores de la lista de campos de la tabla dinámica.

5.  En la lista de campos, expanda la dimensión **Product** y, a continuación, arrastre la jerarquía de usuario **Product Model Lines** hasta el área **Etiquetas de fila** de la lista de campos.

6.  Expanda la dimensión **Customer** en la lista de campos, expanda la carpeta para mostrar **Demographic** y, a continuación, arrastre la jerarquía de atributo **Yearly Income** hasta el área **Etiquetas de columna** .

     Los miembros de la jerarquía de atributo **Yearly Income** están agrupados ahora en seis depósitos, incluido un depósito para las ventas a los clientes cuyos ingresos anuales se desconocen. No se muestran todos los depósitos.

7.  Quite la jerarquía de atributo **Yearly Income** del área de columnas y quite la medida **Internet Sales-Sales Amount** del área **Valores** .

8.  Agregue la medida **Reseller Sales-Sales Amount** al área de datos.

9. En la lista de campos, expanda la dimensión **Employee** , expanda **Organization**y arrastre **Sick Leave Hours** hasta **Etiquetas de columna**.

     Observe que todas las ventas las realizan los empleados de uno de los dos grupos. Observe también que los empleados que tienen de 32 a 42 horas de baja por enfermedad han realizado más ventas que los que tienen de 20 a 31 horas de baja por enfermedad.

     En la imagen siguiente se muestran las ventas dimensionadas por horas de baja por enfermedad de los empleados.

     ![Sales con dimensión por horas de baja por enfermedad de los empleados](../../2014/tutorials/media/l4-discretizationmethod-2.gif "Sales con dimensión por horas de baja por enfermedad de los empleados")

10. Elimine la jerarquía de atributo **Sick Leave Hours** del área de columnas del panel **Datos** .

11. Agregue **Vacation Hours** al área de columnas del panel **Datos** .

     Observe que aparecen dos grupos, basados en el método de agrupación por áreas iguales (EqualAreas). Hay otros tres grupos ocultos porque no contienen valores de datos.

## <a name="modifying-grouping-properties-and-reviewing-the-effect-of-the-changes"></a>Modificar propiedades de agrupación y revisar el efecto de los cambios

1.  Cambie al Diseñador de dimensiones para la dimensión **Employee** y seleccione **Vacation Hours** en el panel **Atributos** .

2.  En la ventana Propiedades, cambie el valor de la propiedad **DiscretizationBucketCount** por **10.**

3.  En el menú **Generar** de [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga clic en **Implementar Tutorial de Analysis Services**.

4.  Cuando la implementación se haya completado correctamente, vuelva al Diseñador de cubos para el cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .

5.  Haga clic en **Volver a conectar** en la pestaña **Explorador** , haga clic en el icono de Excel y vuelva a crear la tabla dinámica para que pueda ver el efecto del cambio al método de agrupación:

    1.  Arrastre Reseller Sales-Sales Amount hasta Valores

    2.  Arrastre Vacation Hours (en la carpeta Employees Organization) hasta Columnas

    3.  Arrastre Product Model Lines hasta Filas

     Observe que ahora hay tres grupos de miembros del atributo **Vacation Hours** que tienen valores de ventas para productos. Los otros siete grupos contienen miembros sin datos de ventas.

## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección
 [Ocultar y deshabilitar jerarquías de atributo](lesson-4-4-hiding-and-disabling-attribute-hierarchies.md)

## <a name="see-also"></a>Consulte también
 [Agrupar miembros de atributos &#40;discretización&#41;](multidimensional-models/attribute-properties-group-attribute-members.md)


