---
title: srv_paramset (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- srv_paramset
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramset
ms.assetid: 2a509206-a1b8-4b20-b0a2-ef680cef7bd8
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 13aad0d80eafea32f0d0a7a8d1bc43b1123fd7b1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106765"
---
# <a name="srvparamset-extended-stored-procedure-api"></a>srv_paramset (API de procedimiento almacenado extendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Establece el valor de un parámetro devuelto a una llamada de un procedimiento almacenado remoto. La función **srv_paramsetoutput** ha reemplazado a esta función.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
int srv_paramset (  
SRV_PROC *  
srvproc  
,  
int  
n  
,   
void *  
data  
,  
int  
len   
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 Es un puntero a la estructura SRV_PROC, que es el identificador de una conexión de cliente determinada (en este caso, el identificador que recibió la llamada al procedimiento almacenado remoto). La estructura contiene información que la biblioteca de API de procedimiento almacenado extendido usa para administrar la comunicación y los datos entre la aplicación y el cliente.  
  
 *n*  
 Indica el número del parámetro para establecer. El primer parámetro es 1.  
  
 *data*  
 Es un puntero hacia el valor de datos que se va a devolver al cliente como el parámetro de retorno de procedimiento almacenado remoto.  
  
 *len*  
 Especifica la longitud real de los datos que se devolverán. Si el tipo de datos del parámetro es de una longitud constante y no permite valores null (por ejemplo, *srvbit* o *srvint1*), se omite *len*.  
  
## <a name="returns"></a>Devuelve  
 SUCCEED si el valor del parámetro se ha establecido correctamente; de lo contrario, FAIL. Se devuelve FAIL cuando no hay ningún procedimiento almacenado remoto actual, cuando no hay ningún parámetro *n* de procedimiento almacenado remoto, cuando el parámetro no es un parámetro de devolución y cuando el argumento *len* no es legal.  
  
 Si *len* es 0, devuelve NULL. La única manera de devolver NULL al cliente es establecer *len* en 0.  
  
 Esta función devuelve los valores siguientes, si el parámetro es uno de los tipos de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
|Nuevos tipos de datos|Devuelve la longitud de datos|  
|--------------------|------------------------|  
|`BITN`|**NULL:** *len* = 0, data = IG, RET = 0<br /><br /> **CERO:** N/A<br /><br /> **>=255:** N/A<br /><br /> **<255:** N/A|  
|`BIGVARCHAR`|**NULL:** *len* = 0, data = IG, RET = 1<br /><br /> **CERO:** *len* = IG, data = IG, RET = 0<br /><br /> **>=255:** *len* = max8k, data = valid, RET = 0<br /><br /> **<255:** *len* = <8k, data = valid, RET = 1|  
|`BIGCHAR`|**NULL:** *len* = 0, data = IG, RET = 1<br /><br /> **CERO:** *len* = IG, data = IG, RET = 0<br /><br /> **>=255:** *len* = max8k, data = valid, RET = 0<br /><br /> **<255:** *len* = <8k, data = valid, RET = 1|  
|`BIGBINARY`|**NULL:** *len* = 0, data = IG, RET = 1<br /><br /> **CERO:** *len* = IG, data = IG, RET = 0<br /><br /> **>=255:** *len* = max8k, data = valid, RET = 0<br /><br /> **<255:** *len* = <8k, data = valid, RET = 1|  
|`BIGVARBINARY`|**NULL:** *len* = 0, data = IG, RET = 1<br /><br /> **CERO:** *len* = IG, data = IG, RET = 0<br /><br /> **>=255:** *len* = max8k, data = valid, RET = 0<br /><br /> **<255:** *len* = <8k, data = valid, RET = 1|  
|NCHAR|**NULL:** *len* = 0, data = IG, RET = 1<br /><br /> **CERO:** *len* = IG, data = IG, RET = 0<br /><br /> **>=255:** *len* = max8k, data = valid, RET = 0<br /><br /> **<255:** *len* = <8k, data = valid, RET = 1|  
|NVARCHAR|**NULL:** *len* = 0, data = IG, RET = 1<br /><br /> **CERO:** *len* = IG, data = IG, RET = 0<br /><br /> **>=255:** *len* = max8k, data = valid, RET = 0<br /><br /> **<255:** *len* = <8k, data = valid, RET = 1|  
|`NTEXT`|**NULL:** *len* = IG, data = IG, RET = 0<br /><br /> **CERO:** *len* = IG, data = IG, RET = 0<br /><br /> **>=255:** *len* = IG, data = IG, RET = 0<br /><br /> **\<255:** *len* = IG, data = IG, RET = 0|  
|RET = valor devuelto de srv_paramset||  
|IG = El valor se omitirá||  
|válido = Cualquier puntero válido a datos||  
  
## <a name="remarks"></a>Notas  
 Los parámetros contienen datos que se pasan entre los clientes y la aplicación con procedimientos almacenados remotos. El cliente puede especificar ciertos parámetros como parámetros de retorno. Estos parámetros de retorno pueden contener valores que la aplicación de servidor Servicios abiertos de datos devuelve al cliente. Usar parámetros de retorno es equivalente a pasar parámetros por referencia.  
  
 No puede establecer el valor devuelto para un parámetro que no se invocó como un parámetro de retorno. Puede usar **srv_paramstatus** para determinar cómo se ha invocado al parámetro.  
  
 Esta función establece el valor devuelto para un parámetro pero realmente no envía el valor devuelto al cliente. Todos los parámetros de devolución, tanto si sus valores devueltos se han establecido con **srv_paramset** como si no, se envían automáticamente al cliente cuando se llama a **srv_senddone** con la marca de estado SRV_DONE_FINAL establecida.  
  
 Cuando se usan parámetros en una llamada a un procedimiento almacenado remoto, estos pueden pasarse por nombre o por posición (sin nombre). Se produce un error si la llamada al procedimiento almacenado remoto se realiza con algunos parámetros pasados por nombre y otros pasados por posición. Sigue llamándose al controlador SRV_RPC, pero parece como si no hubiera ningún parámetro y **srv_rpcparams** devuelve 0.  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Vea también  
 [srv_paramsetoutput &#40;API de procedimiento almacenado extendido&#41;](srv-paramsetoutput-extended-stored-procedure-api.md)  
  
  