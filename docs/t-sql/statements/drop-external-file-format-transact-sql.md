---
title: QUITAR el formato de archivo externo (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8cf9009b-59f9-4aac-bef1-dcf2cf0708b2
caps.latest.revision: 12
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 25719f7617cbb75b1b9467a00c392f703a9710ac
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="drop-external-file-format-transact-sql"></a>QUITAR el formato de archivo externo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Quita un formato de archivo externo de PolyBase.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Drop an external file format  
DROP EXTERNAL FILE FORMAT external_file_format_name  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *external_file_format_name*  
 El nombre del formato de archivo externo para quitar.  
  
## <a name="metadata"></a>Metadatos  
 Para ver una lista de formatos de archivo externo, utilice la [sys.external_file_formats &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md) vista del sistema.  
  
```  
SELECT * FROM sys.external_file_formats;  
```  
  
## <a name="permissions"></a>Permissions  
 Requiere modificar cualquier formato de archivo externo.  
  
## <a name="general-remarks"></a>Notas generales  
 Al quitar un formato de archivo externo, no quita los datos externos.  
  
## <a name="locking"></a>Bloqueo  
 Toma un bloqueo compartido en el objeto de formato de archivo externo.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-basic-syntax"></a>A. Con la sintaxis básica  
  
```  
DROP EXTERNAL FILE FORMAT myfileformat;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-using-basic-syntax"></a>B. Con la sintaxis básica  
  
```  
DROP EXTERNAL FILE FORMAT myfileformat;  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)  
  
  


