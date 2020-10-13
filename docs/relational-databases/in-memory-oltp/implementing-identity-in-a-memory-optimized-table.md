---
title: Implementar IDENTITY en una tabla con optimización para memoria | Microsoft Docs
description: Obtenga información sobre IDENTITY en las tablas optimizadas para memoria en SQL Server. Las tablas optimizadas para memoria admiten IDENTITY para un valor de inicialización e incremento de uno.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c0a704a3-3a31-4c2c-b967-addacda62ef8
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5aecab53a9144d5254eb85190f7652dbe090bf82
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2020
ms.locfileid: "91869119"
---
# <a name="implementing-identity-in-a-memory-optimized-table"></a>Implementar IDENTITY en una tabla con optimización para memoria
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

IDENTITY se admite en una tabla optimizada para memoria siempre y cuando el valor de inicialización y el incremento sean ambos 1 (que es el valor predeterminado). Las columnas de identidad con la definición de IDENTITY(x, y) donde x != 1 o y != 1 no se admiten en las tablas optimizadas para memoria.   
    
Para aumentar el valor de inicialización de IDENTITY, inserte una nueva fila con un valor explícito para la columna de identidad con la opción de sesión `SET IDENTITY_INSERT table_name ON`. Al insertar la fila, el valor de inicialización de IDENTITY se cambia por el valor insertado explícitamente más 1. Por ejemplo, para aumentar el valor de inicialización a 1000, inserte una fila con el valor 999 en la columna de identidad. De esta forma, los valores de identidad que se generen comenzarán a partir de 1000.     
  
## <a name="see-also"></a>Consulte también  
 [Migrar a OLTP en memoria](./plan-your-adoption-of-in-memory-oltp-features-in-sql-server.md)  
  
