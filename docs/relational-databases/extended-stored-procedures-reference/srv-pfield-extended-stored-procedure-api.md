---
title: srv_pfield (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: extended-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- srv_pfield
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_pfield
ms.assetid: a61e4c1f-e65b-48ea-a7d1-3e1544af389d
caps.latest.revision: 32
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 70e5a797f44167d079f9ef3375b591016055eb0e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="srvpfield-extended-stored-procedure-api"></a>srv_pfield (API de procedimiento almacenado extendido)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Devuelve información acerca de una conexión de base de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DBCHAR * srv_pfield (  
SRV_PROC *  
srvproc  
,  
int   
field  
,  
int *  
len  
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 Puntero que identifica una conexión a la base de datos.  
  
 *field*  
 Especifica los datos que se van a devolver en la conexión.  
  
|Valor|Devuelve|  
|-----------|-------------|  
|SRV_APPLNAME|El nombre de aplicación proporcionado por el cliente cuando estableció la conexión.|  
|SRV_BCPFLAG|Una marca que es TRUE si el cliente está preparando una operación de copia masiva; de lo contrario, FALSE.|  
|SRV_CLIB|El nombre de la biblioteca que permite al cliente hablar con un servidor.|  
|SRV_CPID|El identificador de proceso de cliente en el equipo de origen del cliente.|  
|SRV_HOST|El nombre del equipo del cliente proporcionado por el cliente cuando estableció la conexión.|  
|SRV_LIBVERS|La versión de la biblioteca del cliente.|  
|SRV_LSECURE|Una marca. TRUE si la conexión utilizó seguridad integrada para iniciar sesión.|  
|SRV_NETWORK_MODULE|El nombre de la DLL de Net-Library que utiliza la conexión.|  
|SRV_NETWORK_VERSION|La versión de la DLL de Net-Library que utiliza la conexión.|  
|SRV_NETWORK_CONNECTION|La cadena de conexión pasada a la DLL de la biblioteca de red usada para la conexión *srvproc* actual.|  
|SRV_PIPEHANDLE|Una cadena que contiene el identificador de canalización de un cliente conectado o NULL si el cliente está conectado en una red que no utiliza canalizaciones con nombre. Para utilizar este identificador como un identificador de canalización válido con [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, convierta esta cadena en un entero.|  
|SRV_RMTSERVER|El servidor desde el que inicia sesión el proceso de cliente. Si el inicio de sesión se realiza desde un cliente, este valor es una cadena vacía.|  
|SRV_ROWSENT|El número de filas ya enviado por *srvproc* para el conjunto actual de resultados.|  
|SRV_SPID|El identificador de subproceso de servidor de *srvproc*. En los procedimientos almacenados extendidos, este valor es igual que la columna **kpid** de **sys.sysprocesses** y puede cambiar con el tiempo.|  
|SRV_SPROC_CODEPAGE|Página de códigos que utiliza el servidor para interpretar datos multibyte.|  
|SRV_STATUS|El estado actual de *srvproc*: en ejecución o cerrado.|  
|SRV_TYPE|El tipo de conexión de *srvproc*. Si se ha devuelto el servidor, *srvproc* procede de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si se ha devuelto el cliente, *srvproc* procede de un cliente DB-Library u ODBC.|  
|SRV_USER|El nombre del usuario de la conexión.|  
|||  
  
 *len*  
 Es un puntero a una variable **int** que contiene la longitud del valor *field* devuelto. Si *len* es NULL, no se devuelve la longitud de la cadena.  
  
## <a name="returns"></a>Devuelve  
 Un puntero a una cadena terminada en NULL que contiene el valor actual del campo especificado en la estructura de SRV_PROC. Si el campo está vacío, se devuelve un puntero válido a una cadena vacía y *len* contiene 0. Si el campo es desconocido, se devuelve NULL y *len* contiene el valor -1.  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para más información sobre la revisión y las pruebas de seguridad, vea [Security Developer Center](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
  
