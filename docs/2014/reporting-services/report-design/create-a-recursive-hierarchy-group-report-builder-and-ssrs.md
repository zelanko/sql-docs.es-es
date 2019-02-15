---
title: Crear un grupo de jerarquía recursiva (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 8b830ba5-4d64-4348-a2b1-76b9338a1462
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 28ccbab8475a2227dbd4dedfb0eb17bcd69dce03
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2019
ms.locfileid: "56288213"
---
# <a name="create-a-recursive-hierarchy-group-report-builder-and-ssrs"></a>Crear un grupo de jerarquía recursiva (Generador de informes y SSRS)
  Un grupo de jerarquía recursiva organiza los datos existentes en un único conjunto de datos de informe donde existen varios niveles jerárquicos, como puede ser la estructura de mando para las relaciones entre jefes y empleados en una jerarquía de organización.  
  
 Para poder organizar los datos de una tabla como un grupo de jerarquía recursiva, todos los datos jerárquicos deben hallarse en un único conjunto de datos, con campos independientes para el elemento que se va a agrupar y para el elemento por el que se va a agrupar. Por ejemplo, un conjunto de datos donde quiere agrupar a los empleados recursivamente bajo su jefe podría contener contenga un nombre, un nombre de empleado, un identificador de empleado y un identificador de jefe.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-create-a-recursive-hierarchy-group"></a>Para crear un grupo de jerarquía recursiva  
  
1.  En la vista Diseño, agregue una tabla y arrastre los campos del conjunto de datos que desea mostrar. Normalmente, el campo que se desea mostrar como una jerarquía se encuentra en la primera columna.  
  
2.  Haga clic con el botón secundario en cualquier lugar de la tabla para seleccionarla. El Panel de agrupación muestra el grupo de detalles para la tabla seleccionada. En el panel Grupos de filas, haga clic con el botón derecho en **Detalles**y, después, haga clic en **Editar grupo**. Se abrirá el cuadro de diálogo **Propiedades de grupo** .  
  
3.  En **Expresiones de grupo**, haga clic en **Agregar**. Aparecerá una nueva fila en la cuadrícula.  
  
4.  En la lista **Agrupar por** , escriba o seleccione el campo para agrupar.  
  
5.  Haga clic en **Avanzadas**.  
  
6.  En la lista **Primaria recursiva** , escriba o seleccione el campo por el que va a agrupar.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Ejecute el informe. El informe muestra el grupo de jerarquía recursiva, aunque no hay sangría que muestre la jerarquía.  
  
### <a name="to-format-a-recursive-hierarchy-group-with-indent-levels"></a>Para dar formato a un grupo de jerarquía recursiva con niveles de sangría  
  
1.  Haga clic en el cuadro de texto que contiene el campo al que desea agregar niveles de sangría para mostrar la jerarquía con formato. Las propiedades del cuadro de texto aparecen en el panel de propiedades.  
  
    > [!NOTE]  
    >  Si el panel Propiedades no está visible, en la pestaña **Ver** , haga clic en **Propiedades** .  
  
2.  En el panel Propiedades, expanda el `Padding` nodo, haga clic en **izquierda**y en la lista desplegable, seleccione  **\<Expression... >**.  
  
3.  En el panel Expresión, escriba la expresión siguiente:  
  
     `=CStr(2 + (Level()*10)) + "pt"`  
  
     Las propiedades de relleno requieren una cadena con el formato *nnyy*, donde *nn* es un número e *yy* es la unidad de medida. La expresión de ejemplo genera una cadena que usa la función `Level` para aumentar el tamaño del relleno según el nivel de recursividad. Por ejemplo, una fila que tenga un nivel de 1 daría lugar a un relleno de (2 + (1\*10))=12pt, y una fila que tenga un nivel de 3 se traduciría en un relleno de (2 + (3\*10))=32pt. Para obtener información sobre la `Level` de función, vea [nivel](report-builder-functions-level-function.md).  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Ejecute el informe. El informe muestra una vista jerárquica de los datos agrupados.  
  
## <a name="see-also"></a>Vea también  
 [Crear grupos de jerarquía recursiva &#40;Generador de informes y SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)   
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Referencia a las funciones de agregado &#40;Generador de informes y SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)   
 [Tablas &#40;Generador de informes y SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrices &#40;Generador de informes y SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Listas &#40;Generador de informes y SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
