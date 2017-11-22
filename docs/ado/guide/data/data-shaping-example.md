---
title: Ejemplo de la forma de datos | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: data shaping [ADO], about data shaping
ms.assetid: 1bfdcad4-52e1-45bc-ad21-783657ef0a44
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6ac91d7a7e962443e9798b5b2ecf2daf80ee72eb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="data-shaping-example"></a>Ejemplo de la forma de datos
Los siguientes datos para dar forma al comando muestra cómo compilar un jerárquica **Recordset** desde el **clientes** y **pedidos** tablas en la base de datos Northwind.  
  
```  
SHAPE {SELECT CustomerID, ContactName FROM Customers}   
APPEND ({SELECT OrderID, OrderDate, CustomerID FROM Orders} AS chapOrders   
RELATE customerID TO customerID)   
```  
  
 Cuando se utiliza este comando para abrir un **Recordset** objeto (como se muestra en [ejemplo de Visual Basic de forma de datos](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)), crea un capítulo (**chapOrders**) para cada registro devuelto desde el **clientes** tabla. En este capítulo se compone de un subconjunto de la **Recordset** devuelto desde el **pedidos** tabla. El **chapOrders** capítulo contiene toda la información solicitada sobre los pedidos realizados por un cliente determinado. En este ejemplo, el capítulo consta de tres columnas: **OrderID**, **OrderDate**, y **CustomerID**.  
  
 Las dos primeras entradas de la resultante en forma de **Recordset** son los siguientes:  
  
|CustomerID|ContactName|OrderID|OrderDate|CustomerID|  
|----------------|-----------------|-------------|---------------|----------------|  
|ALFKI|Maria Ander|10643<br /><br /> 10692<br /><br /> 10702<br /><br /> 10835<br /><br /> 10952<br /><br /> 11011|1997-08-25<br /><br /> 1997-10-03<br /><br /> 1997-10-13<br /><br /> 1998-01-15<br /><br /> 1998-03-16<br /><br /> 1998-04-09|ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI|  
|ANATR|Ana Trujillo|10308<br /><br /> 10625<br /><br /> 10759<br /><br /> 10926|1996-09-18<br /><br /> 1997-08-08<br /><br /> 1997-11-28<br /><br /> 1998-03-04|ANATR<br /><br /> ANATR<br /><br /> ANATR<br /><br /> ANATR|  
  
 En un comando SHAPE, APPEND se utiliza para crear un elemento secundario **Recordset** relacionados con el elemento primario **Recordset** (tal como lo devuelve el comando específico del proveedor inmediatamente después de la palabra clave de forma que se explicó más adelante) mediante la cláusula RELATE. Los primarios y secundarios normalmente tienen al menos una columna en común: el valor de la columna en una fila del elemento primario es el mismo que el valor de la columna en todas las filas del elemento secundario.  
  
 Hay una segunda forma de utilizar los comandos de forma: es decir, para generar un elemento primario **Recordset** de un elemento secundario **conjunto de registros**. Los registros en el elemento secundario **Recordset** se agrupan, normalmente mediante la cláusula BY y una fila se agrega al elemento primario **Recordset** para cada grupo resultante en el elemento secundario. Si se omite la cláusula BY, el elemento secundario **Recordset** serán forma un solo grupo y el elemento primario **Recordset** contendrá exactamente una fila. Esto es útil para calcular agregados de "total general" en todo el secundario **conjunto de registros**.  
  
 La construcción de comando de forma también le permite crear mediante programación una forma **conjunto de registros**. A continuación, puede tener acceso a los componentes de la **Recordset** mediante programación o a través de un control visual apropiado. Un comando shape se emite como cualquier otro texto de comando ADO. Para obtener más información, consulte [forma comandos en General](../../../ado/guide/data/shape-commands-in-general.md).  
  
 Independientemente de qué manera el elemento primario **Recordset** está formado, contendrá una columna de capítulo que se utiliza para relacionar con un elemento secundario **conjunto de registros**. Si lo desea, el elemento primario **Recordset** puede tener también columnas que contienen agregados (SUM, MIN, MAX etc.) sobre las filas secundarias. El elemento primario y el elemento secundario **Recordset** puede tener columnas que contienen una expresión en la fila en la **Recordset**, así como las columnas que son nuevos e inicialmente vacía.  
  
 En esta sección continúa con el siguiente tema.  
  
-   [Ejemplo de Visual Basic de forma de datos](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)
