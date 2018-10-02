---
title: 'Cómo: Corregir errores | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 0d504e00-4ff0-4fdf-b874-85280bbd8668
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6d1f2fba2b5c2c0f978973eb015674b9b83af806
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47664023"
---
# <a name="how-to-fix-errors"></a>Cómo: Corregir errores
El panel Lista de errores muestra todos los errores de implementación o de compilación. Los errores de sintaxis y semánticos producidos por la edición en el Editor de Transact\-SQL o en el Diseñador de tablas también aparecen en la lista al editar entidades de base de datos y sus definiciones. La Lista de errores se actualiza dinámicamente a medida que se editan scripts en distintas pestañas. Después, puede seguir los errores identificados para la solución de problemas.  
  
> [!WARNING]  
> Los procedimientos siguientes usan entidades creadas en procedimientos de las secciones [Desarrollo de bases de datos conectadas](../ssdt/connected-database-development.md) y [Desarrollo de bases de datos sin conexión orientado a proyectos](../ssdt/project-oriented-offline-database-development.md).  
  
### <a name="to-fix-errors"></a>Para corregir errores  
  
1.  Haga clic con el botón derecho en la tabla **Producto** (Product.sql) en el **Explorador de soluciones** y seleccione **Diseñador de vistas**.  
  
2.  En la cuadrícula de columnas del diseñador, haga clic con el botón derecho en la columna **ShelflLife** y seleccione **Eliminar** para eliminar esta columna de la tabla.  
  
3.  Observe que en el panel **Lista de errores** de la parte inferior de la pantalla aparecen inmediatamente una advertencia y un error similares a los siguientes.  
  
**Advertencia SQL71502: Función: [dbo].[GetProductsBySupplier] contiene una referencia sin resolver a un objeto. El objeto no existe o la referencia es ambigua porque podría referirse a cualquiera de los siguientes objetos: [dbo].[Product].[p]::[ShelfLife] o [dbo].[Product].[ShelfLife]. Error SQL71501: Restricción CHECK: [dbo].[CK_Product_ShelfLife] contiene una referencia sin resolver a un objeto [dbo].[Product].[ShelfLife].**  
  
4.  Puede hacer clic con el botón derecho en la **Lista de errores** y usar los menús contextuales para ordenar los resultados, filtrar las entradas que desea mostrar e indicar qué columnas de información desea que aparezcan para cada entrada.  
  
    Haga doble clic en la primera advertencia identificada y sígala hacia el archivo de script que generó dicha advertencia. La sección de código que tiene el problema aparecerá resaltada. En el ejemplo, se debe a que tanto una instrucción `SELECT` como una instrucción `RETURN` de una función con valores de tabla que se creó previamente usan la columna `ShelfLife`.  
  
5.  En el Editor de Transact\-SQL, quite `ShelfLife` de la función.  
  
6.  Corrija el segundo error de manera similar quitando la restricción CHECK.  
  
7.  Observe que la advertencia y el error desaparecerán de la **Lista de errores** inmediatamente después de corregir los problemas.  
  
## <a name="see-also"></a>Ver también  
[Usar el Editor de Transact-SQL para editar y ejecutar scripts](../ssdt/use-transact-sql-editor-to-edit-and-execute-scripts.md)  
  
