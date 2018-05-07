---
title: sp_cursorprepare (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepare_TSQL
- sp_cursor_prepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_prepare
ms.assetid: 6207e110-f4bf-4139-b3ec-b799c9cb3ad7
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 38f5b276554f749990e73f5c1561a7dadcf3f805
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spcursorprepare-transact-sql"></a>sp_cursorprepare (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Compila la instrucción de cursor o lote en un plan de ejecución, pero no crea el cursor. sp_cursorexecute puede utilizar después la instrucción compilada. Este procedimiento, junto con sp_cursorexecute, tiene la misma función que sp_cursoropen, pero se divide en dos fases. sp_cursorprepare se invoca especificando el identificador = 3 en un paquete de flujo TDS.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_cursorprepare prepared_handle OUTPUT, params , stmt , options  
    [ , scrollopt[ , ccopt]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *prepared_handle*  
 Un SQL Server preparado y generado por *controlar* identificador que devuelve un valor entero.  
  
> [!NOTE]  
>  *prepared_handle* se proporciona posteriormente a un procedimiento sp_cursorexecute para abrir un cursor. Una vez creado un identificador, existe hasta que cierre sesión o hasta que lo quite explícitamente a través de un procedimiento sp_cursorunprepare.  
  
 *Params*  
 Identifica instrucciones con parámetros. El *params* definición de las variables se sustituye por marcadores de parámetros en la instrucción. *params* es un parámetro necesario que requiere un **ntext**, **nchar**, o **nvarchar** valor de entrada. Escriba un valor NULL si la instrucción no tiene parámetros.  
  
> [!NOTE]  
>  Use un **ntext** cadena como entrada de valor cuando *stmt* tiene parámetros y la *scrollopt* valor PARAMETERIZED_STMT es ON.  
  
 *stmt*  
 Define el conjunto de resultados del cursor. El *stmt* parámetro es necesario y requiere un **ntext**, **nchar** o **nvarchar** valor de entrada.  
  
> [!NOTE]  
>  Las reglas para especificar el *stmt* valor son los mismos que para sp_cursoropen, con la excepción de que el *stmt* debe ser el tipo de datos string **ntext**.  
  
 *options*  
 Parámetro opcional que devuelve una descripción de las columnas del conjunto de resultados del cursor. *Opciones de* requiere lo siguiente **int** valor de entrada.  
  
|Value|Description|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
 *scrollopt*  
 Opción de desplazamiento. *scrollopt* es un parámetro opcional que requiere uno de los siguientes **int** valores de entrada.  
  
|Value|Description|  
|-----------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
|0x10|FAST_FORWARD|  
|0x1000|PARAMETERIZED_STMT|  
|0x2000|AUTO_FETCH|  
|0x4000|AUTO_CLOSE|  
|0x8000|CHECK_ACCEPTED_TYPES|  
|0x10000|KEYSET_ACCEPTABLE|  
|0x20000|DYNAMIC_ACCEPTABLE|  
|0x40000|FORWARD_ONLY_ACCEPTABLE|  
|0x80000|STATIC_ACCEPTABLE|  
|0x100000|FAST_FORWARD_ACCEPTABLE|  
  
 Dado que no sean adecuado para el cursor definido por el valor solicitado *stmt*, este parámetro actúa tanto de entrada y salida. En casos como este, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asigna un valor adecuado.  
  
 *ccopt*  
 Opción de control de simultaneidad. *ccopt* es un parámetro opcional que requiere uno de los siguientes **int** valores de entrada.  
  
|Value|Description|  
|-----------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS (conocido anteriormente como LOCKCC)|  
|0x0004|**OPTIMISTA** (conocido anteriormente como OPTCC)|  
|0x0008|OPTIMISTIC (conocido anteriormente como OPTCCVAL)|  
|0x2000|ALLOW_DIRECT|  
|0x4000|UPDT_IN_PLACE|  
|0x8000|CHECK_ACCEPTED_OPTS|  
|0x10000|READ_ONLY_ACCEPTABLE|  
|0x20000|SCROLL_LOCKS_ACCEPTABLE|  
|0x40000|OPTIMISTIC_ACCEPTABLE|  
|0x80000|OPTIMISITC_ACCEPTABLE|  
  
 Al igual que con *scrollpt*, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede asignar un valor diferente de la que se solicita.  
  
## <a name="remarks"></a>Comentarios  
 El parámetro de estado de RPC es uno de los siguientes:  
  
|Value|Descripción|  
|-----------|-----------------|  
|0|Success|  
|0x0001|Failure|  
|1FF6|No pudo devolver los metadatos.<br /><br /> Nota: La razón de ello es que la instrucción no genera un conjunto de resultados; Por ejemplo, es una instrucción INSERT o DDL.|  
  
## <a name="examples"></a>Ejemplos  
 Cuando *stmt* tiene parámetros y la *scrollopt* valor PARAMETERIZED_STMT es ON, el formato de la cadena es como sigue:  
  
 {  *\<nombre de variable local > **\<tipo de datos >* } [,...] *n* ]  
  
## <a name="see-also"></a>Vea también  
 [sp_cursorexecute &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorexecute-transact-sql.md)   
 [sp_cursoropen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorunprepare &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorunprepare-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
