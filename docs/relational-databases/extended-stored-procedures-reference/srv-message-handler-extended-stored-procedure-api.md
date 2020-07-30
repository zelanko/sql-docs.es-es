---
title: srv_message_handler (API de procedimiento almacenado extendido)
description: Obtenga información acerca de srv_message_handler y cómo llama al controlador de mensajes de la API de procedimiento almacenado extendido instalado.
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_message_handler
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_message_handler
ms.assetid: 41bcd057-436f-4fa8-8293-fc8057a30877
author: rothja
ms.author: jroth
ms.openlocfilehash: 2edc96558c00b43dfe9d9b346ad75c32b42af1cd
ms.sourcegitcommit: 75f767c7b1ead31f33a870fddab6bef52f99906b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87332361"
---
# <a name="srv_message_handler-extended-stored-procedure-api"></a>srv_message_handler (API de procedimiento almacenado extendido)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Llama al controlador de mensajes de la API Procedimiento almacenado extendido instalado. Esta función se utiliza normalmente para llamar a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un procedimiento almacenado extendido para registrar un error (definido por el procedimiento almacenado extendido) en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] archivo de registro de errores o en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] registro de aplicación de Windows.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
int srv_message_handler (  
SRV_PROC *  
srvproc  
,  
int  
errornum  
,  
BYTE   
severity  
,  
BYTE  
state  
,  
int  
oserrnum  
,  
char *  
errtext  
,  
int  
errtextlen  
,  
char *  
oserrtext  
,  
int  
oserrtextlen  
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 Es un puntero a la estructura SRV_PROC que es el identificador de una conexión cliente determinada. El parámetro *srvproc* contiene información que se usa para administrar la comunicación y los datos entre la aplicación y el cliente.  
  
 *errornum*  
 Es un número de error definido por el procedimiento almacenado extendido. Este número debe estar comprendido entre 50.001 y 2.147.483.647.  
  
 *severity*  
 Es un valor de gravedad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estándar para el error. Este número debe estar comprendido entre 0 y 24.  
  
 *state*  
 Es un valor de estado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el error.  
  
 *oserrnum*  
 Es el número de error del sistema operativo. Este argumento se pasa por alto.  
  
 *errtext*  
 Es la descripción del error del procedimiento almacenado extendido *errornum*.  
  
 *errtextlen*  
 Es la longitud de la cadena del error del procedimiento almacenado extendido *errtext*.  
  
 *oserrtext*  
 Es la descripción del error del sistema operativo *oserrnum*. Este argumento se pasa por alto.  
  
 *oserrtextlen*  
 Es la longitud de la cadena de error del sistema operativo *oserrtext*.  
  
## <a name="returns"></a>Devuelve  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Observaciones  
 La función **srv_message_handler** permite que un procedimiento almacenado extendido se integre con las características centralizadas de registro e informe de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se pueden establecer alertas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para eventos a partir de los procedimientos almacenados extendidos; el Agente SQL Server supervisa estas condiciones de alerta.  
  
 Si el mensaje de error es más largo, se trunca a 412 bytes.  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](https://msdn.microsoft.com/security/).  
  
  
