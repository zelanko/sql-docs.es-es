---
title: Read (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Read_TSQL
- Read
dev_langs:
- TSQL
helpviewer_keywords:
- Read [Database Engine]
ms.assetid: f2b8207c-b69f-4327-a874-100b3a1f27d8
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 9fb69a5c4e9d303ab0e3a7a3e2edeeeeed228391
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68000605"
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
  
## <a name="see-also"></a>Consulte también  
[Write &#40;motor de base de datos&#41;](../../t-sql/data-types/write-database-engine.md)  
[ToString &#40;motor de base de datos&#41;](../../t-sql/data-types/tostring-database-engine.md)  
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Referencia de los métodos del tipo de datos hierarchyid](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  
