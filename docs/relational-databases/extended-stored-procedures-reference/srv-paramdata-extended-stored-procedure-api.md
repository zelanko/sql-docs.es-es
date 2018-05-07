---
title: srv_paramdata (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: extended-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- srv_paramdata
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_paramdata
ms.assetid: 3104514d-b404-47c9-b6d7-928106384874
caps.latest.revision: 30
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d73d1e6f2cf07edf29d96ef358b085a89e427a5c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="srvparamdata-extended-stored-procedure-api"></a>srv_paramdata (API de procedimiento almacenado extendido)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Devuelve el valor de un parámetro de llamada a un procedimiento almacenado remoto. La función **srv_paraminfo** ha reemplazado a esta.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
void * srv_paramdata (  
SRV_PROC *  
srvproc  
,  
int  
n   
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 Es un puntero a la estructura SRV_PROC, que es el identificador de una conexión de cliente determinada (en este caso, el identificador que recibió la llamada al procedimiento almacenado remoto). La estructura contiene información que la biblioteca de Procedimiento almacenado extendido usa para administrar la comunicación y los datos entre la aplicación y el cliente.  
  
 *n*  
 Es el número del parámetro. El primer parámetro es número 1.  
  
## <a name="returns"></a>Devuelve  
 Un puntero al valor del parámetro. Si el parámetro *n* es NULL, no hay ningún parámetro de *n* o no hay ningún procedimiento almacenado remoto, devuelve NULL. Si el valor del parámetro es una cadena, no podría terminar en NULL. Use **srv_paramlen** para determinar la longitud de la cadena.  
  
 Esta función devuelve los valores siguientes, si el parámetro es uno de los tipos de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los datos de puntero incluyen si el puntero para el tipo de datos es válido (VP), NULL o no aplicable (N/A) y el contenido al que señalan los datos.  
  
|Nuevos tipos de datos|Longitud de datos de entrada|  
|--------------------|-----------------------|  
|BITN|**NULL:** VP, NULL<br /><br /> **CERO:** VP, NULL<br /><br /> **>=255:** N/A<br /><br /> **<255:** N/A|  
|BIGVARCHAR|**NULL:** NULL, N/A<br /><br /> **CERO:** VP, NULL<br /><br /> **>=255:** VP, 255 caracteres<br /><br /> **<255:** VP, datos reales|  
|BIGCHAR|**NULL:** NULL, N/A<br /><br /> **CERO:** VP, 255 espacios<br /><br /> **>=255:** VP, 255 caracteres<br /><br /> **<255:** VP, datos reales + relleno (hasta 255)|  
|BIGBINARY|**NULL:** NULL, N/A<br /><br /> **CERO:** VP, 255 0x00<br /><br /> **>=255:** VP, 255 bytes<br /><br /> **<255:** VP, datos reales + relleno (hasta 255)|  
|BIGVARBINARY|**NULL:** NULL, N/A<br /><br /> **ZERO:** VP, 0x00<br /><br /> **>=255:** VP, 255 bytes<br /><br /> **<255:** VP, datos reales|  
|NCHAR|**NULL:** NULL, N/A<br /><br /> **CERO:** VP, 255 espacios<br /><br /> **>=255:** VP, 255 caracteres<br /><br /> **<255:** VP, datos reales + relleno (hasta 255)|  
|NVARCHAR|**NULL:** NULL, N/A<br /><br /> **CERO:** VP, NULL<br /><br /> **>=255:** VP, 255 caracteres<br /><br /> **<255:** VP, datos reales|  
|NTEXT|**NULL:** N/A<br /><br /> **CERO:** N/A<br /><br /> **>=255:** N/A<br /><br /> **\<255:** N/A|  
  
 \*   los datos no terminan en NULL; no se produce ninguna advertencia de truncamiento en los datos >255 caracteres.  
  
## <a name="remarks"></a>Notas  
 Si conoce el nombre de parámetro, puede usar **srv_paramnumber** para obtener el número de parámetro. Para determinar si un parámetro es NULL, use **srv_paramlen**.  
  
 Cuando se usan parámetros en una llamada a un procedimiento almacenado remoto, estos pueden pasarse por nombre o por posición (sin nombre). Se produce un error si la llamada al procedimiento almacenado remoto se realiza con algunos parámetros pasados por nombre y otros pasados por posición. Si se produce un error, se sigue llamando al controlador SRV_RPC, pero aparece como si no hubiera ningún parámetro y **srv_rpcparams** devuelve 0.  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Ver también  
 [srv_rpcparams &#40;API de procedimiento almacenado extendido&#41;](../../relational-databases/extended-stored-procedures-reference/srv-rpcparams-extended-stored-procedure-api.md)  
  
  
