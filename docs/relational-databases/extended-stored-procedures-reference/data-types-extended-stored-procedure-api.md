---
title: Tipos de datos (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], data types
- data types [SQL Server], extended stored procedures
ms.assetid: 37fb86b9-8819-4387-bcdc-9616968e15ad
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a69f167e3979a975deb506270843886142244dc4
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="data-types-extended-stored-procedure-api"></a>Tipos de datos (API de procedimiento almacenado extendido)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] En su lugar, use la integración de CLR.  
  
 Para utilizar los tipos de datos de la API Procedimiento almacenado extendido, incluya el archivo de encabezado Srv.h en el programa.  
  
|Tipo de datos|Tipo de datos de SQL Server|Description|  
|---------------|--------------------------|-----------------|  
|SRVBIGBINARY|**binario**|Tipo de datos **binary**, longitud de 0 a 8000 bytes.|  
|SRVBIGCHAR|**char**|Tipo de datos **character**, longitud de 0 a 8000 bytes.|  
|SRVBIGVARBINARY|**varbinary**|Tipo de datos **binary** de longitud variable, longitud de 0 a 8000 bytes.|  
|SRVBIGVARCHAR|**varchar**|Tipo de datos **character** de longitud variable, longitud de 0 a 8000 bytes.|  
|SRVBINARY|**binario**|Tipo de datos **binary**.|  
|SRVBIT|**Bit**|Tipo de datos **bit**.|  
|SRVBITN|**bit null**|Tipo de datos **bit**, permite valores NULL.|  
|SRVCHAR|**char**|Tipo de datos **character**.|  
|SRVDATETIME|**datetime**|Tipo de datos **datetime** de 8 bytes.|  
|SRVDATETIM4|**smalldatetime**|Tipo de datos **smalldatetime** de 4 bytes.|  
|SRVDATETIMN|**datetime null**|Tipo de datos **smalldatetime** o **datetime**, permite valores NULL.|  
|SRVDECIMAL|**decimal**|Tipo de datos **decimal**.|  
|SRVDECIMALN|**decimal null**|Tipo de datos **decimal**, permite valores NULL.|  
|SRVFLT4|**real**|Tipo de datos **real** de 4 bytes.|  
|SRVFLT8|**float**|Tipo de datos **float** de 8 bytes.|  
|SRVFLTN|**real** &#124; **float null**|Tipo de datos **real** o **float**, permite valores NULL.|  
|SRVIMAGE|**imagen**|Tipo de datos **image**.|  
|SRVINT1|**tinyint**|Tipo de datos **tinyint** de 1 byte.|  
|SRVINT2|**smallint**|Tipo de datos **smallint** de 2 bytes.|  
|SRVINT4|**int**|Tipo de datos **int** de 4 bytes.|  
|SRVINTN|**tinyint** &#124; **smallint** &#124; **int null**|Tipo de datos **tinyint**, **smallint** o **int**, permite valores NULL.|  
|SRVMONEY4|**smallmoney**|Tipo de datos **smallmoney** de 4 bytes.|  
|SRVMONEY|**money**|Tipo de datos **money** de 8 bytes.|  
|SRVMONEYN|**money** &#124; **smallmoney null**|Tipo de datos **smallmoney** o **money**, permite valores NULL.|  
|SRVNCHAR|**nchar**|Tipo de datos **character** Unicode.|  
|SRVNTEXT|**ntext**|Tipo de datos **text** Unicode.|  
|SRVNUMERIC|**numeric**|Tipo de datos **numeric**.|  
|SRVNUMERICN|**numeric null**|Tipo de datos **numeric**, permite valores NULL.|  
|SRVNVARCHAR|**nvarchar**|Tipo de datos **character** Unicode de longitud variable.|  
|SRVTEXT|**texto**|Tipo de datos **text**.|  
|SRVVARBINARY|**varbinary**|Tipo de datos **binary** de longitud variable.|  
|SRVVARCHAR|**varchar**|Tipo de datos **character** de longitud variable.|  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
  
