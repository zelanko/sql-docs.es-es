---
title: Cuadro de diálogo Restricción CHECK (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.checkconstraint
ms.assetid: ad0bbf7f-b0de-406a-bd0a-cb779816b101
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d41cc9f3b52c0c5e70ead6b93c0b929ef521f673
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63067461"
---
# <a name="check-constraint-dialog-box-visual-database-tools"></a>Restricción CHECK (cuadro de diálogo, Visual Database Tools)
  Este cuadro de diálogo aparece cuando hace clic con el botón secundario en una cuadrícula de definición de tabla en Diseñador de tablas y hace clic en **restricciones check**. Este cuadro de diálogo contiene un conjunto de propiedades para las restricciones no UNIQUE anexadas a las tablas de la base de datos. Las propiedades que se aplican a las restricciones UNIQUE aparecen en el cuadro de diálogo **Índices o claves** .  
  
> [!NOTE]  
>  Si se publica la tabla para la replicación, debe modificar el esquema mediante la instrucción Transact-SQL [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) u Objetos de administración de SQL Server (SMO). Si se modifica el esquema mediante el Diseñador de tablas o el Diseñador de diagramas de base de datos, se intentará eliminar la tabla y volver a crearla. No se pueden eliminar objetos publicados, por lo que la modificación del esquema generará un error.  
  
## <a name="options"></a>Opciones  
 **Restricciones check seleccionadas**  
 Muestra las restricciones CHECK disponibles. Para ver las propiedades de una restricción, seleccione esta restricción en la lista.  
  
 **Add (Agregar)**  
 Crea una nueva restricción en la tabla de base de datos seleccionada y proporciona el nombre predeterminado y otros valores para la restricción. La restricción no será válida hasta que se especifique una expresión en la restricción.  
  
 **Eliminar**  
 Elimina la restricción seleccionada de la tabla. Para cancelar la adición de una restricción CHECK, utilice este botón para eliminar la restricción.  
  
 **Categoría General**  
 Se expande para mostrar el campo de la propiedad **Expresión** .  
  
 **Expression**  
 Muestra la expresión de la restricción CHECK seleccionada. En las restricciones nuevas, debe especificar la expresión antes de salir del cuadro. También puede editar las restricciones CHECK existentes. Para más información, consulte [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md).  
  
 **Categoría Identidad**  
 Se expande para mostrar las propiedades de **Nombre** y **Descripción**.  
  
 **Nombre**  
 Muestra el nombre de la restricción CHECK seleccionada. Para cambiar el nombre de esta restricción, escriba el texto directamente en el campo de propiedad.  
  
 **Descripción**  
 Descripción de esta restricción CHECK. Puede editar la descripción si escribe en el campo de la propiedad o puede hacer clic en el botón de puntos suspensivos (**...**) que aparece a la derecha del campo de propiedad y editar la descripción en el cuadro de diálogo **Propiedad Description**.  
  
 **Categoría Diseñador de tablas**  
 Se expande para mostrar las propiedades de **Comprobar datos existentes al crear o al habilitar de nuevo**y **Exigir para INSERTs y UPDATEs**y **Exigir para replicación**.  
  
 **Comprobar los datos existentes al crear o al habilitar de nuevo**  
 Especifica si todos los datos preexistentes (los existentes en la tabla antes de que se cree la restricción) se comprueban con la restricción.  
  
 **Exigir para inserciones y actualizaciones**  
 Especifica si se exigirá la restricción cuando se inserten o se actualicen datos en la tabla.  
  
 **Exigir para replicación**  
 Indica si se exigirá la restricción cuando un agente de replicación realice una inserción o actualización en esta tabla.  
  
## <a name="see-also"></a>Consulte también  
 [Restricciones UNIQUE y restricciones check](../../relational-databases/tables/unique-constraints-and-check-constraints.md)   
 [Cuadro de diálogo índices y claves &#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
  
