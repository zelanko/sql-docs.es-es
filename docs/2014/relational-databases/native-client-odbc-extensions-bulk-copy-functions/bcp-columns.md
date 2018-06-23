---
title: bcp_columns | Documentos de Microsoft
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
- bcp_columns
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_columns function
ms.assetid: 5376f6fe-9508-439a-8c66-778d77f19ac3
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f2f7cb508f9b7715abbc2505f38b30795df2d142
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105363"
---
# <a name="bcpcolumns"></a>bcp_columns
  Establece el número total de columnas del archivo de usuario para su uso con una copia masiva a o de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [bcp_setbulkmode](bcp-setbulkmode.md) puede usarse en lugar de bcp_columns y [bcp_colfmt](bcp-colfmt.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RETCODE bcp_columns (  
HDBC   
hdbc  
,  
INT   
nColumns  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *HDBC*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
 *nColumns*  
 Es el número total de columnas en el archivo de usuario. Incluso si se está preparando para la copia masiva de datos del archivo de usuario para un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de tabla y no desea copiar todas las columnas del archivo de usuario, debe establecer *nColumns* al número total de columnas del archivo de usuario.  
  
## <a name="returns"></a>Devuelve  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Notas  
 Esta función se puede llamar solo después [bcp_init](bcp-init.md) se ha llamado con un nombre de archivo válido.  
  
 Solo debe llamar a esta función si piensa utilizar un formato de archivo de usuario que difiere del valor predeterminado. Para obtener más información acerca de la descripción del formato predeterminado del archivo de usuario, consulte **bcp_init**.  
  
 Después de llamar a `bcp_columns`, debe llamar a [bcp_colfmt](bcp-colfmt.md)para cada columna en el archivo de usuario para definir completamente un formato de archivo personalizado.  
  
## <a name="see-also"></a>Vea también  
 [Funciones de copia masiva](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  