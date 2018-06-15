---
title: sp_cursorexecute (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursorexecute
- sp_cursorexecute_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_execute
ms.assetid: 6a204229-0a53-4617-a57e-93d4afbb71ac
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: cae17034cdcc2d048e539961bf07971acb3b3410
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33238795"
---
# <a name="spcursorexecute-transact-sql"></a>sp_cursorexecute (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea y rellena un cursor basado en el plan de ejecución creado por sp_cursorprepare. Este procedimiento, junto con sp_cursorprepare, tiene la misma función que sp_cursoropen, pero se divide en dos fases. sp_cursorexecute se invoca especificando el identificador = 4 en un paquete de flujo TDS.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_cursorexecute prepared_handle, cursor  
    [ , scrollopt[ OUTPUT ]  
    [ , ccopt[ OUTPUT ]  
    [ ,rowcount OUTPUT [ ,bound param][,...n]]]]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *prepared_handle*  
 Es la instrucción preparada *controlar* valor devuelto por sp_cursorprepare. *prepared_handle* es un parámetro necesario que requiere un **int** valor de entrada.  
  
 *cursor*  
 Es el identificador del cursor generado por SQL Server. *cursor* es un parámetro necesario que se debe proporcionar en todos los procedimientos subsiguientes que actúen en el cursor, como sp_cursorfetch  
  
 *scrollopt*  
 Opción de desplazamiento. *scrollopt* es un parámetro opcional que requiere un **int** valor de entrada. El sp_cursorexecute*scrollopt* parámetro tiene las mismas opciones que para sp_cursoropen.  
  
> [!NOTE]  
>  No se admite el valor PARAMETERIZED_STMT.  
  
> [!IMPORTANT]  
>  Si un *scrollopt* valor no se especifica, el valor predeterminado es KEYSET con independencia de *scrollopt* valor especificado en sp_cursorprepare.  
  
 *ccopt*  
 Opción de control de divisa. *ccopt* es un parámetro opcional que requiere un **int** valor de entrada. El sp_cursorexecute*ccopt* parámetro tiene las mismas opciones que para sp_cursoropen.  
  
> [!IMPORTANT]  
>  Si un *ccopt* valor no se especifica, el valor predeterminado es OPTIMISTIC, con independencia de *ccopt* valor especificado en sp_cursorprepare.  
  
 *recuento de filas*  
 Es un parámetro opcional que indica el número de filas del búfer de captura que se van a usar con AUTO_FETCH. El valor predeterminado es 20 filas. *recuento de filas* tiene un comportamiento diferente cuando se asigna como un valor de entrada frente a un valor devuelto.  
  
|Como valor de entrada|Como valor devuelto|  
|--------------------|---------------------|  
|Cuando AUTO_FETCH se especifica con cursores FAST_FORWARD *rowcount* representa el número de filas que se va a colocar en el búfer de captura.|Representa el número de filas en el conjunto de resultados. Cuando el *scrollopt* se especifica el valor AUTO_FETCH, *rowcount* devuelve el número de filas que se colocaron en el búfer de captura.|  
  
 *bound_param*  
 Indica el uso opcional de parámetros adicionales.  
  
> [!NOTE]  
>  Cualquier parámetro después del quinto se pasa como parámetro de entrada al plan de instrucción.  
  
## <a name="code-return-value"></a>Valor del código de retorno  
 *recuento de filas* puede devolver los valores siguientes.  
  
|Value|Description|  
|-----------|-----------------|  
|-1|Número de filas desconocido.|  
|-n|Un rellenado asincrónico está en vigor.|  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="scrollopt-and-ccopt-parameters"></a>Parámetros ccopt y scrollopt  
 *scrollopt* y *ccopt* son útiles cuando se reemplazan los planes almacenados en caché para la caché del servidor, lo que significa que se debe volver a compilar el identificador preparado que identifica la instrucción. El *scrollopt* y *ccopt* valores de parámetro deben coincidir con los valores enviados en la solicitud original a sp_cursorprepare.  
  
> [!NOTE]  
>  PARAMETERIZED_STMT no debe asignarse a *scrollopt*.  
  
 Si no se pueden proporcionar los valores correspondientes, se provocará la recompilación de los planes, impidiéndose las operaciones de preparación y ejecución.  
  
## <a name="rpc-and-tds-considerations"></a>Consideraciones sobre RPC y TDS  
 La marca de entrada RPC RETURN_METADATA puede establecerse en 1 para solicitar que se devuelvan los metadatos de la lista de selección del cursor en el flujo de TDS.  
  
## <a name="see-also"></a>Vea también  
 [sp_cursoropen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorfetch &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
