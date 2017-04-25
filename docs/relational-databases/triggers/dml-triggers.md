---
title: Desencadenadores DML | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-dml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- triggers [SQL Server], about triggers
- DML triggers, about DML triggers
- triggers [SQL Server]
ms.assetid: 298eafca-e01f-4707-8c29-c75546fcd6b0
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 49e88050bea0405d8801a5b53faafcb644a6b62d
ms.lasthandoff: 04/11/2017

---
# <a name="dml-triggers"></a>Desencadenadores DML
  Los desencadenadores DML constituyen un tipo especial de procedimiento almacenado que se inicia automáticamente cuando tiene lugar un evento de lenguaje de manipulación de datos (DML) que afecta a la tabla o la vista definida en el desencadenador. Los eventos DML incluyen las instrucciones INSERT, UPDATE o DELETE. Los desencadenadores DML pueden usarse para aplicar reglas de negocios y la integridad de datos, consultar otras tablas e incluir instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] complejas. El desencadenador y la instrucción que lo activa se tratan como una sola transacción, que puede revertirse desde el desencadenador. Si se detecta un error grave (por ejemplo, no hay suficiente espacio en disco), se revierte automáticamente toda la transacción.  
  
## <a name="dml-trigger-benefits"></a>Ventajas de los desencadenadores DML  
 Los desencadenadores DML se parecen a las restricciones en que pueden aplicar la integridad de entidad o de dominio. En general, la integridad de entidad se debe exigir siempre en el nivel más bajo mediante índices que formen parte de las restricciones PRIMARY KEY y UNIQUE o que se creen independientemente de las restricciones. La integridad de dominio se debe aplicar con restricciones CHECK y la integridad referencial (RI) se debe aplicar a las restricciones de FOREIGN KEY. Los desencadenadores DML resultan de especial utilidad cuando las características permitidas por las restricciones no cubren las necesidades funcionales de la aplicación.  
  
 En la lista siguiente se comparan los desencadenadores DML con restricciones y se identifica cuándo los desencadenadores DML tienen ventaja.  
  
-   Los desencadenadores DML pueden realizar cambios en cascada mediante tablas relacionadas de la base de datos; sin embargo, estos cambios pueden ejecutarse de manera más eficaz con restricciones de integridad referencial en cascada. Las restricciones FOREIGN KEY solo pueden validar un valor de columna si coinciden exactamente con un valor de otra columna, a menos que la cláusula REFERENCES defina una acción referencial en cascada.  
  
-   Pueden proteger contra operaciones INSERT, UPDATE y DELETE incorrectas o malintencionadas, y exigir otras restricciones que sean más complejas que las definidas con restricciones CHECK.  
  
     A diferencia de éstas, los desencadenadores DML pueden hacer referencia a columnas de otras tablas. Por ejemplo, un desencadenador puede utilizar una instrucción SELECT de otra tabla para comparar con los datos insertados o actualizados y para realizar acciones adicionales, como modificar los datos o mostrar un mensaje de error definido por el usuario.  
  
-   Pueden evaluar el estado de una tabla antes y después de realizar una modificación de datos y actuar en función de esa diferencia.  
  
-   Varios desencadenadores DML del mismo tipo (INSERT, UPDATE o DELETE) en una tabla permiten realizar distintas acciones en respuesta a una misma instrucción de modificación.  
  
-   Las restricciones solo pueden comunicar la existencia de errores mediante mensajes de error estándar del sistema. Si la aplicación necesita o puede aprovechar mensajes personalizados y un control de errores más complejo, deberá usar un desencadenador.  
  
-   Los desencadenadores DML pueden impedir o revertir los cambios que infrinjan la integridad referencial y cancelar, de ese modo, cualquier intento de modificación de los datos. Ese tipo de desencadenador puede activarse cuando se cambia una clave externa y el nuevo valor no coincide con su clave principal. No obstante, para estos casos suelen utilizarse restricciones FOREIGN KEY.  
  
-   Si hay restricciones en la tabla de desencadenadores, se comprobarán después de la ejecución del desencadenador INSTEAD OF, pero antes de la ejecución del desencadenador AFTER. Si se infringen las restricciones, se revertirán las acciones del desencadenador INSTEAD OF y no se ejecutará el desencadenador AFTER.  
  
## <a name="types-of-dml-triggers"></a>Tipos de desencadenadores DML  
 Desencadenador AFTER  
 Los desencadenadores AFTER se ejecutan después de llevar a cabo una acción de las instrucciones INSERT, UPDATE, MERGE o DELETE. Los desencadenadores AFTER no se ejecutan nunca si se produce una infracción de restricción; por tanto, no se puede usar estos desencadenadores para ningún procesamiento que pueda impedir infracciones de restricciones. Para cada acción INSERT, UPDATE o DELETE especificada en una instrucción MERGE, se activa el desencadenador correspondiente para cada operación DML.  
  
 Desencadenador INSTEAD OF  
 Los desencadenadores INSTEAD OF pasan por alto las acciones estándar de la instrucción de desencadenamiento. Por lo tanto, se pueden usar para realizar comprobación de errores o valores en una o más columnas y, a continuación, realizar acciones adicionales antes de insertar, actualizar o eliminar la fila o las filas. Por ejemplo, cuando el valor que se actualiza en una columna de tarifa de una hora de trabajo de una tabla de nómina supera un valor específico, se puede definir un desencadenador para producir un error y revertir la transacción, o insertar un nuevo registro en un registro de auditoría antes de insertar el registro en la tabla de nómina. La principal ventaja de los desencadenadores INSTEAD OF es que habilitan las vistas que no serían actualizables para admitir actualizaciones. Por ejemplo, las vistas que contengan varias tablas base deben usar un desencadenador INSTEAD OF para permitir inserciones, actualizaciones y eliminaciones que hagan referencia a datos de más de una tabla. Otra ventaja de los desencadenadores INSTEAD OF es que permiten codificar la lógica para rechazar partes de un lote y, al mismo tiempo, aceptar otras partes del mismo.  
  
 En la tabla siguiente se compara la funcionalidad de los desencadenadores AFTER e INSTEAD OF.  
  
|Función|Desencadenador AFTER|Desencadenador INSTEAD OF|  
|--------------|-------------------|------------------------|  
|Aplicabilidad|Tablas|Tablas y vistas|  
|Cantidad por tabla o vista|Varios por cada acción de desencadenamiento (UPDATE, DELETE y INSERT)|Uno por cada acción de desencadenamiento (UPDATE, DELETE y INSERT)|  
|Referencias en cascada|No se aplica ninguna restricción|No se permiten los desencadenadores INSTEAD OF UPDATE y DELETE en tablas que son destino de las restricciones de integridad referencial en cascada|  
|Ejecución|Después:<br /><br /> Procesamiento de restricciones<br /><br /> Acciones de integridad referencial declarativa<br /><br /> Creación de tablas**inserted** y **deleted** <br /><br /> La acción de desencadenamiento|Antes: Procesamiento de restricciones<br /><br /> En lugar de: La acción de desencadenamiento<br /><br /> Después: Creación de tablas  **inserted** y **deleted**|  
|Orden de la ejecución|Se puede especificar la primera y la última ejecución|No aplicable|  
|Referencias a columnas**varchar(max)**, **nvarchar(max)**y **varbinary(max)** en tablas **inserted** y **deleted** |Permitido|Permitido|  
|Referencias a columnas**text**, **ntext**y **image** en las tablas **inserted** y **deleted** |No permitido|Permitido|  
  
 Desencadenadores CLR  
 Un desencadenador CLR puede ser un desencadenador AFTER o INSTEAD OF. Un desencadenador CLR también puede ser un desencadenador DDL. En lugar de ejecutar un procedimiento almacenado [!INCLUDE[tsql](../../includes/tsql-md.md)] , un desencadenador CLR ejecuta uno o más métodos escritos en código administrado que son miembros de un ensamblado creado en .NET Framework y cargado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="related-tasks"></a>Tareas relacionadas  
  
|Tarea|Tema|  
|----------|-----------|  
|Describe cómo crear un desencadenador DML.|[Crear desencadenadores DML](../../relational-databases/triggers/create-dml-triggers.md)|  
|Describe cómo crear un desencadenador CLR.|[Crear desencadenadores CLR](../../relational-databases/triggers/create-clr-triggers.md)|  
|Describe cómo crear un desencadenador DML para administrar las modificaciones de datos en una sola fila o en múltiples filas.|[Crear desencadenadores DML para administrar varias filas de datos](../../relational-databases/triggers/create-dml-triggers-to-handle-multiple-rows-of-data.md)|  
|Describe cómo anidar desencadenadores.|[Crear desencadenadores anidados](../../relational-databases/triggers/create-nested-triggers.md)|  
|Describe cómo especificar el orden en el que se activan los desencadenadores AFTER.|[Especificar el primer y el último desencadenador](../../relational-databases/triggers/specify-first-and-last-triggers.md)|  
|Describe cómo usar las tablas inserted y delete especiales en código del desencadenador.|[Usar las tablas insertadas y eliminadas](../../relational-databases/triggers/use-the-inserted-and-deleted-tables.md)|  
|Describe cómo modificar o cambiar el nombre de un desencadenador DML.|[Modificar o cambiar el nombre de desencadenadores DML](../../relational-databases/triggers/modify-or-rename-dml-triggers.md)|  
|Describe cómo ver información acerca de los desencadenadores DML.|[Obtener información acerca de los desencadenadores DML](../../relational-databases/triggers/get-information-about-dml-triggers.md)|  
|Describe cómo eliminar o deshabilitar los desencadenadores DML.|[Eliminar o deshabilitar desencadenadores DML](../../relational-databases/triggers/delete-or-disable-dml-triggers.md)|  
|Describe cómo administrar la seguridad de los desencadenadores.|[Administrar la seguridad de los desencadenadores](../../relational-databases/triggers/manage-trigger-security.md)|  
  
## <a name="see-also"></a>Vea también  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [Funciones de desencadenador &#40;Transact-SQL&#41;](../../t-sql/functions/trigger-functions-transact-sql.md)  
  
  
