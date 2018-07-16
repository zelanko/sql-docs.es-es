---
title: Combinar tablas en varias columnas (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- multiple column joins
- joins [SQL Server], multiple columns
ms.assetid: 56a158bc-a42a-4b78-baad-4721d2d22cd3
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e0b8807ad4a8b2cbcadc0ecaa30db2db105ed482
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37218695"
---
# <a name="join-tables-on-multiple-columns-visual-database-tools"></a>Combinar tablas en varias columnas (Visual Database Tools)
  Puede combinar tablas con varias columnas. Es decir, puede crear una consulta que compare filas de las dos tablas solo si cumplen varias condiciones. Si la base de datos contiene una relación en la que varias columnas de clave externa de una tabla se corresponden con una clave principal de varias columnas en la otra tabla, puede utilizar esta relación para crear una combinación de varias columnas. Para detalles, consulte [Combinar tablas automáticamente &#40;Visual Database Tools&#41;](visual-database-tools.md).  
  
 Aunque la base de datos no contenga una relación de clave externa de varias columnas, puede crear la combinación manualmente.  
  
### <a name="to-manually-create-a-multicolumn-join"></a>Para crear una combinación de varias columnas manualmente  
  
1.  Agregue al [panel Diagrama](diagram-pane-visual-database-tools.md) las tablas que desea combinar.  
  
2.  Arrastre el nombre de la primera columna de combinación de la ventana de la primera tabla y colóquela en la columna relacionada de la ventana de la segunda tabla. No puede basar una combinación en columnas del tipo de datos text, ntext o image.  
  
    > [!NOTE]  
    >  Por lo general, las columnas de combinación deben tener el mismo tipo de datos (o compatibles). Por ejemplo, si la columna de combinación de la primera tabla es una fecha, deberá relacionarla con una columna de fecha de la segunda tabla. O bien, si la primera columna de combinación es un entero, la columna de combinación relacionada debe ser también de un tipo de datos entero, pero puede tener un tamaño diferente. Sin embargo, puede haber casos en los que las conversiones de tipos de datos implícitas pueden unir columnas aparentemente incompatibles correctamente.  
    >   
    >  El [Diseñador de consultas y vistas](query-and-view-designer-tools-visual-database-tools.md) no comprobará los tipos de datos de las columnas que utilice para crear una combinación, pero al ejecutar la consulta, la base de datos mostrará un error si los tipos de datos no son compatibles.  
  
3.  Arrastre el nombre de la segunda columna de combinación de la ventana de la primera tabla y colóquela en la columna relacionada de la ventana de la segunda tabla.  
  
4.  Repita el paso 3 para cada par adicional de columnas de combinación en las dos tablas.  
  
5.  Ejecuta la consulta.  
  
## <a name="see-also"></a>Vea también  
 [Realizar consultas con combinaciones &#40;Visual Database Tools&#41;](query-with-joins-visual-database-tools.md)  
  
  
