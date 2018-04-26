---
title: Read (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 433a83375e2ae256963c5f304d9c6921086e41f9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="read-database-engine"></a>Read (motor de base de datos)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Read lee una representación binaria de **SqlHierarchyId** desde la clase **BinaryReader** pasada y establece el objeto **SqlHierarchyId** en dicho valor. No se puede llamar a Read con [!INCLUDE[tsql](../../includes/tsql-md.md)]. En su lugar, use CAST o CONVERT.
  
## <a name="syntax"></a>Sintaxis  
  
```sql
void Read( BinaryReader r )   
```  
  
## <a name="arguments"></a>Argumentos  
*r*  
 El objeto **BinaryReader** que produce un flujo binario correspondiente a una representación binaria de un nodo **hierarchyid**.  
  
## <a name="return-types"></a>Tipos de valores devueltos
 **Tipo de valor devuelto de CLR: void**  
  
## <a name="remarks"></a>Notas  
 Read no valida su entrada. Si se proporciona una entrada binaria no válida, Read puede provocar una excepción. O bien, la operación puede realizarse sin errores y producir un objeto **SqlHierarchyId** no válido cuyos métodos pueden producir resultados imprevisibles o provocar una excepción.  
  
 Solo se puede llamar a Read en un objeto **SqlHierarchyId** recién creado.  
  
 Read usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] internamente cuando es necesario, por ejemplo, al escribir datos en la columna **hierarchyid**. También se llama a Read internamente cuando se realiza una conversión entre **varbinary** y **hierarchyid**.  
  
## <a name="examples"></a>Ejemplos  
  
```sql
Byte[] encoding = new byte[] { 0x58 };  
MemoryStream stream = new MemoryStream(encoding, false /*not writable*/);  
BinaryReader br = new BinaryReader(stream);  
SqlHierarchyId hid = new SqlHierarchyId();  
hid.Read(br);   
```  
  
## <a name="see-also"></a>Ver también  
[Write &#40;motor de base de datos&#41;](../../t-sql/data-types/write-database-engine.md)  
[ToString &#40;motor de base de datos&#41;](../../t-sql/data-types/tostring-database-engine.md)  
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Referencia de los métodos del tipo de datos hierarchyid](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  
