---
title: Utilizar IMultipleResults para procesar varios conjuntos de resultados | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-commands
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- IMultipleResults interface
- multiple-rowset results
ms.assetid: 754d3f30-7d94-4b67-8dac-baf2699ce9c6
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6a3d352a423a810dfda61d29b4b595e11cddd9e9
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="using-imultipleresults-to-process-multiple-result-sets"></a>Utilizar IMultipleResults para procesar varios conjuntos de resultados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Los consumidores utilizan la **IMultipleResults** interfaz para procesar los resultados devueltos por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecución de comando del proveedor OLE DB de Native Client. Cuando el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client envía un comando de ejecución, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecuta las instrucciones y devuelve todos los resultados.  
  
 Un cliente debe procesar todos los resultados de la ejecución de comandos. Dado que la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecución de comando del proveedor OLE DB de Native Client puede generar objetos de varios conjuntos de filas como resultado, use la **IMultipleResults** interfaz para asegurarse de que se complete la recuperación de datos de aplicación el iniciada por el cliente de ida y vuelta.  
  
 El siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción genera varios conjuntos de filas, algunos datos de fila que contiene el **OrderDetails** tabla y otros contienen resultados de la cláusula COMPUTE BY:  
  
```  
SELECT OrderID, FullPrice = (UnitPrice * Quantity), Discount,  
    Discounted = UnitPrice * (1 - Discount) * Quantity  
FROM OrderDetails  
ORDER BY OrderID  
COMPUTE  
    SUM(UnitPrice * Quantity), SUM(UnitPrice * (1 - Discount) * Quantity)  
    BY OrderID  
```  
  
 Si un consumidor ejecuta un comando que contiene este texto y solicita un conjunto de filas como interfaz de resultados devueltos, solo se devuelve el primer conjunto de filas. El consumidor puede procesar todas las filas del conjunto de filas devuelto. Sin embargo, si se establece la propiedad de origen de datos DBPROP_MULTIPLECONNECTIONS en VARIANT_FALSE y MARS no está habilitado en la conexión, no se puede ejecutar ningún otro comando en el objeto de sesión (la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client no creará otra conexión) hasta que se cancela el comando. Si MARS no está habilitado en la conexión, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB devuelve un error DB_E_OBJECTOPEN si DBPROP_MULTIPLECONNECTIONS es VARIANT_FALSE y devuelve E_FAIL si hay una transacción activa.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client también devolverá DB_E_OBJECTOPEN al utilizar los parámetros de salida transmitidos y la aplicación no ha consumido todos los valores de parámetro de salida devueltos antes de llamar a **IMultipleResults:: GetResults**  para obtener el siguiente conjunto de resultados. Si MARS no está habilitado y la conexión está ocupada ejecutando un comando que no genera un conjunto de filas o que genera un conjunto de filas que no es un cursor de servidor, y la propiedad de origen de datos DBPROP_MULTIPLECONNECTIONS está establecida en VARIANT_TRUE, el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client crea conexiones adicionales para admitir objetos de comando simultáneos, a menos que haya una transacción activa, en cuyo caso devolverá un error. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administra las transacciones y el bloqueo para cada conexión. Si se genera una segunda conexión, los comandos de cada una de las conexiones no comparten los bloqueos. Hay que tener cuidado para asegurarse de que un comando no bloquee otro comando manteniendo bloqueos en filas solicitadas por el otro comando. Si MARS está habilitado, puede haber varios comandos activos en las conexiones y si se utilizan transacciones explícitas, todos los comandos comparten una transacción común.  
  
 El consumidor puede cancelar el comando mediante [issabort:: Abort](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md) o liberando todas las referencias que se mantienen en el objeto de comando y el conjunto de filas derivado.  
  
 Usar **IMultipleResults** en todas las instancias, el consumidor puede obtener todos los conjuntos de filas generados mediante la ejecución de comandos y permite que los consumidores determinar apropiadamente cuándo se debe cancelar la ejecución de comandos y liberar un objeto de sesión para su uso con otros comandos.  
  
> [!NOTE]  
>  Si se utilizan cursores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la ejecución de comandos crea el cursor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] indica si la creación del cursor se ha llevado a cabo correctamente o no; por consiguiente, el viaje de ida y vuelta (round trip) a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se completa cuando se obtiene el resultado de la ejecución del comando. Cada **GetNextRows** llamada, a continuación, se convierte en un de ida y vuelta. De esta manera, pueden existir varios objetos de comando activos, y cada uno de ellos procesará un conjunto de filas que es el resultado de una captura del cursor de servidor. Para obtener más información, consulte [conjuntos de filas y cursores de servidor SQL](../../relational-databases/native-client-ole-db-rowsets/rowsets-and-sql-server-cursors.md).  
  
## <a name="see-also"></a>Vea también  
 [Comandos](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
