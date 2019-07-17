---
title: sp_cursorprepexec (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursorprepexec_TSQL
- sp_cursorprepexec
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorprepexec
ms.assetid: 8094fa90-35b5-4cf4-8012-0570cb2ba1e6
author: stevestein
ms.author: sstein
ms.openlocfilehash: c344948b5eab2de6c7987494a29fe1131c47f35a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108416"
---
# <a name="spcursorprepexec-transact-sql"></a>sp_cursorprepexec (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Compila un plan para la instrucción de cursor enviada o lote. Después, crea y rellena el cursor. sp_cursorprepexec combina las funciones de sp_cursorprepare y sp_cursorexecute. Estos procedimientos se invocan especificando el identificador 5 en un paquete de flujo TDS.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_cursorprepexec prepared handle OUTPUT, cursor OUTPUT, params , statement , options  
    [ , scrollopt [ , ccopt [ , rowcount ] ] ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *identificador preparado*  
 Es un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generado preparado *controlar* identificador. *identificador preparado* es necesario y devuelve **int**.  
  
 *cursor*  
 Es el identificador de cursor generado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *cursor* es un parámetro necesario que se debe proporcionar en todos los procedimientos subsiguientes que actúen en este cursor, por ejemplo sp_cursorfetch.  
  
 *params*  
 Identifica instrucciones con parámetros. El *params* definición de las variables se sustituye por marcadores de parámetros en la instrucción. *params* es un parámetro necesario que requiere un **ntext**, **nchar**, o **nvarchar** valor de entrada.  
  
> [!NOTE]  
>  Use un **ntext** cadena como entrada valor cuando *stmt* tiene parámetros y el *scrollopt* valor PARAMETERIZED_STMT es ON.  
  
 *instrucción*  
 Define el conjunto de resultados del cursor. El *instrucción* parámetro es necesario y requiere un **ntext**, **nchar** o **nvarchar** valor de entrada.  
  
> [!NOTE]  
>  Las reglas para especificar el valor de stmt son los mismos que para sp_cursoropen, con la excepción de que el *stmt* debe ser el tipo de datos string **ntext**.  
  
 *options*  
 Parámetro opcional que devuelve una descripción de las columnas del conjunto de resultados del cursor. *Opciones de* requiere lo siguiente **int** valor de entrada.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
 *scrollopt*  
 Opción de desplazamiento. *scrollopt* es un parámetro opcional que requiere uno de los siguientes **int** valores de entrada.  
  
|Valor|Descripción|  
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
  
 Debido a la posibilidad de que la opción solicitada no es adecuada para el cursor definido por  *\<stmt >* , este parámetro actúa tanto de entrada y salida. En casos como este, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asigna un tipo adecuado y modifica este valor.  
  
 *ccopt*  
 Opción de control de simultaneidad. *ccopt* es un parámetro opcional que requiere uno de los siguientes **int** valores de entrada.  
  
|Valor|Descripción|  
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
  
 Igual que con *scrollpt*, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede asignar un valor diferente al solicitado.  
  
 *rowcount*  
 Es un parámetro opcional que indica el número de filas del búfer de captura que se van a usar con AUTO_FETCH. El valor predeterminado es 20 filas. *recuento de filas* tiene un comportamiento diferente cuando se asigna como un valor de entrada frente a un valor devuelto.  
  
|Como valor de entrada|Como valor devuelto|  
|--------------------|---------------------|  
|Cuando AUTO_FETCH se especifica con cursores FAST_FORWARD *rowcount* representa el número de filas que se va a colocar en el búfer de captura.|Representa el número de filas en el conjunto de resultados. Cuando el *scrollopt* se especifica el valor AUTO_FETCH, *rowcount* devuelve el número de filas que se colocaron en el búfer de captura.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 Si *params* devuelve un valor NULL, a continuación, la instrucción no tiene parámetros.  
  
## <a name="see-also"></a>Vea también  
 [sp_cursoropen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorexecute &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorexecute-transact-sql.md)   
 [sp_cursorprepare &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorprepare-transact-sql.md)   
 [sp_cursorfetch &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
