---
title: Definir propiedades de atributo primario en una jerarquía de elementos primarios y secundarios | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 2d78fa73-a13b-4e12-bbd0-43e5307f760c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 36584cce341bdbe0e13b917cbe1bcc47469d0deb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62729174"
---
# <a name="defining-parent-attribute-properties-in-a-parent-child-hierarchy"></a>Definir propiedades de atributo primario en una jerarquía de elementos primarios y secundarios
  Una jerarquía de elementos primarios y secundarios es una jerarquía de una dimensión que está basada en dos columnas de tabla. La combinación de estas columnas define las relaciones jerárquicas entre los miembros de dimensión. La primera columna, denominada *columna de claves de miembro*, identifica a cada miembro de dimensión. La otra columna, denominada *columna principal*, identifica al elemento principal de cada miembro de dimensión. La propiedad **NamingTemplate** de un atributo primario determina el nombre de cada nivel en la jerarquía de elementos primarios y secundarios, y la propiedad **MembersWithData** determina si deben mostrarse los datos de los miembros primarios.  
  
 Para obtener más información, consulte [jerarquía de elementos primarios y secundarios](multidimensional-models/parent-child-dimension.md), [atributos en jerarquías de elementos primarios y secundarios](multidimensional-models/parent-child-dimension-attributes.md)  
  
> [!NOTE]  
>  Cuando se utiliza el Asistente para dimensiones con objeto de crear una dimensión, el asistente reconoce las tablas que incluyen relaciones de elementos primarios y secundarios, y define automáticamente la jerarquía de elementos primarios y secundarios.  
  
 En las tareas de este tema, creará una plantilla de asignación de nombres que define el nombre para cada nivel en la jerarquía de elementos primarios y secundarios de la dimensión **Employee** . A continuación, configurará el atributo primario para ocultar todos los datos primarios, de modo que solo se muestren las ventas de los miembros del nivel de hoja.  
  
## <a name="browsing-the-employee-dimension"></a>Examinar la dimensión Employee  
  
1.  En el Explorador de soluciones, haga doble clic en **Employee.dim** en la carpeta **Dimensiones** para abrir el Diseñador de dimensiones para la dimensión Employee.  
  
2.  Haga clic en la pestaña **Explorador** , compruebe que **Employees** está seleccionado en la lista **Jerarquía** y, después, expanda el miembro **All Employees** .  
  
     Observe que **Ken J. Sánchez** es el director de nivel superior de esta jerarquía de elementos primarios y secundarios.  
  
3.  Seleccione el miembro **Ken J. Sánchez** .  
  
     Observe que el nombre de nivel para este miembro es **Level 02**. (El nombre de nivel aparece después de **Nivel actual:**, justo encima del miembro **All Employees**.) En esta tarea, definirá nombres más descriptivos para cada nivel.  
  
4.  Expanda **Ken J. Sánchez** para ver los nombres de los empleados que informan a este director y, después, seleccione **Brian S. Welcker** para ver el nombre de este nivel.  
  
     Observe que el nombre de nivel para este miembro es **Level 03**.  
  
5.  En el Explorador de soluciones, haga doble clic en **Analysis Services Tutorial.cube** en la carpeta **Cubos** para abrir el Diseñador de cubos para el cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
6.  Haga clic en la pestaña **Explorador** .  
  
7.  Haga clic en el icono de Excel y, después, haga clic en **Habilitar** cuando se le pida que habilite las conexiones.  
  
8.  En la Lista de campos de tabla dinámica, expanda **Reseller Sales**. Arrastre **Reseller Sales-Sales Amount** hasta el área Valores.  
  
9. En la Lista de campos de tabla dinámica, expanda **Employee**, y arrastre la jerarquía **Employees** hasta el área **Filas** .  
  
     Todos los miembros de la jerarquía Employees se agregarán a la columna A del informe de tabla dinámica.  
  
     En la ilustración siguiente se muestra expandida la jerarquía Employees.  
  
10. ![Tabla dinámica que muestra la jerarquía Employees](../../2014/tutorials/media/l4-employee-1.gif "tabla dinámica que muestra la jerarquía Employees")  
  
     Observe que las ventas realizadas por cada director del nivel 03 también se muestran en el nivel 04. Esto es así porque cada director también es un empleado de otro director. En la tarea siguiente, ocultará estos importes de ventas.  
  
## <a name="modifying-parent-attribute-properties-in-the-employee-dimension"></a>Modificar las propiedades de los atributos primarios en la dimensión Employee  
  
1.  Cambie al Diseñador de dimensiones para la dimensión **Employee** .  
  
2.  Haga clic en la pestaña **Estructura de dimensión** , y, después, seleccione la jerarquía de atributo **Employees** en el panel **Atributos** .  
  
     Observe el icono único de este atributo. Este icono significa que el atributo es la clave principal de una jerarquía de elementos primarios y secundarios. Observe también que, en la ventana Propiedades, la propiedad **Usage** del atributo está definida como **Primaria**. Esta propiedad se estableció con el Asistente para dimensiones cuando se diseñó la dimensión. El asistente detectó automáticamente la relación de elementos primarios y secundarios.  
  
3.  En la ventana Propiedades, haga clic en el botón de puntos suspensivos (**...**) de la celda de la propiedad **NamingTemplate** .  
  
     En el cuadro de diálogo **Plantilla de asignación de nombres de nivel**, debe definir la plantilla de asignación de nombres de nivel que determina los nombres de nivel de la jerarquía de elementos primarios y secundarios que se muestran a los usuarios cuando examinan los cubos.  
  
4.  En la segunda fila, la fila **\***, escriba **Employee Level \*** en la columna **Nombre** y después haga clic en la tercera fila.  
  
     Observe que, bajo **Resultado**, cada nivel ahora se denominará "Employee Level" seguido por un número que aumenta de forma secuencial.  
  
     En la imagen siguiente se muestran los cambios realizados en el cuadro de diálogo **Plantilla de asignación de nombres de nivel** .  
  
     ![Cuadro de diálogo plantilla de nomenclatura nivel](../../2014/tutorials/media/l4-namingtemplate.gif "cuadro de diálogo plantilla de nivel de nomenclatura")  
  
5.  Haga clic en **Aceptar**.  
  
6.  En la ventana Propiedades del atributo **Employees** , en la celda de la propiedad **MembersWithData** , seleccione **NonLeafDataHidden** para cambiar este valor por el atributo **Employees** .  
  
     De este modo se ocultarán los datos relacionados con los miembros no hoja de la jerarquía de elementos primarios y secundarios.  
  
## <a name="browsing-the-employee-dimension-with-the-modified-attributes"></a>Examinar la dimensión Employee con los atributos modificados  
  
1.  En el menú **Generar** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], haga clic en **Implementar Tutorial de Analysis Services**.  
  
2.  Cuando la implementación se haya completado correctamente, cambie al Diseñador de cubos para el cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y haga clic en **Volver a conectar** en la pestaña **Explorador** .  
  
3.  Haga clic en el icono de Excel y, a continuación, haga clic en **Habilitar**.  
  
4.  Arrastre **Reseller Sales-Sales Amount** hasta el área Valores.  
  
5.  Arrastre la jerarquía **Employees** hasta el área Etiquetas de fila.  
  
     En la imagen siguiente se muestran los cambios realizados en la jerarquía Employees. Observe que Stephen Y. Jiang ya no aparece como empleado de sí mismo.  
  
     ![Puede modificar la jerarquía Employees](../../2014/tutorials/media/l4-employee-2.png "jerarquía Employees modificado")  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Agrupar miembros de atributo automáticamente](../analysis-services/lesson-4-3-automatically-grouping-attribute-members.md)  
  
## <a name="see-also"></a>Vea también  
 [Jerarquía de elementos primarios y secundarios](multidimensional-models/parent-child-dimension.md)   
 [Atributos en las jerarquías de elementos primarios y secundarios](multidimensional-models/parent-child-dimension-attributes.md)  
  
  
