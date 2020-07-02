---
title: srv_paramsetoutput (API de procedimiento almacenado extendido)
ms.custom: seo-dt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_paramsetoutput
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_paramsetoutput
ms.assetid: f2810e19-e513-458b-8925-5756b6ee1313
author: rothja
ms.author: jroth
ms.openlocfilehash: 5b00f2fedd9c1053e332aaee8691207fbf990649
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85755954"
---
# <a name="srv_paramsetoutput-extended-stored-procedure-api"></a>srv_paramsetoutput (API de procedimiento almacenado extendido)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
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
  
## <a name="returns"></a>Devoluciones  
 Si la información de los parámetros está definida correctamente, se devuelve SUCCEED; de lo contrario, se devuelve FAIL. FAIL se devuelve cuando  
  
-   el parámetro no es un parámetro de devolución o  
  
-   el argumento *cbLen* no es válido.  
  
## <a name="remarks"></a>Comentarios  
 **Nota de seguridad** Debe revisar cuidadosamente el código fuente de los procedimientos almacenados extendidos y probar las DLL compiladas antes de instalarlas en un servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
