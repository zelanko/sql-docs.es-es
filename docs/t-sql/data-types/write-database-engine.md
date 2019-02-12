---
title: Write (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 07/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Write_TSQL
- Write
dev_langs:
- TSQL
helpviewer_keywords:
- Write [Database Engine]
ms.assetid: 7c554334-d2d9-4eae-a4ae-097aa4020e1a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3ba1be72858cea8813b500020b7a429f63570da0
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031276"
---
# <a name="write-database-engine"></a>Write (motor de base de datos)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Write escribe una representación binaria de **SqlHierarchyId** en la clase **BinaryWriter** pasada. No se puede llamar a Write por medio de [!INCLUDE[tsql](../../includes/tsql-md.md)]. En su lugar, use CAST o CONVERT.
  
## <a name="syntax"></a>Sintaxis  
  
```sql
void Write( BinaryWriter w )   
```  
  
## <a name="arguments"></a>Argumentos  
*w*  
Un objeto **BinaryWriter** en el que se escribirá la representación binaria de este nodo de **hierarchyid**.
  
## <a name="return-types"></a>Tipos devueltos  
**Tipo de valor devuelto de CLR: void**
  
## <a name="remarks"></a>Notas  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa Write internamente cuando es necesario, por ejemplo, al cargar datos en la columna **hierarchyid**. También se llama a Write internamente cuando se realiza una conversión entre **hierarchyid** y **varbinary**.
  
## <a name="examples"></a>Ejemplos  
  
```sql
MemoryStream stream = new MemoryStream();  
BinaryWriter bw = new BinaryWriter(stream);  
hid.Write(bw);  
byte[] encoding = stream.ToArray();  
  
```  
  
## <a name="see-also"></a>Vea también
[Read &#40;motor de base de datos&#41;](../../t-sql/data-types/read-database-engine.md)  
[ToString &#40;motor de base de datos&#41;](../../t-sql/data-types/tostring-database-engine.md)  
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Referencia de los métodos del tipo de datos hierarchyid](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  
