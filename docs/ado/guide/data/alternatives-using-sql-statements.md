---
title: 'Alternativas: Mediante instrucciones SQL | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ADO]
- editing data [ADO], sql statements
- ADO, SQL statements
ms.assetid: 8b528b23-063d-45ea-8dea-6a90d4060b20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b95e6f0bd2b702080b3580b8b9eeb80ac5b06e8d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63063131"
---
# <a name="alternatives-using-sql-statements"></a>Alternativas: Uso de instrucciones SQL
ADO también permite usar comandos como alternativa a sus propiedades y métodos integrados para modificar los datos. Dependiendo de su proveedor, todas las operaciones que se mencionan en esta sección también se podrían lograr pasando comandos al origen de datos. Por ejemplo, las instrucciones UPDATE de SQL pueden usarse para modificar los datos sin usar la **valor** propiedad de un **campo**. Las instrucciones INSERT de SQL pueden utilizarse para agregar nuevos registros a un origen de datos, en lugar del método ADO **AddNew**. Para obtener más información acerca de SQL o el lenguaje de manipulación de datos de su proveedor, consulte la documentación del origen de datos.  
  
 Por ejemplo, puede pasar una cadena SQL que contiene una instrucción DELETE en una base de datos, como se muestra en el código siguiente:  
  
```  
'BeginSQLDelete  
strSQL = "DELETE FROM Shippers WHERE ShipperID = " & intId  
objConn1.Execute strSQL, , adCmdText + adExecuteNoRecords  
'EndSQLDelete  
```
