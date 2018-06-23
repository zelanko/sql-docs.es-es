---
title: srv_willconvert (API de procedimiento almacenado extendido) | Microsoft Docs
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
- srv_willconvert
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_willconvert
ms.assetid: 6f4db5fd-215a-461c-95e4-17697852733e
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d2c00fa353c633ca7d831b814bce8b07a31693fd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111140"
---
# <a name="srvwillconvert-extended-stored-procedure-api"></a>srv_willconvert (API de procedimiento almacenado extendido)
    
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
 Para obtener una descripción de cada tipo de datos, vea [Data Types &#40;Extended Stored Procedure API&#41;](data-types-extended-stored-procedure-api.md) (Tipos de datos &#40;API de procedimiento almacenado extendido&#41;).  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Vea también  
 [srv_convert &#40;API de procedimiento almacenado extendido&#41;](srv-convert-extended-stored-procedure-api.md)  
  
  