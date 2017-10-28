---
title: "Tablas y columnas (cuadro de diálogo, Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdt.dlgbox.tablesandcolumns
ms.assetid: 8cf27be1-e66d-4735-a428-9ab4b33af4f5
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 34307dfeb1d1670ced8011d8f541143b1c1de42b
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="tables-and-columns-dialog-box-visual-database-tools"></a>Tablas y columnas (cuadro de diálogo, Visual Database Tools)
Utilice este cuadro de diálogo para asignar una clave principal de una tabla a una clave externa de otra. Para obtener acceso a este cuadro de diálogo, en el menú **Diseñador de tablas** haga clic en **Relaciones**. En el cuadro de diálogo **Relaciones de clave externa** , haga clic en el campo **Especificación de tablas y columnas** y, luego, haga clic en los puntos suspensivos **(...)** que aparecen a la derecha de la propiedad.  
  
> [!NOTE]  
> Si se publica la tabla para la replicación, debe modificar el esquema mediante la instrucción Transact-SQL [ALTER TABLE](http://msdn.microsoft.com/en-us/f1745145-182d-4301-a334-18f799d361d1) u Objetos de administración de SQL Server (SMO). Si se modifica el esquema mediante el Diseñador de tablas o el Diseñador de diagramas de base de datos, se intentará eliminar la tabla y volver a crearla. No se pueden eliminar objetos publicados, por lo que la modificación del esquema generará un error.  
  
## <a name="options"></a>Opciones  
**Nombre de relación**  
Muestra el nombre de relación.  
  
**Tabla de clave principal**  
Enumera las tablas de la base de datos. Elija la tabla que estará en el lado de la clave principal de la relación.  
  
**Tabla de clave externa**  
Muestra la tabla del lado de la clave externa de la relación. Ésta es la tabla que está actualmente seleccionada en el Diseñador de tablas.  
  
**Cuadrícula debajo de la tabla de clave principal**  
Enumere las columnas de la tabla seleccionada en la lista **Tabla de clave principal** . Especifique las columnas que contribuyen a la clave principal de esa tabla.  
  
**Cuadrícula debajo de la tabla de clave externa**  
Enumere las columnas de la tabla seleccionada en la lista **Tabla de clave externa** . Especifique la columna de clave externa de la tabla de clave externa que corresponde a la columna de clave principal.  
  
> [!NOTE]  
> Las columnas que elija para la clave externa deben tener el mismo tipo de datos que las columnas principales correspondientes. Debe haber un número igual de columnas en cada una de las claves. Por ejemplo, si la clave principal de la tabla en el lado principal de la relación se compone de dos columnas, necesitará hacer coincidir cada una de esas columnas con una columna de la tabla del lado de la clave externa de la relación.  
  
## <a name="see-also"></a>Vea también  
[Cómo crear relaciones entre tablas (Visual Database Tools)](http://msdn.microsoft.com/en-us/867a54b8-5be4-46e6-9702-49ae6dabf67c)  
  

