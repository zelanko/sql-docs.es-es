---
title: srv_parammaxlen (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- srv_parammaxlen
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_parammaxlen
ms.assetid: 49bfc29d-f76a-4963-b0e6-b8532dfda850
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f6613a8ad4e907444de66fd8a09777b1704f48a2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200355"
---
# <a name="srvparammaxlen-extended-stored-procedure-api"></a>srv_parammaxlen (API de procedimiento almacenado extendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Devuelve la longitud máxima de datos de un parámetro de llamada a un procedimiento almacenado remoto. La función **srv_paraminfo** ha reemplazado a esta.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
int srv_parammaxlen (  
SRV_PROC *  
srvproc  
,  
int  
n   
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 Es un puntero a la estructura SRV_PROC, que es el identificador de una conexión de cliente determinada (en este caso, el identificador que recibió la llamada al procedimiento almacenado remoto). La estructura contiene información que la biblioteca de API de procedimiento almacenado extendido usa para administrar la comunicación y los datos entre la aplicación y el cliente.  
  
 *n*  
 Indica el número del parámetro. El primer parámetro es 1.  
  
## <a name="returns"></a>Devuelve  
 La longitud máxima, en bytes, de los datos del parámetro. Si no existe ningún parámetro *n* o no hay ningún procedimiento almacenado remoto, devuelve -1.  
  
 Esta función devuelve los valores siguientes, si el parámetro es uno de los siguientes tipos de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nuevos tipos de datos|Longitud de datos de entrada|  
|--------------------|-----------------------|  
|`BITN`|**NULL:** 1<br /><br /> **CERO:** 1<br /><br /> **>=255:** N/A<br /><br /> **<255:** N/A|  
|`BIGVARCHAR`|**NULL:** 255<br /><br /> **CERO:** 255<br /><br /> **>=255:** 255<br /><br /> **<255:** 255|  
|`BIGCHAR`|**NULL:** 255<br /><br /> **CERO:** 255<br /><br /> **>=255:** 255<br /><br /> **<255:** 255|  
|`BIGBINARY`|**NULL:** 255<br /><br /> **CERO:** 255<br /><br /> **>=255:** 255<br /><br /> **<255:** 255|  
|`BIGVARBINARY`|**NULL:** 255<br /><br /> **CERO:** 255<br /><br /> **>=255:** 255<br /><br /> **<255:** 255|  
|`NCHAR`|**NULL:** 255<br /><br /> **CERO:** 255<br /><br /> **>=255:** 255<br /><br /> **<255:** 255|  
|`NVARCHAR`|**NULL:** 255<br /><br /> **CERO:** 255<br /><br /> **>=255:** 255<br /><br /> **<255:** 255|  
|`NTEXT`|**NULL:** -1<br /><br /> **CERO:** -1<br /><br /> **>=255:** -1<br /><br /> **\<255:** -1|  
  
## <a name="remarks"></a>Notas  
 Cada parámetro de procedimiento almacenado remoto tiene una longitud de datos real y una longitud máxima. En los tipos de datos de longitud fija estándar que no permiten valores NULL, las longitudes real y máxima son las mismas. En los tipos de datos de longitud variable, las longitudes pueden variar. Por ejemplo, un parámetro declarado como **varchar(30)** puede tener datos con una longitud de solo 10 bytes. La longitud real del parámetro es 10 y su longitud máxima es 30. La función **srv_parammaxlen** obtiene la longitud máxima de los datos de un procedimiento almacenado remoto. Para obtener la longitud real de un parámetro, use **srv_paramlen**.  
  
 Cuando se usan parámetros en una llamada a un procedimiento almacenado remoto, estos pueden pasarse por nombre o por posición (sin nombre). Se produce un error si la llamada al procedimiento almacenado remoto se realiza con algunos parámetros pasados por nombre y otros pasados por posición. Sigue llamándose al controlador SRV_RPC, pero parece como si no hubiera ningún parámetro y **srv_rpcparams** devuelve 0.  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Vea también  
 [srv_paraminfo &#40;API de procedimiento almacenado extendido&#41;](srv-paraminfo-extended-stored-procedure-api.md)   
 [srv_rpcparams &#40;API de procedimiento almacenado extendido&#41;](srv-rpcparams-extended-stored-procedure-api.md)  
  
  