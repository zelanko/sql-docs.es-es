---
title: srv_willconvert (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
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
- srv_willconvert
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_willconvert
ms.assetid: 6f4db5fd-215a-461c-95e4-17697852733e
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e22955b073e17802be37e95ddf41659766da0662
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="srvwillconvert-extended-stored-procedure-api"></a>srv_willconvert (API de procedimiento almacenado extendido)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Determina si está disponible una conversión de tipos de datos concreta en la Biblioteca ODS.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL srv_willconvert (  
int  
srctype  
,  
int  
desttype   
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *srctype*  
 Indica el tipo de los datos que se van a convertir. Este parámetro puede ser cualquiera de los tipos de datos de la API Procedimiento almacenado extendido.  
  
 *desttype*  
 Indica el tipo de datos al que se convierten los datos de origen. Este parámetro puede ser cualquiera de los tipos de datos de la API Procedimiento almacenado extendido.  
  
## <a name="returns"></a>Devuelve  
 TRUE si se admite la conversión del tipo de datos; FALSE si no se admite la conversión del tipo de datos.  
  
## <a name="remarks"></a>Notas  
 Para obtener una descripción de cada tipo de datos, vea [Data Types &#40;Extended Stored Procedure API&#41;](../../relational-databases/extended-stored-procedures-reference/data-types-extended-stored-procedure-api.md) (Tipos de datos &#40;API de procedimiento almacenado extendido&#41;).  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Ver también  
 [srv_convert &#40;API de procedimiento almacenado extendido&#41;](../../relational-databases/extended-stored-procedures-reference/srv-convert-extended-stored-procedure-api.md)  
  
  
