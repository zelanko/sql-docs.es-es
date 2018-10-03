---
title: Ejemplo de la forma de datos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], about data shaping
ms.assetid: 1bfdcad4-52e1-45bc-ad21-783657ef0a44
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 92e34de1b9fd675570527f9a28f8476a51597f10
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696433"
---
# <a name="data-shaping-example"></a>Ejemplo de la forma de datos
El siguientes comando de la forma de datos muestra cómo generar un jerárquica **Recordset** desde el **clientes** y **pedidos** tablas en la base de datos Northwind.  
  
```  
SHAPE {SELECT CustomerID, ContactName FROM Customers}   
APPEND ({SELECT OrderID, OrderDate, CustomerID FROM Orders} AS chapOrders   
RELATE customerID TO customerID)   
```  
  
 Cuando se usa este comando para abrir un **Recordset** objeto (como se muestra en [ejemplo Visual Basic de forma de datos](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)), crea un capítulo (**chapOrders**) para cada registro devuelto desde el **clientes** tabla. Este capítulo consta de un subconjunto de la **Recordset** devuelto desde el **pedidos** tabla. El **chapOrders** capítulo contiene toda la información solicitada sobre los pedidos realizados por un cliente determinado. En este ejemplo, el capítulo consta de tres columnas: **OrderID**, **OrderDate**, y **CustomerID**.  
  
 Las dos primeras entradas de la resultante en forma de **Recordset** son los siguientes:  
  
|CustomerID|ContactName|OrderID|OrderDate|CustomerID|  
|----------------|-----------------|-------------|---------------|----------------|  
|ALFKI|Maria Ander|10643<br /><br /> 10692<br /><br /> 10702<br /><br /> 10835<br /><br /> 10952<br /><br /> 11011|1997-08-25<br /><br /> 1997-10-03<br /><br /> 1997-10-13<br /><br /> 1998-01-15<br /><br /> 1998-03-16<br /><br /> 1998-04-09|ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI|  
|ANATR|Ana Trujillo|10308<br /><br /> 10625<br /><br /> 10759<br /><br /> 10926|1996-09-18<br /><br /> 1997-08-08<br /><br /> 1997-11-28<br /><br /> 1998-03-04|ANATR<br /><br /> ANATR<br /><br /> ANATR<br /><br /> ANATR|  
  
 En un comando SHAPE, APPEND se utiliza para crear un elemento secundario **Recordset** relacionados con el elemento primario **Recordset** (tal como lo devuelve el comando específico del proveedor inmediatamente después de la palabra clave de forma que se ha analizado más adelante) mediante la cláusula RELATE. Los primarios y secundarios suelen tengan al menos una columna en común: el valor de la columna en una fila del elemento primario es el mismo que el valor de la columna en todas las filas del elemento secundario.  
  
 Hay una segunda forma de usar comandos de forma: es decir, para generar un elemento primario **Recordset** desde un elemento secundario **Recordset**. Los registros en el elemento secundario **Recordset** se agrupan, normalmente mediante la cláusula BY y una fila se agrega al elemento primario **Recordset** para cada grupo resultante en el elemento secundario. Si se omite la cláusula BY, el elemento secundario **Recordset** le formulario de un solo grupo y el elemento primario **Recordset** contendrá exactamente una fila. Esto es útil para calcular agregados de "total general" en todo el secundario **Recordset**.  
  
 La construcción de comando de forma también le permite crear mediante programación una forma **Recordset**. A continuación, puede tener acceso a los componentes de la **Recordset** mediante programación o a través de un control visual adecuado. Se emite un comando de forma similar a cualquier otro texto de comando ADO. Para obtener más información, consulte [comandos de forma General](../../../ado/guide/data/shape-commands-in-general.md).  
  
 Independientemente de qué manera el elemento primario **Recordset** está formado, contiene una columna de capítulo se usa para relacionarla con un elemento secundario **Recordset**. Si lo desea, el elemento primario **Recordset** también se puede tener columnas que contienen agregados (SUM, MIN, MAX etc.) a través de las filas secundarias. El elemento primario y secundario **Recordset** pueden tener columnas que contienen una expresión en la fila de la **Recordset**, así como las columnas que son nuevos e inicialmente vacía.  
  
 En esta sección se continúa con el siguiente tema.  
  
-   [Ejemplo de Visual Basic de forma de datos](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)
