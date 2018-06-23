---
title: srv_paramsetoutput (API de procedimiento almacenado extendido) | Microsoft Docs
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
- srv_paramsetoutput
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramsetoutput
ms.assetid: f2810e19-e513-458b-8925-5756b6ee1313
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 182fc8b68a6b3b4673317a3524c1c92f51898342
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111566"
---
# <a name="srvparamsetoutput-extended-stored-procedure-api"></a>srv_paramsetoutput (API de procedimiento almacenado extendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Establece el valor de un parámetro de devolución. Esta función reemplaza a **srv_paramset**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
int srv_paramsetoutput (  
SRV_PROC *  
srvproc  
,  
int  
n  
,  
BYTE *  
pbData  
,  
ULONG   
cbLen  
,  
BOOL  
fNull   
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 Es un identificador de una conexión cliente.  
  
 *n*  
 Es el número ordinal del parámetro que se va a definir. El primer parámetro es 1.  
  
 *pbData*  
 Es un puntero al valor de datos que se va a devolver al cliente como parámetro de devolución del procedimiento.  
  
 *cbLen*  
 Es la longitud real de los datos que se van a devolver. Si el tipo de datos del parámetro especifica valores de una longitud constante y no permite valores null (por ejemplo, *srvbit* o *srvint1*), se omite *cbLen*. Un valor de 0 indica datos de longitud cero si *fNull* es FALSE.  
  
 *fNull*  
 Es una marca que indica si el valor del parámetro de devolución es NULL. Establezca esta marca en TRUE si el parámetro debe estar establecido en NULL. El valor predeterminado es FALSE. Si *fNull* está establecido en TRUE, *cbLen* debe establecerse en 0 o se produce un error en la función.  
  
## <a name="returns"></a>Devuelve  
 Si la información de los parámetros está definida correctamente, se devuelve SUCCEED; de lo contrario, se devuelve FAIL. FAIL se devuelve cuando  
  
-   el parámetro no es un parámetro de devolución o  
  
-   el argumento *cbLen* no es válido.  
  
## <a name="remarks"></a>Notas  
 **Nota de seguridad** Debe revisar cuidadosamente el código fuente de los procedimientos almacenados extendidos y probar las DLL compiladas antes de instalarlas en un servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
  