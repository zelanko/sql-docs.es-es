---
title: "Implementar IDENTITY en una tabla con optimización para memoria | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c0a704a3-3a31-4c2c-b967-addacda62ef8
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 21133ec5172c13b5d010c9aef1f461282acd35b5
ms.lasthandoff: 04/11/2017

---
# <a name="implementing-identity-in-a-memory-optimized-table"></a>Implementar IDENTITY en una tabla con optimización para memoria
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

IDENTITY se admite en una tabla con optimización para memoria siempre y cuando el valor de inicialización y el incremento sean ambos 1 (que es el valor predeterminado). Las columnas de identidad con la definición de IDENTITY(x, y) donde x != 1 o y != 1 no se admiten en las tablas con optimización para memoria.   
    
Para aumentar el valor de inicialización de IDENTITY, inserte una nueva fila con un valor explícito para la columna de identidad con la opción de sesión `SET IDENTITY_INSERT table_name ON`. Al insertar la fila, el valor de inicialización de IDENTITY se cambia por el valor insertado explícitamente más 1. Por ejemplo, para aumentar el valor de inicialización a 1000, inserte una fila con el valor 999 en la columna de identidad. De esta forma, los valores de identidad que se generen comenzarán a partir de 1000.     
  
## <a name="see-also"></a>Vea también  
 [Migrar a OLTP en memoria](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  
