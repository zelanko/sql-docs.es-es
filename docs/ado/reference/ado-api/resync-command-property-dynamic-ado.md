---
title: Resincronizar comando propiedad dinámicos (ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Resync Command property [ADO]
ms.assetid: 4e2bb601-0fe8-4d61-b00e-38341d85a6bb
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 37896464c8c9387cb0d68da8bf9bc561e29602d0
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35281380"
---
# <a name="resync-command-property-dynamic-ado"></a>Resincronizar comando propiedad dinámicos (ADO)
Especifica la cadena de un comando proporcionados por el usuario que la [Resync](../../../ado/reference/ado-api/resync-method.md) problemas del método para actualizar los datos en la tabla mencionada en el [tabla única](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) propiedades dinámicas.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **cadena** valor que es una cadena de comandos.  
  
## <a name="remarks"></a>Notas  
 El [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto es el resultado de una operación JOIN ejecutada en varias tablas base. Las filas afectadas dependen el *AffectRecords* parámetro de la [Resync](../../../ado/reference/ado-api/resync-method.md) método. El estándar **Resync** método se ejecuta si la [tabla única](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) y **Resync Command** propiedades no están establecidas.  
  
 La cadena de comandos de la **Resync Command** propiedad es un comando con parámetros o un procedimiento almacenado que identifica de forma única la fila que se está actualiza y devuelve una sola fila que contiene el mismo número y orden de las columnas como la fila que se va a ser actualizar. La cadena de comandos contiene un parámetro para cada columna de clave principal en la **tabla única**; en caso contrario, se devuelve un error de tiempo de ejecución. Los parámetros se rellenan automáticamente con los valores de clave principal de la fila que se va a actualizar.  
  
 Éstos son dos ejemplos que se basa en SQL:  
  
 1\) el **Recordset** se define mediante un comando:  
  
```  
SELECT * FROM Customers JOIN Orders ON   
   Customers.CustomerID = Orders.CustomerID  
   WHERE city = 'Seattle'  
   ORDER BY CustomerID  
```  
  
 El **Resync Command** propiedad se establece en:  
  
```  
"SELECT * FROM   
   (SELECT * FROM Customers JOIN Orders   
   ON Customers.CustomerID = Orders.CustomerID  
   city = 'Seattle' ORDER BY CustomerID)  
WHERE Orders.OrderID = ?"  
```  
  
 El **tabla única** es *pedidos* y su clave principal, *OrderID*, tiene parámetros. La Subselección proporciona una manera sencilla de asegurarse de que el mismo número y orden de las columnas se devuelven por el comando original mediante programación.  
  
 2\) el **Recordset** se define mediante un procedimiento almacenado:  
  
```  
CREATE PROC Custorders @CustomerID char(5) AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID   
WHERE Customers.CustomerID = @CustomerID  
```  
  
 El **Resync** método debe ejecutar el siguiente procedimiento almacenado:  
  
```  
CREATE PROC CustordersResync @ordid int AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID  
WHERE Orders.ordid  = @ordid  
```  
  
 El **Resync Command** propiedad se establece en:  
  
```  
"{call CustordersResync (?)}"  
```  
  
 Una vez más, la **tabla única** es *pedidos* y su clave principal, *OrderID*, tiene parámetros.  
  
 **Comando Resync** es una propiedad dinámica que se anexa a la **Recordset** objeto [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección cuando la [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad está establecida en **adUseClient**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
