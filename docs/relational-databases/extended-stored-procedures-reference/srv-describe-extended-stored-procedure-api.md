---
title: srv_describe (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_describe
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_describe
ms.assetid: 2115600e-5ce7-4be0-9cd3-a1dd1fab0729
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: de810e283429f36c52258a53b22addff96be8ba1
ms.sourcegitcommit: 480961f14405dc0b096aa8009855dc5a2964f177
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/22/2019
ms.locfileid: "54419901"
---
# <a name="srvdescribe-extended-stored-procedure-api"></a>srv_describe (API de procedimiento almacenado extendido)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Define el nombre de columna y los tipos de datos de origen y destino para una columna específica de una fila.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
int srv_describe (  
SRV_PROC *  
srvproc  
,  
int  
colnumber  
,  
DBCHAR *  
column_name  
,  
int  
namelen  
,  
DBINT  
desttype  
,  
DBINT  
destlen  
,  
DBINT  
srctype  
,  
DBINT  
srclen  
,  
void *  
srcdata  
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 Es un puntero a la estructura SRV_PROC, que es el identificador de una conexión de cliente determinada (en este caso, el cliente que envía la fila). La estructura contiene toda la información que la biblioteca de API Procedimiento almacenado extendido usa para administrar las comunicaciones y los datos entre la aplicación y el cliente.  
  
 *colnumber*  
 No se admite actualmente. Las columnas se deben describir en orden. Todas las columnas se deben describir antes de llamar a **srv_sendrow**.  
  
 *column_name*  
 Especifica el nombre de la columna a la que pertenecen los datos. Este parámetro puede ser NULL porque no es preciso que una columna tenga nombre.  
  
 *namelen*  
 Especifica la longitud en bytes de *column_name*. Si *namelen* es SRV_NULLTERM, *column_name* debe terminar en NULL.  
  
 *desttype*  
 Especifica el tipo de datos de la columna de fila de destino. Éste es el tipo de datos que se envía al cliente. Se debe especificar el tipo de datos aunque los datos sean NULL; para más información, vea [Data Types &#40;Extended Stored Procedure API&#41; (Tipos de datos &#40;API de procedimiento almacenado extendido&#41;)](../../relational-databases/extended-stored-procedures-reference/data-types-extended-stored-procedure-api.md).  
  
 *destlen*  
 Especifica la longitud, en bytes, de los datos que se envían al cliente. En los tipos de datos de longitud fija que no permiten valores NULL, *destlen* se omite. En los tipos de datos de longitud variable y los tipos de datos de longitud fija que permiten valores NULL, *destlen* especifica la longitud máxima de los datos de destino.  
  
 *srctype*  
 Especifica el tipo de datos de los datos de origen.  
  
 *srclen*  
 Especifica la longitud en bytes de los datos de origen. Este valor se pasa por alto en los tipos de datos de longitud fija.  
  
 *srcdata*  
 Proporciona la dirección de los datos de origen para una columna determinada. Cuando se llama a **srv_sendrow**, busca los datos de *colnumber* en *srcdata*. Por consiguiente, no se debería liberar antes de llamar a **srv_sendrow**. La dirección de los datos de origen se puede cambiar entre las llamadas a **srv_sendrow** mediante **srv_setcoldata**. La memoria asignada a *srcdata* no se debe liberar hasta que los datos de la columna se sustituyan por otra llamada a **srv_setcoldata**, o hasta que se realice una llamada a **srv_senddone**.  
  
 Si *desttype* es SRVDECIMAL o SRVNUMERIC, el parámetro *srcdata* debe ser un puntero a una estructura DBNUMERIC o DBDECIMAL con los campos de escala y precisión de la estructura ya establecidos en los valores deseados. Puede usar DEFAULTPRECISION para especificar una precisión predeterminada y DEFAULTSCALE para especificar una escala predeterminada.  
  
## <a name="returns"></a>Devuelve  
 El número de la columna descrita. La primera columna es la columna 1. Si se produce un error, devuelve 0.  
  
## <a name="remarks"></a>Notas  
 Se debe llamar a la función **srv_describe** una vez por cada columna de la fila antes de realizar la primera llamada a **srv_sendrow**. Las columnas de una fila se pueden describir en cualquier orden.  
  
 Para cambiar la ubicación y la longitud de los datos de origen en las filas de columna antes de que se haya enviado el conjunto de resultados completo, use **srv_setcoldata** y **srv_setcollen**, respectivamente.  
  
 Para obtener una descripción de tipos de datos y conversiones de tipos de datos de API de procedimiento almacenado extendido, vea [Data Types &#40;Extended Stored Procedure API&#41; (Tipos de datos &#40;API de procedimiento almacenado extendido&#41;)](../../relational-databases/extended-stored-procedures-reference/data-types-extended-stored-procedure-api.md).  
  
 Si el nombre de columna de la aplicación se encuentra en formato Unicode, debe convertirlo a la página de códigos multibyte del servidor antes de llamar a **srv_describe**. Para más información, vea [Datos Unicode y páginas de códigos de servidor](../../relational-databases/extended-stored-procedures-programming/unicode-data-and-server-code-pages.md).  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Consulte también  
 [srv_sendrow &#40;API de procedimiento almacenado extendido&#41;](../../relational-databases/extended-stored-procedures-reference/srv-sendrow-extended-stored-procedure-api.md)   
 [srv_setutype &#40;API de procedimiento almacenado extendido&#41;](../../relational-databases/extended-stored-procedures-reference/srv-setutype-extended-stored-procedure-api.md)   
 [srv_setcoldata &#40;API de procedimiento almacenado extendido&#41;](../../relational-databases/extended-stored-procedures-reference/srv-setcoldata-extended-stored-procedure-api.md)  
  
  
