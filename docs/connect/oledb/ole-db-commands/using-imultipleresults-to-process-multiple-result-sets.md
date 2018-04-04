---
title: Utilizar IMultipleResults para procesar varios conjuntos de resultados | Documentos de Microsoft
description: Utilizar IMultipleResults para procesar resultados múltiples conjuntos de
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- IMultipleResults interface
- multiple-rowset results
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 292b4e9d22d99fcf45e728f0806f4f27f7a5d82f
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2018
---
# <a name="using-imultipleresults-to-process-multiple-result-sets"></a>Utilizar IMultipleResults para procesar varios conjuntos de resultados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Los consumidores utilizan la **IMultipleResults** interfaz para procesar los resultados devueltos por el controlador OLE DB para la ejecución del comando de SQL Server. Cuando el controlador OLE DB para SQL Server envía un comando de ejecución, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ejecuta las instrucciones y devuelve todos los resultados.  
  
 Un cliente debe procesar todos los resultados de la ejecución de comandos. Debido a que el controlador OLE DB para la ejecución del comando de SQL Server puede generar objetos de varios conjuntos de filas como resultado, use la **IMultipleResults** interfaz para asegurarse de que la recuperación de datos de aplicación completa el recorrido de ida iniciada por el cliente.  
  
 El siguiente [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrucción genera varios conjuntos de filas, algunos datos de fila que contiene el **OrderDetails** tabla y otros contienen resultados de la cláusula COMPUTE BY:  
  
```  
SELECT OrderID, FullPrice = (UnitPrice * Quantity), Discount,  
    Discounted = UnitPrice * (1 - Discount) * Quantity  
FROM OrderDetails  
ORDER BY OrderID  
COMPUTE  
    SUM(UnitPrice * Quantity), SUM(UnitPrice * (1 - Discount) * Quantity)  
    BY OrderID  
```  
  
 Si un consumidor ejecuta un comando que contiene este texto y solicita un conjunto de filas como interfaz de resultados devueltos, solo se devuelve el primer conjunto de filas. El consumidor puede procesar todas las filas del conjunto de filas devuelto. Sin embargo, si se establece la propiedad de origen de datos DBPROP_MULTIPLECONNECTIONS en VARIANT_FALSE y MARS no está habilitado en la conexión, no se puede ejecutar ningún otro comando en el objeto de sesión (el controlador OLE DB para SQL Server no creará otra conexión) hasta que el se cancela el comando. Si MARS no está habilitado en la conexión, el controlador OLE DB para SQL Server devuelve un error DB_E_OBJECTOPEN si DBPROP_MULTIPLECONNECTIONS es VARIANT_FALSE y devuelve E_FAIL si hay una transacción activa.  
  
 El controlador OLE DB para SQL Server también devolverá DB_E_OBJECTOPEN al utilizar los parámetros de salida transmitidos y la aplicación no ha consumido todos los valores de parámetro de salida devueltos antes de llamar a **IMultipleResults:: GetResults** a obtener el siguiente conjunto de resultados. Si MARS no está habilitado y si la conexión está ocupada ejecutando un comando que no genera un conjunto de filas o que genera un conjunto de filas que no es un cursor de servidor y si la propiedad del origen de datos DBPROP_MULTIPLECONNECTIONS se establece en VARIANT_TRUE, el controlador OLE DB para SQL Server crea conexiones adicionales para admitir objetos de comando simultáneos, a menos que una transacción está activa, en cuyo caso devuelve un error. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] administra las transacciones y el bloqueo para cada conexión. Si se genera una segunda conexión, los comandos de cada una de las conexiones no comparten los bloqueos. Hay que tener cuidado para asegurarse de que un comando no bloquee otro comando manteniendo bloqueos en filas solicitadas por el otro comando. Si MARS está habilitado, puede haber varios comandos activos en las conexiones y si se utilizan transacciones explícitas, todos los comandos comparten una transacción común.  
  
 El consumidor puede cancelar el comando mediante [issabort:: Abort](../../oledb/ole-db-interfaces/issabort-abort-ole-db.md) o liberando todas las referencias que se mantienen en el objeto de comando y el conjunto de filas derivado.  
  
 Usar **IMultipleResults** en todas las instancias, el consumidor puede obtener todos los conjuntos de filas generados mediante la ejecución de comandos y permite que los consumidores determinar apropiadamente cuándo se debe cancelar la ejecución de comandos y liberar un objeto de sesión para su uso con otros comandos.  
  
> [!NOTE]  
>  Si se utilizan cursores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], la ejecución de comandos crea el cursor. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] indica si la creación del cursor se ha llevado a cabo correctamente o no; por consiguiente, el viaje de ida y vuelta (round trip) a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se completa cuando se obtiene el resultado de la ejecución del comando. Cada **GetNextRows** llamada, a continuación, se convierte en un de ida y vuelta. De esta manera, pueden existir varios objetos de comando activos, y cada uno de ellos procesará un conjunto de filas que es el resultado de una captura del cursor de servidor. Para obtener más información, consulte [conjuntos de filas y cursores de servidor SQL](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md).  
  
## <a name="see-also"></a>Vea también  
 [Comandos](../../oledb/ole-db-commands/commands.md)  
  
  
