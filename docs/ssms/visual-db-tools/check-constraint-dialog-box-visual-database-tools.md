---
title: Cuadro de diálogo Restricción CHECK
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.checkconstraint
ms.assetid: ad0bbf7f-b0de-406a-bd0a-cb779816b101
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: 0566d91cb0dfa5e2df23bb2e245a42fdb5bd73df
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "85998933"
---
# <a name="check-constraint-dialog-box-visual-database-tools"></a>Restricción CHECK (cuadro de diálogo, Visual Database Tools)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Este cuadro de diálogo aparece cuando se hace clic con el botón derecho en una cuadrícula de definición de tabla en el Diseñador de tablas y, a continuación, se hace clic en **Restricciones CHECK**. Este cuadro de diálogo contiene un conjunto de propiedades para las restricciones no UNIQUE anexadas a las tablas de la base de datos. Las propiedades que se aplican a las restricciones UNIQUE aparecen en el cuadro de diálogo **Índices o claves** .  
  
> [!NOTE]  
> Si se publica la tabla para la replicación, debe modificar el esquema mediante la instrucción Transact-SQL [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) u Objetos de administración de SQL Server (SMO). Si se modifica el esquema mediante el Diseñador de tablas o el Diseñador de diagramas de base de datos, se intentará eliminar la tabla y volver a crearla. No se pueden eliminar objetos publicados, por lo que la modificación del esquema generará un error.  
  
## <a name="options"></a>Opciones

**Restricciones CHECK seleccionadas**  
Muestra las restricciones CHECK disponibles. Para ver las propiedades de una restricción, seleccione esta restricción en la lista.  
  
**Add (Agregar)**  
Crea una nueva restricción en la tabla de base de datos seleccionada y proporciona el nombre predeterminado y otros valores para la restricción. La restricción no será válida hasta que se especifique una expresión en la restricción.  
  
**Eliminar**  
Elimina la restricción seleccionada de la tabla. Para cancelar la adición de una restricción CHECK, utilice este botón para eliminar la restricción.  
  
**Categoría General**  
Se expande para mostrar el campo de la propiedad **Expresión** .  
  
**Expression**  
Muestra la expresión de la restricción CHECK seleccionada. En las restricciones nuevas, debe especificar la expresión antes de salir del cuadro. También puede editar las restricciones CHECK existentes. Para más información, consulte [Trabajar con restricciones](https://msdn.microsoft.com/637098af-2567-48f8-90f4-b41df059833e).  
  
**Categoría Identidad**  
Se expande para mostrar las propiedades de **Nombre** y **Descripción**.  
  
**Nombre**  
Muestra el nombre de la restricción CHECK seleccionada. Para cambiar el nombre de esta restricción, escriba el texto directamente en el campo de propiedad.  
  
**Descripción**  
Descripción de esta restricción CHECK. Puede editar la descripción si escribe en el campo de la propiedad o puede hacer clic en el botón de puntos suspensivos ( **...** ) que aparece a la derecha del campo de propiedad y editar la descripción en el cuadro de diálogo **Propiedad Description**.  
  
**Categoría Diseñador de tablas**  
Se expande para mostrar las propiedades de **Comprobar datos existentes al crear o al habilitar de nuevo**y **Exigir para INSERTs y UPDATEs**y **Exigir para replicación**.  
  
**Check Existing Data On Creation or Re-Enabling**  
Especifica si todos los datos preexistentes (los existentes en la tabla antes de que se cree la restricción) se comprueban con la restricción.  
  
**Exigir para INSERTs y UPDATEs**  
Especifica si se exigirá la restricción cuando se inserten o se actualicen datos en la tabla.  
  
**Exigir para replicación**  
Indica si se exigirá la restricción cuando un agente de replicación realice una inserción o actualización en esta tabla.  
  
## <a name="see-also"></a>Consulte también

[Trabajar con restricciones](https://msdn.microsoft.com/637098af-2567-48f8-90f4-b41df059833e)
[Índices o claves (cuadro de diálogo, Visual Database Tools)](../../ssms/visual-db-tools/indexes-keys-dialog-box-visual-database-tools.md)
