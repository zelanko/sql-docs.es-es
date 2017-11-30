---
title: srv_paraminfo (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: srv_paraminfo
apilocation: opends60.dll
apitype: DLLExport
dev_langs: C++
helpviewer_keywords: srv_paraminfo
ms.assetid: ee2afd4e-0d91-462b-9403-98d481546330
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4fc82b7b7aebbfaaaef946ce7f5f42e8a4398c5d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="srvparaminfo-extended-stored-procedure-api"></a>srv_paraminfo (API de procedimiento almacenado extendido)
    
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
 Si la información de los parámetros se obtiene correctamente, se devuelve SUCCEED; de lo contrario, se devuelve FAIL. Se devuelve FAIL cuando no hay ningún procedimiento almacenado remoto actual y cuando no hay *n*ésimo parámetro de procedimiento almacenado remoto.  
  
## <a name="remarks"></a>Comentarios  
 **Nota de seguridad** Debe revisar cuidadosamente el código fuente de los procedimientos almacenados extendidos y probar las DLL compiladas antes de instalarlas en un servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del programador de procedimientos almacenados extendidos](../../relational-databases/extended-stored-procedures-reference/database-engine-extended-stored-procedures-reference.md)  
  
  
