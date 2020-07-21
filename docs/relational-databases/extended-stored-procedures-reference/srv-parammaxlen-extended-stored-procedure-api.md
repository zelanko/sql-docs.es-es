---
title: srv_parammaxlen (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_parammaxlen
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_parammaxlen
ms.assetid: 49bfc29d-f76a-4963-b0e6-b8532dfda850
author: rothja
ms.author: jroth
ms.openlocfilehash: 936dddfc9faecc48f61ac61e390aca7b82533314
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85756706"
---
# <a name="srv_parammaxlen-extended-stored-procedure-api"></a>srv_parammaxlen (API de procedimiento almacenado extendido)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
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
  
## <a name="returns"></a>Devoluciones  
 La longitud máxima, en bytes, de los datos del parámetro. Si no existe ningún parámetro *n* o no hay ningún procedimiento almacenado remoto, devuelve -1.  
  
 Esta función devuelve los valores siguientes, si el parámetro es uno de los siguientes [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos.  
  
|Nuevos tipos de datos|Longitud de datos de entrada|  
|--------------------|-----------------------|  
|**BITN**|**NULL:** 1<br /><br /> **Cero:** 1<br /><br /> **>= 255:** N/A<br /><br /> **<255:** N/A|  
|**BIGVARCHAR**|**NULL:** 255<br /><br /> **CERO:** 255<br /><br /> **>= 255:** 255<br /><br /> **<255:** 255|  
|**BIGCHAR**|**NULL:** 255<br /><br /> **CERO:** 255<br /><br /> **>= 255:** 255<br /><br /> **<255:** 255|  
|**BIGBINARY**|**NULL:** 255<br /><br /> **CERO:** 255<br /><br /> **>= 255:** 255<br /><br /> **<255:** 255|  
|**BIGVARBINARY**|**NULL:** 255<br /><br /> **CERO:** 255<br /><br /> **>= 255:** 255<br /><br /> **<255:** 255|  
|**NCHAR**|**NULL:** 255<br /><br /> **CERO:** 255<br /><br /> **>= 255:** 255<br /><br /> **<255:** 255|  
|**NVARCHAR**|**NULL:** 255<br /><br /> **CERO:** 255<br /><br /> **>= 255:** 255<br /><br /> **<255:** 255|  
|**NTEXT**|**Null:** -1<br /><br /> **CERO:** -1<br /><br /> **>= 255:** -1<br /><br /> ** \< 255:** -1|  
  
## <a name="remarks"></a>Comentarios  
 Cada parámetro de procedimiento almacenado remoto tiene una longitud de datos real y una longitud máxima. En los tipos de datos de longitud fija estándar que no permiten valores NULL, las longitudes real y máxima son las mismas. En los tipos de datos de longitud variable, las longitudes pueden variar. Por ejemplo, un parámetro declarado como **varchar(30)** puede tener datos con una longitud de solo 10 bytes. La longitud real del parámetro es 10 y su longitud máxima es 30. La función **srv_parammaxlen** obtiene la longitud máxima de los datos de un procedimiento almacenado remoto. Para obtener la longitud real de un parámetro, use **srv_paramlen**.  
  
 Cuando se usan parámetros en una llamada a un procedimiento almacenado remoto, estos pueden pasarse por nombre o por posición (sin nombre). Se produce un error si la llamada al procedimiento almacenado remoto se realiza con algunos parámetros pasados por nombre y otros pasados por posición. Sigue llamándose al controlador SRV_RPC, pero parece como si no hubiera ningún parámetro y **srv_rpcparams** devuelve 0.  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Consulte también  
 [srv_paraminfo API de procedimiento almacenado extendido &#40;&#41;](../../relational-databases/extended-stored-procedures-reference/srv-paraminfo-extended-stored-procedure-api.md)   
 [srv_rpcparams &#40;API de procedimiento almacenado extendido&#41;](../../relational-databases/extended-stored-procedures-reference/srv-rpcparams-extended-stored-procedure-api.md)  
  
  
