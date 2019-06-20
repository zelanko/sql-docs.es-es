---
title: sp_db_selective_xml_index (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_db_selective_xml_index_TSQL
- sp_db_selective_xml_index
dev_langs:
- TSQL
helpviewer_keywords:
- sp_db_selective_xml_index procedure
ms.assetid: 017301a2-4a23-4e68-82af-134f3d4892b3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e9b1752b5e567c2a26080422874e5bf6e31bc568
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62506679"
---
# <a name="spdbselectivexmlindex-transact-sql"></a>sp_db_selective_xml_index (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Habilita y deshabilita la funcionalidad de Índice XML selectivo en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si se llama sin ningún parámetro, el procedimiento almacenado devuelve 1 si el índice XML selectivo está habilitado en una base de datos determinada.  
  
> [!NOTE]  
>  Para deshabilitar el índice XML selectivo con este procedimiento almacenado, la base de datos debe colocarse en modo de recuperación simple mediante el [ALTER DATABASE SET Options &#40;Transact-SQL&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) comando.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
  
      sys.sp_db_selective_xml_index[[ @db_name = ] 'db_name'],   
[[ @action = ] 'action']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @ db_name = ] 'db_name'` El nombre de la base de datos para habilitar o deshabilitar el índice XML selectivo. Si *db_name* es NULL, se supone que la base de datos actual.  
  
`[ @action = ] 'action'` Determina si se debe habilitar o deshabilitar el índice. Si otro valor que no sea 'on', se pasa 'true', 'off' o 'false', se producirá un error.  
  
```  
  
Allowed values: 'on', 'off', 'true', 'false'  
```  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **1** si el índice XML selectivo está habilitado en una base de datos determinada.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-enable-selective-xml-index-functionality"></a>A. Habilitar la funcionalidad de índice XML selectivo  
 En el ejemplo siguiente se habilita el índice XML selectivo en la base de datos actual.  
  
```  
EXECUTE sys.sp_db_selective_xml_index  
    @db_name = NULL  
  , @action = N'on';  
GO  
```  
  
 En el ejemplo siguiente se habilita el índice XML selectivo en la base de datos AdventureWorks2012.  
  
```  
EXECUTE sys.sp_db_selective_xml_index  
    @db_name = N'AdventureWorks2012'  
  , @action = N'true';  
GO  
```  
  
### <a name="b-disable-selective-xml-index-functionality"></a>b. Deshabilitar la funcionalidad de índice XML selectivo  
 En el ejemplo siguiente se deshabilita el índice XML selectivo en la base de datos actual.  
  
```  
EXECUTE sys.sp_db_selective_xml_index  
    @db_name = NULL  
  , @action = N'off';  
GO  
```  
  
 En el ejemplo siguiente se deshabilita el índice XML selectivo en la base de datos AdventureWorks2012.  
  
```  
EXECUTE sys.sp_db_selective_xml_index  
    @db_name = N'AdventureWorks2012'  
  , @action = N'false';  
GO  
```  
  
### <a name="c-detect-if-selective-xml-index-is-enabled"></a>C. Detectar si el índice XML selectivo está habilitado  
 En el ejemplo siguiente se detecta si el índice XML selectivo está habilitado. Devuelve 1 si el índice XML selectivo está habilitado.  
  
```  
EXECUTE sys.sp_db_selective_xml_index;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Índices XML selectivos &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)  
  
  
