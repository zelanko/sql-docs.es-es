---
title: Lectura (motor de base de datos) | Documentos de Microsoft
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Read_TSQL
- Read
dev_langs:
- TSQL
helpviewer_keywords:
- Read [Database Engine]
ms.assetid: f2b8207c-b69f-4327-a874-100b3a1f27d8
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 21f27c627a36f747d9e3ecbb52d14d1ac6bc5d28
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="read-database-engine"></a>Read (motor de base de datos)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Lectura lee una representación binaria de **SqlHierarchyId** en el pasado **BinaryReader** y establece la **SqlHierarchyId** objeto con ese valor. Lectura no se puede llamar mediante el uso de [!INCLUDE[tsql](../../includes/tsql-md.md)]. En su lugar, use CAST o CONVERT.
  
## <a name="syntax"></a>Sintaxis  
  
```sql
void Read( BinaryReader r )   
```  
  
## <a name="arguments"></a>Argumentos  
*r*  
 El **BinaryReader** objeto que genera una secuencia binaria correspondiente a una representación binaria de un **hierarchyid** nodo.  
  
## <a name="return-types"></a>Tipos de valor devuelto
 **Tipo de valor devuelto CLR: void**  
  
## <a name="remarks"></a>Comentarios  
 Lectura no valida su entrada. Si no se especifica una entrada binaria no válida, lectura puede provocar una excepción. O bien, podría tener éxito y producir un no válido **SqlHierarchyId** objeto cuyos métodos pueden producir resultados imprevisibles o provocar una excepción.  
  
 Lectura solo puede llamarse en otra recién creada **SqlHierarchyId** objeto.  
  
 Lectura se utiliza internamente por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando es necesario, como al escribir datos en **hierarchyid** columna. Lectura también se llama internamente cuando se realiza una conversión entre **varbinary** y **hierarchyid**.  
  
## <a name="examples"></a>Ejemplos  
  
```sql
Byte[] encoding = new byte[] { 0x58 };  
MemoryStream stream = new MemoryStream(encoding, false /*not writable*/);  
BinaryReader br = new BinaryReader(stream);  
SqlHierarchyId hid = new SqlHierarchyId();  
hid.Read(br);   
```  
  
## <a name="see-also"></a>Vea también  
[Escritura &#40; motor de base de datos &#41;](../../t-sql/data-types/write-database-engine.md)  
[ToString &#40; motor de base de datos &#41;](../../t-sql/data-types/tostring-database-engine.md)  
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Referencia de los métodos del tipo de datos hierarchyid](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  

