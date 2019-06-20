---
title: srv_getbindtoken (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_getbindtoken
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_getbindtoken
ms.assetid: c947d011-08ac-4fb8-b925-3da6e0999277
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: dec2e73de3c4c3525b29b44b7c4563a7fd6887ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127302"
---
# <a name="srvgetbindtoken-extended-stored-procedure-api"></a>srv_getbindtoken (API de procedimiento almacenado extendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Obtiene un token de enlace de la transacción en la sesión del cliente actual que invoca el procedimiento almacenado extendido.  
  
 Luego el procedimiento almacenado extendido puede usar **sp_bindsession** para enlazar cualquier sesión nueva que cree con el mismo servidor a la transacción existente, de manera que la nueva sesión pueda compartir el mismo espacio de bloqueo de transacción con la sesión cliente que ha invocado el procedimiento almacenado extendido.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
int srv_getbindtoken (  
SRV_PROC*  
srvproc  
,  
char*  
bindtoken  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 Es un puntero a la estructura SRV_PROC que es el identificador de una conexión cliente determinada. La estructura contiene toda la información que la biblioteca de API Procedimiento almacenado extendido usa para administrar las comunicaciones y los datos entre la aplicación y el cliente.  
  
 *bindtoken*  
 Es un puntero a un búfer donde se copiará el token de enlace. El token de enlace se representa como una cadena terminada en NULL. El búfer que especifica debería tener por lo menos 255 bytes de longitud.  
  
## <a name="returns"></a>Devuelve  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Comentarios  
  
### <a name="to-bind-an-extended-stored-procedure-session-to-the-client-session-that-called-it-so-they-share-the-same-transaction-lock-space"></a>Para enlazar una sesión de procedimiento almacenado extendido a la sesión del cliente que lo llamó de modo que compartan el mismo espacio de bloqueo de transacción  
  
1.  El procedimiento almacenado extendido llama a **svr_getbindtoken** para obtener el token de enlace de la transacción actual en la sesión. El token se devuelve en el parámetro *bindtoken* determinado.  
  
2.  El procedimiento almacenado extendido abre nuevas sesiones con el mismo servidor. Dentro de esa sesión, el procedimiento almacenado extendido usa el token de enlace con **sp_bindsession** para enlazar la nueva sesión a la misma transacción. El procedimiento almacenado extendido puede crear varias sesiones y enlazar todas las sesiones a la misma transacción.  
  
3.  Una sesión enlazada se desenlaza cuando finaliza el procedimiento almacenado externo o cuando se llama a **sp_bindsession** con una cadena vacía.  
  
    > [!NOTE]  
    >  Solo una sesión enlazada puede tener cada vez acceso a una conexión compartida. Si una sesión está ejecutando actualmente una instrucción en el servidor o tiene resultados pendientes del servidor, ninguna otra sesión que comparta la misma conexión de enlace puede obtener acceso al servidor hasta que la sesión actual haya finalizado de ejecutar la instrucción actual. Si una sesión intenta obtener acceso a la conexión mientras el servidor no está disponible, se devolverá un error a la sesión en conflicto que indique que la conexión se está usando y que se debería reintentar la sesión más tarde.  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Vea también  
 [sp_bindsession &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-bindsession-transact-sql)   
 [sp_getbindtoken &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql)  
  
  
