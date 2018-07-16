---
title: Editor de la tarea de inserción (página Opciones) de forma masiva | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.bulkinserttask.options.f1
helpviewer_keywords:
- Bulk Insert Task Editor
ms.assetid: b3702811-3eb8-4b28-9190-5ae7a1a7bb6f
caps.latest.revision: 31
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b878f48473e70d61f6de2a02c9268eb4fc91f0ec
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37326215"
---
# <a name="bulk-insert-task-editor-options-page"></a>Editor de la tarea Inserción masiva (página Opciones)
  Use la página **Opciones** del cuadro de diálogo **Editor de la tarea Inserción masiva** para establecer las propiedades de la operación de inserción masiva. La tarea Inserción masiva copia gran cantidad de datos en una tabla o vista de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 Para más información sobre las inserciones masivas, vea [Tarea Inserción masiva](control-flow/bulk-insert-task.md) y [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql).  
  
## <a name="options"></a>Opciones  
 **CodePage**  
 Especifique la página de códigos de los datos incluidos en el archivo de datos.  
  
 **DataFileType**  
 Especifique el valor del tipo de datos que desea utilizar en la operación de carga.  
  
 **BatchSize**  
 Especifique el número de filas de un lote. El valor predeterminado es todo el archivo de datos. Si establece el valor cero en **BatchSize** , se cargarán los datos en un único lote.  
  
 **LastRow**  
 Especifique la última fila que desea copiar.  
  
 **FirstRow**  
 Especifique la primera fila desde la que desea empezar a copiar.  
  
 **Opciones**  
 |Término|Definición|  
|----------|----------------|  
|**Restricciones CHECK**|Seleccione esta opción para comprobar las restricciones de la tabla y de la columna.|  
|**Mantener valores NULL**|Seleccione esta opción para conservar los valores NULL durante la operación de inserción masiva, en lugar de insertar valores predeterminados en las columnas vacías.|  
|**Habilitar la inserción de identidad**|Seleccione esta opción para insertar valores existentes en una columna de identidad.|  
|**Bloqueo de tabla**|Seleccione esta opción para bloquear la tabla durante la inserción masiva.|  
|**Activar desencadenadores**|Seleccione esta opción para activar desencadenadores de inserción, actualización o eliminación en la tabla.|  
  
 **SortedData**  
 Especifique la cláusula ORDER BY en la instrucción de inserción masiva. El nombre de columna que proporcione debe ser una columna válida de la tabla de destino. El valor predeterminado es `false`. Significa que los datos están ordenados mediante una cláusula ORDER BY.  
  
 **MaxErrors**  
 Especifique el número máximo de errores que pueden producirse antes de que se cancele la operación de inserción masiva. El valor 0 indica que se permite un número infinito de errores.  
  
> [!NOTE]  
>  Cada fila que no pueda importarse con la operación de carga masiva se contabilizará como un error.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de la tarea de inserción de forma masiva &#40;página General&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor de la tarea de inserción de forma masiva &#40;página de conexión&#41;](../../2014/integration-services/bulk-insert-task-editor-connection-page.md)   
 [Página expresiones](expressions/expressions-page.md)   
 [Flujo de control](control-flow/control-flow.md)  
  
  
