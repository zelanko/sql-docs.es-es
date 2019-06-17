---
title: Resincronizar comando propiedad dinámicos (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Resync Command property [ADO]
ms.assetid: 4e2bb601-0fe8-4d61-b00e-38341d85a6bb
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5acaaa20667ac13f89b41391c1cc1d567eccf580
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711667"
---
# <a name="resync-command-property-dynamic-ado"></a>Resincronizar comando propiedad dinámicos (ADO)
Especifica la cadena de un comando proporcionado por el usuario que la [Resync](../../../ado/reference/ado-api/resync-method.md) problemas del método para actualizar los datos en la tabla mencionada en el [Unique Table](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) propiedad dinámica.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **cadena** valor que es una cadena de comandos.  
  
## <a name="remarks"></a>Comentarios  
 El [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto es el resultado de una operación de combinación que se ejecuta en varias tablas base. Dependen de las filas afectadas las *AffectRecords* parámetro de la [Resync](../../../ado/reference/ado-api/resync-method.md) método. El estándar **Resync** método se ejecuta si la [Unique Table](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) y **resincronizar comando** no se establecen propiedades.  
  
 La cadena de comandos de la **resincronizar comando** propiedad es un procedimiento almacenado que identifica la fila que se va a actualizar o un comando con parámetros y devuelve una sola fila que contiene el mismo número y orden de las columnas como la fila sea actualizar. La cadena de comandos contiene un parámetro para cada columna de clave principal en el **Unique Table**; en caso contrario, se devuelve un error de tiempo de ejecución. Los parámetros se rellenan automáticamente con los valores de clave principal de la fila que se va a actualizar.  
  
 Estos son dos ejemplos basados en SQL:  
  
 1\) el **Recordset** se define mediante un comando:  
  
```  
SELECT * FROM Customers JOIN Orders ON   
   Customers.CustomerID = Orders.CustomerID  
   WHERE city = 'Seattle'  
   ORDER BY CustomerID  
```  
  
 El **resincronizar comando** propiedad está establecida en:  
  
```  
"SELECT * FROM   
   (SELECT * FROM Customers JOIN Orders   
   ON Customers.CustomerID = Orders.CustomerID  
   city = 'Seattle' ORDER BY CustomerID)  
WHERE Orders.OrderID = ?"  
```  
  
 El **Unique Table** es *pedidos* y su clave principal, *OrderID*, tiene parámetros. La Subselección proporciona una manera sencilla de asegurarse de que el mismo número y orden de las columnas se devuelven como, por el comando original mediante programación.  
  
 2\) el **Recordset** se define mediante un procedimiento almacenado:  
  
```  
CREATE PROC Custorders @CustomerID char(5) AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID   
WHERE Customers.CustomerID = @CustomerID  
```  
  
 El **Resync** método debería ejecutar el siguiente procedimiento almacenado:  
  
```  
CREATE PROC CustordersResync @ordid int AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID  
WHERE Orders.ordid  = @ordid  
```  
  
 El **resincronizar comando** propiedad está establecida en:  
  
```  
"{call CustordersResync (?)}"  
```  
  
 Una vez más, el **Unique Table** es *pedidos* y su clave principal, *OrderID*, tiene parámetros.  
  
 **Resincronizar comando** se anexa una propiedad dinámica a la **Recordset** objeto [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección cuando el [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad está establecida en **adUseClient**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
