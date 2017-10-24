---
title: Coloque el origen de datos externo (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 3f65a2f5-a6c6-4be5-8ca4-6057078fe10e
caps.latest.revision: 14
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 6657a09ca9f3e1e700e078d707c92c495e444d42
ms.contentlocale: es-es
ms.lasthandoff: 10/24/2017

---
# <a name="drop-external-data-source-transact-sql"></a>Coloque el origen de datos externo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Quita un origen de datos externo de PolyBase.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Drop an external data source  
DROP EXTERNAL DATA SOURCE external_data_source_name  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *external_data_source_name*  
 El nombre del origen de datos externo para quitar.  
  
## <a name="metadata"></a>Metadatos  
 Para ver una lista de datos externos orígenes usan la vista del sistema sys.external_data_sources.  
  
```  
SELECT * FROM sys.external_data_sources;  
```  
  
## <a name="permissions"></a>Permissions  
 Requiere modificar cualquier origen de datos externo.  
  
## <a name="locking"></a>Bloqueo  
 Tiene un bloqueo compartido en el objeto de origen de datos externo.  
  
## <a name="general-remarks"></a>Notas generales  
 Al quitar un origen de datos externo, no quita los datos externos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-basic-syntax"></a>A. Con la sintaxis básica  
  
```  
DROP EXTERNAL DATA SOURCE mydatasource;  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  


