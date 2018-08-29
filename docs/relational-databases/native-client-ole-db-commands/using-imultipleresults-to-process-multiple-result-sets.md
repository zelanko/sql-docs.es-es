---
title: Uso de IMultipleResults para procesar varios conjuntos de resultados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- IMultipleResults interface
- multiple-rowset results
ms.assetid: 754d3f30-7d94-4b67-8dac-baf2699ce9c6
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2626d2a7b81eab998f6d6410a124a47e914e5b64
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43087282"
---
# <a name="using-imultipleresults-to-process-multiple-result-sets"></a>Utilizar IMultipleResults para procesar varios conjuntos de resultados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Los consumidores utilizan la **IMultipleResults** interfaz para procesar los resultados devueltos por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecución de comando del proveedor OLE DB de Native Client. Cuando el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client envía un comando de ejecución, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecuta las instrucciones y devuelve todos los resultados.  
  
 Un cliente debe procesar todos los resultados de la ejecución de comandos. Dado que el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecución de comando del proveedor OLE DB de Native Client puede generar objetos de varios conjuntos de filas como resultado, use la **IMultipleResults** interfaz para asegurarse de que se complete la recuperación de datos de aplicación el ida y vuelta iniciada por el cliente.  
  
 La siguiente instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] genera varios conjuntos de filas; unos contienen datos de filas de la tabla **OrderDetails** y otros contienen resultados de la cláusula COMPUTE BY:  
  
```  
SELECT OrderID, FullPrice = (UnitPrice * Quantity), Discount,  
    Discounted = UnitPrice * (1 - Discount) * Quantity  
FROM OrderDetails  
ORDER BY OrderID  
COMPUTE  
    SUM(UnitPrice * Quantity), SUM(UnitPrice * (1 - Discount) * Quantity)  
    BY OrderID  
```  
  
 Si un consumidor ejecuta un comando que contiene este texto y solicita un conjunto de filas como interfaz de resultados devueltos, solo se devuelve el primer conjunto de filas. El consumidor puede procesar todas las filas del conjunto de filas devuelto. Sin embargo, si se establece la propiedad de origen de datos DBPROP_MULTIPLECONNECTIONS en VARIANT_FALSE y MARS no está habilitado en la conexión, no se puede ejecutar ningún otro comando en el objeto de sesión (la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client no creará otra conexión) hasta que se cancela el comando. Si MARS no está habilitado en la conexión, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client devuelve un error DB_E_OBJECTOPEN si DBPROP_MULTIPLECONNECTIONS es VARIANT_FALSE y devuelve E_FAIL si hay una transacción activa.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client también devolverá DB_E_OBJECTOPEN al usar parámetros de salida transmitidos y la aplicación no ha consumido todos los valores de parámetro de salida devueltos antes de llamar a **IMultipleResults:: GetResults**  para obtener el siguiente conjunto de resultados. Si MARS no está habilitado y la conexión está ocupada ejecutando un comando que no genera un conjunto de filas o que genera un conjunto de filas que no es un cursor de servidor, y la propiedad de origen de datos DBPROP_MULTIPLECONNECTIONS está establecida en VARIANT_TRUE, el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client crea conexiones adicionales para admitir objetos de comando simultáneos, a menos que haya una transacción activa, en cuyo caso devolverá un error. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administra las transacciones y el bloqueo para cada conexión. Si se genera una segunda conexión, los comandos de cada una de las conexiones no comparten los bloqueos. Hay que tener cuidado para asegurarse de que un comando no bloquee otro comando manteniendo bloqueos en filas solicitadas por el otro comando. Si MARS está habilitado, puede haber varios comandos activos en las conexiones y si se utilizan transacciones explícitas, todos los comandos comparten una transacción común.  
  
 El consumidor puede cancelar el comando mediante [ISSAbort::Abort](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md) o al liberar todas las referencias que se mantienen en el objeto de comando y el conjunto de filas derivado.  
  
 Si se usa **IMultipleResults** en todas las instancias, el consumidor puede obtener todos los conjuntos de filas generados mediante la ejecución de comandos, determinar apropiadamente cuándo se ha de cancelar la ejecución de comandos y liberar un objeto de sesión para que lo puedan usar otros comandos.  
  
> [!NOTE]  
>  Si se utilizan cursores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la ejecución de comandos crea el cursor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] indica si la creación del cursor se ha llevado a cabo correctamente o no; por consiguiente, el viaje de ida y vuelta (round trip) a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se completa cuando se obtiene el resultado de la ejecución del comando. Así, cada llamada a **GetNextRows** se convierte en un recorrido de ida y vuelta. De esta manera, pueden existir varios objetos de comando activos, y cada uno de ellos procesará un conjunto de filas que es el resultado de una captura del cursor de servidor. Para obtener más información, vea [Conjuntos de filas y cursores de SQL Server](../../relational-databases/native-client-ole-db-rowsets/rowsets-and-sql-server-cursors.md).  
  
## <a name="see-also"></a>Vea también  
 [Comandos](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
