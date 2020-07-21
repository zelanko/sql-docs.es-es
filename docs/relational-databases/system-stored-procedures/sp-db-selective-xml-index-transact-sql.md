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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: eeed1432c6f3c3ba4f6dcd80608c2c40bd0db374
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728209"
---
# <a name="sp_db_selective_xml_index-transact-sql"></a>sp_db_selective_xml_index (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Habilita y deshabilita la funcionalidad de Índice XML selectivo en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si se llama sin ningún parámetro, el procedimiento almacenado devuelve 1 si el índice XML selectivo está habilitado en una base de datos determinada.  
  
> [!NOTE]  
>  Para deshabilitar el índice XML selectivo mediante este procedimiento almacenado, la base de datos se debe poner en modo de recuperación simple mediante el comando de [opciones set de Alter database &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md) .  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
  
      sys.sp_db_selective_xml_index[[ @db_name = ] 'db_name'],   
[[ @action = ] 'action']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @ db_name = ] 'db_name'`Nombre de la base de datos en la que se va a habilitar o deshabilitar el índice XML selectivo. Si *db_name* es null, se supone que es la base de datos actual.  
  
`[ @action = ] 'action'`Determina si se debe habilitar o deshabilitar el índice. Si se pasa otro valor, excepto ' on ', ' true ', ' OFF ' o ' false ', se producirá un error.  
  
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
  
### <a name="b-disable-selective-xml-index-functionality"></a>B. Deshabilitar la funcionalidad de índice XML selectivo  
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
  
## <a name="see-also"></a>Consulte también  
 [Índices XML selectivos &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)  
  
  
