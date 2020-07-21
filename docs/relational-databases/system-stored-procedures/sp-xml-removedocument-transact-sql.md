---
title: sp_xml_removedocument (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_xml_removedocument_TSQL
- sp_xml_removedocument
dev_langs:
- TSQL
helpviewer_keywords:
- sp_xml_removedocument
ms.assetid: f9dca50a-8baf-4170-90bc-e72783ce5b73
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e3ee34c74a10414104f96190cd04244c28171db4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85790330"
---
# <a name="sp_xml_removedocument-transact-sql"></a>sp_xml_removedocument (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Quita la representación interna del documento XML especificado por el identificador del documento y lo convierte en no válido.  
  
> [!NOTE]  
>  Un documento analizado se guarda en la caché interna de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El analizador MSXML (Msxmlsql.dll) utiliza una octava parte de la memoria total disponible para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para evitar quedarse sin memoria, ejecute **sp_xml_removedocument** para liberar memoria.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_xml_removedocument hdoc  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdoc*  
 Es el identificador del documento recién creado. Un identificador que no es válido devuelve un error. *hdoc* es un entero.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o >0 (error)  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se quita la representación interna de un documento XML. El identificador del documento se proporciona como entrada.  
  
```  
EXEC sp_xml_removedocument @hdoc;  
```  
  
## <a name="see-also"></a>Consulte también      
 <br>[Procedimientos almacenados del sistema (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)
 <br>[Procedimientos almacenados XML (Transact-SQL)](../../relational-databases/system-stored-procedures/xml-stored-procedures-transact-sql.md)
 <br>[Sys. dm_exec_xml_handles (Transact-SQL)](../system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)
 <br>[sp_xml_preparedocument (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql.md)
 <br>[OPENXML (Transact-SQL)](../../t-sql/functions/openxml-transact-sql.md)
  
  
