---
title: srv_paraminfo (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_paraminfo
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_paraminfo
ms.assetid: ee2afd4e-0d91-462b-9403-98d481546330
author: rothja
ms.author: jroth
ms.openlocfilehash: 85efd235861522754cbcdc209d6cf28558907d76
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68058775"
---
# <a name="srv_paraminfo-extended-stored-procedure-api"></a>srv_paraminfo (API de procedimiento almacenado extendido)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Devuelve información sobre un parámetro. Esta función reemplaza a las siguientes funciones: [srv_paramtype](../../relational-databases/extended-stored-procedures-reference/srv-paramtype-extended-stored-procedure-api.md), [srv_paramlen](../../relational-databases/extended-stored-procedures-reference/srv-paramlen-extended-stored-procedure-api.md), [srv_parammaxlen](../../relational-databases/extended-stored-procedures-reference/srv-parammaxlen-extended-stored-procedure-api.md) y [srv_paramdata](../../relational-databases/extended-stored-procedures-reference/srv-paramdata-extended-stored-procedure-api.md). **srv_paraminfo** admite los tipos de datos de [Tipos de datos](../../relational-databases/extended-stored-procedures-reference/data-types-extended-stored-procedure-api.md) y datos de longitud cero.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
int srv_paraminfo (  
SRV_PROC *  
srvproc  
,  
int  
n  
,  
BYTE *  
pbType  
,  
ULONG *  
pcbMaxLen  
,  
ULONG *  
pcbActualLen  
,  
BYTE *  
pbData  
,  
BOOL *  
pfNull  
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 Un identificador de una conexión cliente.  
  
 *n*  
 El número ordinal del parámetro que se va a definir. El primer parámetro es 1.  
  
 *pbType*  
 El tipo de datos del parámetro.  
  
 *pcbMaxLen*  
 Puntero a la longitud máxima del parámetro.  
  
 *pcbActualLen*  
 Puntero a la longitud real del parámetro. Un valor de 0 (\**pcbActualLen* == 0) significa datos de longitud cero si **pfNull* está establecido en FALSE.  
  
 *pbData*  
 Puntero al búfer para los datos de parámetro. Si *pbData* no es NULL, la API de procedimiento almacenado extendido escribe \**pcbActualLen* bytes de datos en \**pbData*. Si *pbData* es NULL, no se escriben datos en \**pbData*, pero la función devuelve \**pbType*, \**pcbMaxLen*, \**pcbActualLen* y **pfNull*. La aplicación debe administrar la memoria para este búfer.  
  
 *pfNull*  
 Puntero a una marca nula. **pfNull* se establece en TRUE si el valor del parámetro es NULL.  
  
## <a name="returns"></a>Devuelve  
 Si la información de los parámetros se obtiene correctamente, se devuelve SUCCEED; de lo contrario, se devuelve FAIL. Se devuelve FAIL cuando no hay ningún procedimiento almacenado remoto actual y cuando no hay ningún parámetro *n* de procedimiento almacenado remoto.  
  
## <a name="remarks"></a>Observaciones  
 **Nota de seguridad** Debe revisar cuidadosamente el código fuente de los procedimientos almacenados extendidos y probar las DLL compiladas antes de instalarlas en un servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Consulte también  
 [Referencia del programador de procedimientos almacenados extendidos](../../relational-databases/extended-stored-procedures-reference/database-engine-extended-stored-procedures-reference.md)  
  
  
