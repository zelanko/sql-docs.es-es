---
title: srv_pfieldex (API de procedimiento almacenado extendido) | Microsoft Docs
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
- srv_pfieldex
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_pfieldex
ms.assetid: d4e9a34b-b3a3-434f-8556-768bd20d145a
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 77ce8845cce63eb942c57c45d60dc56ce500f73b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112005"
---
# <a name="srvpfieldex-extended-stored-procedure-api"></a>srv_pfieldex (API de procedimiento almacenado extendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Devuelve un puntero a los datos que contienen el campo SRV_PROC solicitado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
void *srv_pfieldex(SRV_PROC *   
srvproc  
, int   
field  
, int *   
len  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 Es un puntero a la estructura SRV_PROC que es el identificador de una conexión cliente determinada. La estructura contiene información que la biblioteca de API de procedimiento almacenado extendido usa para administrar la comunicación y los datos entre la aplicación y el cliente.  
  
 *field*  
 Especifica el campo *srvproc* que se va a devolver.  
  
|Campo|Descripción|Tipo devuelto|  
|-----------|-----------------|------------------|  
|SRV_MSGLCID|LCID de mensaje de la sesión actual.|ULONG*|  
|SRV_INSTANCENAME|Nombre de instancia (si tiene nombre); de lo contrario, devuelve NULL.|WCHAR*|  
  
 *len*  
 Es un puntero a una variable **int** que contiene la longitud del valor *field* devuelto en bytes. Si *len* es NULL, no se devuelve la longitud. Cuando se devuelve NULL **len* se establece en 0.  
  
## <a name="returns"></a>Devuelve  
 Un puntero a los datos cuyo tipo depende de *field*. Se devuelve NULL cuando *len* o *srvproc* son NULL. Si *field* es desconocido, se devuelve NULL. Cuando se devuelve NULL **len* se establece en 0.  
  
> [!IMPORTANT]  
>  El búfer que se devuelve desde el servidor debe ser de solo lectura. Si no es así, es posible que el estado del servidor esté dañado.  
  
## <a name="remarks"></a>Notas  
 **Nota de seguridad** Debe revisar cuidadosamente el código fuente de los procedimientos almacenados extendidos y probar las DLL compiladas antes de instalarlas en un servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
  