---
title: Visor de conflictos de replicación (combinación)
description: Describe el visor de conflictos de replicación utilizado para la replicación de combinación en SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.replconflictviewer.cvmerge.f1
ms.assetid: bfef5e21-ac04-4bc5-a55e-595421e34923
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2e10e89850c8028590fd9e498a062abe0ac0de06
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868236"
---
# <a name="microsoft-replication-conflict-viewer-merge-replication"></a>Visor de conflictos de replicación de Microsoft (Replicación de mezcla)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  El Visor de conflictos de replicación le permite ver los conflictos que hayan podido producirse durante la sincronización de la replicación. Los conflictos ocurren cuando los mismos datos se modifican en dos servidores diferentes, por ejemplo, en un publicador y en un suscriptor, o en dos suscriptores diferentes. La replicación soluciona automáticamente los conflictos mediante el solucionador de conflictos seleccionado durante la creación del artículo. Sin embargo, el Visor de conflictos de replicación le permite elegir una resolución diferente para el conflicto si fuese necesario. Pueden producirse los siguientes conflictos:  
  
-   Conflictos de actualización. Los conflictos de actualización se producen cuando se modifican los mismos datos en dos ubicaciones. Una de las modificaciones "gana", mientras que la otra "pierde". Existe la opción de mantener los datos existentes (los datos que ganan), sobrescribir los datos existentes con los datos con los que se produce el conflicto (los datos que pierden) o mezclar los datos que ganan y los que pierden para actualizar los datos existentes.  
  
-   Conflictos de inserción. Los conflictos de inserción se producen al insertar una fila en una ubicación que infringe alguna regla de coherencia de datos al mezclarse con cambios en otras ubicaciones. Existe la opción de mantener los datos existentes (los datos que ganan), sobrescribir los datos existentes con los datos con los que se produce el conflicto (los datos que pierden) o mezclar los datos que ganan y los que pierden para actualizar los datos existentes.  
  
-   Conflictos de eliminación. Ocurren cuando se elimina una fila en una ubicación y se modifica la misma fila en otra.  
  
 Mientras se resuelven los conflictos durante la sincronización, los datos de la fila que pierde se escriben en una tabla de conflictos. Tanto si acepta la resolución original como si elige una resolución distinta para el conflicto, la fila de conflicto registrada se eliminará de la tabla de conflictos. Se recomienda revisar los conflictos de forma habitual con el fin de reducir el tamaño de las tablas de seguimiento de conflictos.  
  
> [!NOTE]  
>  Los conflictos que implican registros lógicos no se muestran en el Visor de conflictos. Para ver información acerca de estos conflictos, utilice procedimientos almacenados de replicación. Para obtener más información, vea [Ver información de conflictos para publicaciones de mezcla &#40;programación de la replicación con Transact-SQL&#41;](./view-and-resolve-data-conflicts-for-merge-publications.md).  
  
## <a name="options"></a>Opciones  
 El Visor de conflictos de replicación está dividido en dos secciones. La sección superior del cuadro de diálogo muestra la lista de conflictos de la tabla seleccionada. Si hace clic en un elemento de la lista de conflictos, se mostrarán los detalles del conflicto en la sección inferior del cuadro de diálogo.  
  
 La información que describe las causas del conflicto (por ejemplo, que la misma fila se actualizó tanto en el publicador como en el suscriptor) se muestra en la sección inferior del cuadro de diálogo. Los datos del conflicto de la sección inferior se muestran en las dos columnas correspondientes (**Ganador del conflicto** y **Perdedor del conflicto**). Si el conflicto se produce entre datos actualizados y eliminados, es posible que no haya datos que mostrar en el lado eliminado del conflicto. En este caso, el Visor de conflictos de replicación muestra un mensaje en una de las columnas en el que indica que se eliminó la fila en una ubicación y se actualizó en otra. También indica la resolución recomendada.  
  
 Los datos que no se pueden editar en el Visor de conflictos de replicación (por ejemplo, los datos **rowguid** ) se muestran como datos de solo lectura con el cuadro sombreado.  
  
 **Base de datos**  
 Elija una base de datos que contenga publicaciones con conflictos.  
  
 **Publicación**  
 Elija una publicación que contenga tablas con conflictos.  
  
 **Table**  
 Elija una tabla que contenga conflictos.  
  
 **Definir filtro**  
 Haga clic para abrir el cuadro de diálogo **Definir filtros** .  
  
 **Aplicar o quitar filtro**  
 Haga clic para aplicar o quitar un filtro definido en el cuadro de diálogo **Definir filtros** .  
  
 **Seleccionar todo**  
 Haga clic para seleccionar todos los conflictos mostrados en la cuadrícula.  
  
 **No seleccionar nada**  
 Haga clic para anular la selección de todos los conflictos mostrados en la cuadrícula.  
  
 **Remove**  
 Haga clic en esta opción para quitar los conflictos seleccionados del visor y los metadatos asociados de las tablas del sistema de replicación. Es equivalente a hacer clic en el botón Enviar ganador (sin realizar cambios en los datos) para cada conflicto seleccionado.  
  
 **Mostrar todas las columnas**  
 Seleccione esta opción para mostrar todas las columnas de la tabla.  
  
 **Mostrar las primeras cinco columnas y el resto de las columnas con datos en conflicto**  
 Seleccione esta opción para mostrar las cinco primeras columnas y otras columnas con conflictos. Resulta útil si las tablas presentan un número elevado de columnas y solo desea ver las columnas más importantes para solucionar el conflicto. Las cinco primeras columnas se incluyen en esta vista, como campos que identifican una fila, como la clave principal o campos de nombre, que con frecuencia se encuentran entre las cinco primeras columnas de la tabla.  
  
 **Mostrar información de columna** ( **…** )  
 Haga clic para ver la información de la columna: **Nombre de tabla**, **Nombre de columna**, **Tipo de datos**y **Valor de columna**. Es posible editar**Valor de columna** excepto en el caso de que el valor se muestre como de solo lectura.  
  
 **Enviar ganador**  
 Haga clic en esta opción para conservar la fila que el solucionador de conflictos determinó ser la ganadora. Es posible cambiar el valor de las columnas que no se muestran como de solo lectura antes de hacer clic en este botón.  
  
 **Enviar perdedor**  
 Haga clic en esta opción para aceptar la fila que el solucionador de conflictos determinó ser la perdedora. Es posible cambiar el valor de las columnas que no se muestran como de solo lectura antes de hacer clic en este botón.  
  
 **Registrar los detalles de este conflicto**  
 Active esta casilla para registrar los detalles del conflicto en un archivo. Para especificar la ubicación del archivo, señale el menú **Ver** y haga clic en **Opciones**. Escriba un valor o haga clic en el botón de búsqueda ( **...** ) y navegue hasta encontrar el archivo adecuado. Haga clic en **Aceptar** para salir del cuadro de diálogo **Opciones** .  
  
## <a name="see-also"></a>Consulte también  
 [Ver y resolver conflictos de datos para publicaciones de mezcla &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)   
 [Replicación de mezcla avanzada: detección y resolución de conflictos](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
