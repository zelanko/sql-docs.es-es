---
title: Write (motor de base de datos) | Documentos de Microsoft
ms.custom: 
ms.date: 07/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Write_TSQL
- Write
dev_langs:
- TSQL
helpviewer_keywords:
- Write [Database Engine]
ms.assetid: 7c554334-d2d9-4eae-a4ae-097aa4020e1a
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 60707b57671c2ad607bd85b0fedececccd478038
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="write-database-engine"></a>Write (motor de base de datos)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Escribir escribe una representación binaria de **SqlHierarchyId** en el pasado **BinaryWriter**. Escritura no se puede llamar mediante el uso de [!INCLUDE[tsql](../../includes/tsql-md.md)]. En su lugar, use CAST o CONVERT.
  
## <a name="syntax"></a>Sintaxis  
  
```sql
void Write( BinaryWriter w )   
```  
  
## <a name="arguments"></a>Argumentos  
*w*  
A **BinaryWriter** objeto al que la representación binaria de este **hierarchyid** nodo se escribirá.
  
## <a name="return-types"></a>Tipos devueltos  
**Tipo de valor devuelto CLR: void**
  
## <a name="remarks"></a>Comentarios  
Escribir se usa internamente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando es necesario, como al cargar datos desde una **hierarchyid** columna. Escritura también se llama internamente cuando se realiza una conversión entre **hierarchyid** y **varbinary**.
  
## <a name="examples"></a>Ejemplos  
  
```sql
MemoryStream stream = new MemoryStream();  
BinaryWriter bw = new BinaryWriter(stream);  
hid.Write(bw);  
byte[] encoding = stream.ToArray();  
  
```  
  
## <a name="see-also"></a>Vea también
[Lectura &#40; motor de base de datos &#41;](../../t-sql/data-types/read-database-engine.md)  
[ToString &#40; motor de base de datos &#41;](../../t-sql/data-types/tostring-database-engine.md)  
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Referencia de los métodos del tipo de datos hierarchyid](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  

