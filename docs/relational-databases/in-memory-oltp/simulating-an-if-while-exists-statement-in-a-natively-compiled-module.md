---
title: 'Simulación de IF-WHILE EXISTS: módulo compilado de forma nativa'
description: Obtenga información sobre cómo simular la cláusula EXISTS en instrucciones condicionales, la cual no es compatible con los procedimientos almacenados compilados de forma nativa en SQL Server.
ms.custom: seo-dt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c0e187c1-cbd9-463c-b417-8a734574f102
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0438806d15caf806c4598f3d2b3882011d77d0f5
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97485207"
---
# <a name="simulating-an-if-while-exists-statement-in-a-natively-compiled-module"></a>Simular una instrucción IF-WHILE EXISTS en un módulo compilado de forma nativa
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Los procedimientos almacenados compilados de forma nativa no admiten la cláusula **EXISTS** en instrucciones condicionales como IF y WHILE.  
  
 En el ejemplo siguiente se muestra una solución mediante una variable BIT con una instrucción SELECT para simular una cláusula EXISTS:  
  
```sql  
DECLARE @exists BIT = 0  
SELECT TOP 1 @exists = 1 FROM MyTable WHERE ...  
IF @exists = 1  
```  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de migración para los procedimientos almacenados compilados de forma nativa](./a-guide-to-query-processing-for-memory-optimized-tables.md)   
 [Construcciones de Transact-SQL no admitidas en In-Memory OLTP.](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
