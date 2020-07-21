---
title: srv_willconvert (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0d9ba59555ce590c460854481d916e30ef942cba
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85755803"
---
# <a name="srv_willconvert-extended-stored-procedure-api"></a>srv_willconvert (API de procedimiento almacenado extendido)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
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
  
## <a name="returns"></a>Devoluciones  
 TRUE si se admite la conversión del tipo de datos; FALSE si no se admite la conversión del tipo de datos.  
  
## <a name="remarks"></a>Comentarios  
 Para obtener una descripción de cada tipo de datos, vea [Data Types &#40;Extended Stored Procedure API&#41;](../../relational-databases/extended-stored-procedures-reference/data-types-extended-stored-procedure-api.md) (Tipos de datos &#40;API de procedimiento almacenado extendido&#41;).  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](https://www.microsoft.com/msrc?rtc=1).  
  
## <a name="see-also"></a>Consulte también  
 [srv_convert &#40;API de procedimiento almacenado extendido&#41;](../../relational-databases/extended-stored-procedures-reference/srv-convert-extended-stored-procedure-api.md)  
  
  
