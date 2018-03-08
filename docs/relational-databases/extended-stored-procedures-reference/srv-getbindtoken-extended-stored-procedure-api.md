---
title: srv_getbindtoken (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- srv_getbindtoken
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_getbindtoken
ms.assetid: c947d011-08ac-4fb8-b925-3da6e0999277
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a7deeadc2003fa6dd4dba53e11efc2c135240696
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="srvgetbindtoken-extended-stored-procedure-api"></a>srv_getbindtoken (API de procedimiento almacenado extendido)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] En su lugar, use la integración de CLR.  
  
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
  
## <a name="remarks"></a>Notas  
  
### <a name="to-bind-an-extended-stored-procedure-session-to-the-client-session-that-called-it-so-they-share-the-same-transaction-lock-space"></a>Para enlazar una sesión de procedimiento almacenado extendido a la sesión del cliente que lo llamó de modo que compartan el mismo espacio de bloqueo de transacción  
  
1.  El procedimiento almacenado extendido llama a **svr_getbindtoken** para obtener el token de enlace de la transacción actual en la sesión. El token se devuelve en el parámetro *bindtoken* determinado.  
  
2.  El procedimiento almacenado extendido abre nuevas sesiones con el mismo servidor. Dentro de esa sesión, el procedimiento almacenado extendido usa el token de enlace con **sp_bindsession** para enlazar la nueva sesión a la misma transacción. El procedimiento almacenado extendido puede crear varias sesiones y enlazar todas las sesiones a la misma transacción.  
  
3.  Una sesión enlazada se desenlaza cuando finaliza el procedimiento almacenado externo o cuando se llama a **sp_bindsession** con una cadena vacía.  
  
    > [!NOTE]  
    >  Solo una sesión enlazada puede tener cada vez acceso a una conexión compartida. Si una sesión está ejecutando actualmente una instrucción en el servidor o tiene resultados pendientes del servidor, ninguna otra sesión que comparta la misma conexión de enlace puede obtener acceso al servidor hasta que la sesión actual haya finalizado de ejecutar la instrucción actual. Si una sesión intenta obtener acceso a la conexión mientras el servidor no está disponible, se devolverá un error a la sesión en conflicto que indique que la conexión se está usando y que se debería reintentar la sesión más tarde.  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Ver también  
 [sp_bindsession &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindsession-transact-sql.md)   
 [sp_getbindtoken &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql.md)  
  
  
