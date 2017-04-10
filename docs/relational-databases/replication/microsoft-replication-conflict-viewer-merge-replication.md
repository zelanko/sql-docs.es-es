---
title: "Visor de conflictos de replicaci&#243;n de Microsoft (Replicaci&#243;n de mezcla) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.replconflictviewer.cvmerge.f1"
ms.assetid: bfef5e21-ac04-4bc5-a55e-595421e34923
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# Visor de conflictos de replicaci&#243;n de Microsoft (Replicaci&#243;n de mezcla)
  El Visor de conflictos de replicación le permite ver los conflictos que hayan podido producirse durante la sincronización de la replicación. Los conflictos ocurren cuando los mismos datos se modifican en dos servidores diferentes, por ejemplo, en un publicador y en un suscriptor, o en dos suscriptores diferentes. La replicación soluciona automáticamente los conflictos mediante el solucionador de conflictos seleccionado durante la creación del artículo. Sin embargo, el Visor de conflictos de replicación le permite elegir una resolución diferente para el conflicto si fuese necesario. Pueden producirse los siguientes conflictos:  
  
-   Conflictos de actualización. Los conflictos de actualización se producen cuando se modifican los mismos datos en dos ubicaciones. Una de las modificaciones "gana", mientras que la otra "pierde". Existe la opción de mantener los datos existentes (los datos que ganan), sobrescribir los datos existentes con los datos con los que se produce el conflicto (los datos que pierden) o mezclar los datos que ganan y los que pierden para actualizar los datos existentes.  
  
-   Conflictos de inserción. Los conflictos de inserción se producen al insertar una fila en una ubicación que infringe alguna regla de coherencia de datos al mezclarse con cambios en otras ubicaciones. Existe la opción de mantener los datos existentes (los datos que ganan), sobrescribir los datos existentes con los datos con los que se produce el conflicto (los datos que pierden) o mezclar los datos que ganan y los que pierden para actualizar los datos existentes.  
  
-   Conflictos de eliminación. Ocurren cuando se elimina una fila en una ubicación y se modifica la misma fila en otra.  
  
 Mientras se resuelven los conflictos durante la sincronización, los datos de la fila que pierde se escriben en una tabla de conflictos. Tanto si acepta la resolución original como si elige una resolución distinta para el conflicto, la fila de conflicto registrada se eliminará de la tabla de conflictos. Se recomienda revisar los conflictos de forma habitual con el fin de reducir el tamaño de las tablas de seguimiento de conflictos.  
  
> [!NOTE]  
>  Los conflictos que implican registros lógicos no se muestran en el Visor de conflictos. Para ver información acerca de estos conflictos, utilice procedimientos almacenados de replicación. Para obtener más información, consulte [Ver la información de conflictos para publicaciones de mezcla & #40; Programación de replicación Transact-SQL & #41;](../../relational-databases/replication/view conflict information for merge publications.md).  
  
## Opciones  
 El Visor de conflictos de replicación está dividido en dos secciones. La sección superior del cuadro de diálogo muestra la lista de conflictos de la tabla seleccionada. Si hace clic en un elemento de la lista de conflictos, se mostrarán los detalles del conflicto en la sección inferior del cuadro de diálogo.  
  
 La información que describe las causas del conflicto (por ejemplo, que la misma fila se actualizó tanto en el publicador como en el suscriptor) se muestra en la sección inferior del cuadro de diálogo. Los datos del conflicto en la sección inferior se muestran en dos columnas correspondientes (**ganador del conflicto** y **perdedor del conflicto**). Si el conflicto se produce entre datos actualizados y eliminados, es posible que no haya datos que mostrar en el lado eliminado del conflicto. En este caso, el Visor de conflictos de replicación muestra un mensaje en una de las columnas en el que indica que se eliminó la fila en una ubicación y se actualizó en otra. También indica la resolución recomendada.  
  
 Datos que no se puede editar en el Visor de conflictos de replicación (por ejemplo, **rowguid** datos) con el cuadro sombreado aparece como de solo lectura.  
  
 **Base de datos**  
 Elija una base de datos que contenga publicaciones con conflictos.  
  
 **Publicación**  
 Elija una publicación que contenga tablas con conflictos.  
  
 **Tabla**  
 Elija una tabla que contenga conflictos.  
  
 **Definir filtro**  
 Haga clic para abrir el **definir filtros** cuadro de diálogo.  
  
 **Aplicar o quitar filtro**  
 Haga clic para aplicar o quitar un filtro que se ha definido en el **definir filtros** cuadro de diálogo.  
  
 **Seleccionar todo**  
 Haga clic para seleccionar todos los conflictos mostrados en la cuadrícula.  
  
 **No seleccionar nada**  
 Haga clic para anular la selección de todos los conflictos mostrados en la cuadrícula.  
  
 **Quitar**  
 Haga clic en esta opción para quitar los conflictos seleccionados del visor y los metadatos asociados de las tablas del sistema de replicación. Es equivalente a hacer clic en el botón Enviar ganador (sin realizar cambios en los datos) para cada conflicto seleccionado.  
  
 **Mostrar todas las columnas**  
 Seleccione esta opción para mostrar todas las columnas de la tabla.  
  
 **Mostrar las primeras cinco columnas y el resto de las columnas con datos en conflicto**  
 Seleccione esta opción para mostrar las cinco primeras columnas y otras columnas con conflictos. Resulta útil si las tablas presentan un número elevado de columnas y solo desea ver las columnas más importantes para solucionar el conflicto. Las cinco primeras columnas se incluyen en esta vista, como campos que identifican una fila, como la clave principal o campos de nombre, que con frecuencia se encuentran entre las cinco primeras columnas de la tabla.  
  
 **Mostrar información de la columna** (**...**)  
 Haga clic para ver la información de la columna: **Nombre de tabla**, **Nombre de columna**, **Tipo de datos**y **Valor de columna**. **Valor de la columna** es editable, a menos que el valor se muestra como de solo lectura.  
  
 **Enviar ganador**  
 Haga clic en esta opción para conservar la fila que el solucionador de conflictos determinó ser la ganadora. Es posible cambiar el valor de las columnas que no se muestran como de solo lectura antes de hacer clic en este botón.  
  
 **Enviar perdedor**  
 Haga clic en esta opción para aceptar la fila que el solucionador de conflictos determinó ser la perdedora. Es posible cambiar el valor de las columnas que no se muestran como de solo lectura antes de hacer clic en este botón.  
  
 **Registrar los detalles de este conflicto**  
 Active esta casilla para registrar los detalles del conflicto en un archivo. Para especificar la ubicación del archivo, señale el menú **Ver** y haga clic en **Opciones**. Escriba un valor o haga clic en el (**...**) y navegue hasta el archivo apropiado. Haga clic en **Aceptar** para salir del cuadro de diálogo **Opciones** .  
  
## Vea también  
 [Ver y resolver conflictos de datos de publicaciones de mezcla & #40; SQL Server Management Studio & #41;](../../relational-databases/replication/view and resolve data conflicts for merge publications.md)   
 [Detección y resolución de conflictos de replicación de mezcla avanzada](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  