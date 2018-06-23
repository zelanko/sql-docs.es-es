---
title: bcp_colptr | Documentos de Microsoft
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
- bcp_colptr
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_colptr function
ms.assetid: 02ece13e-1da3-4f9d-b860-3177e43d2471
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c0fa867ec82520f1dcc0def040d7a8edf8a2a713
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199356"
---
# <a name="bcpcolptr"></a>bcp_colptr
  Establece la dirección de datos de la variable de programa para la copia actual en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RETCODE bcp_colptr (  
HDBC   
hdbc  
,  
LPCBYTE   
pData  
,  
INT   
idxServerCol  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *HDBC*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
 *pData*  
 Es un puntero a los datos que van a copiarse. Si el tipo de datos enlazado es el tipo de valor grande (como SQLTEXT o SQLIMAGE), *pData* puede ser NULL. Un valor NULL *pData* indica valores de datos largos se enviarán a SQL Server en fragmentos utilizando [bcp_moretext](bcp-moretext.md).  
  
 Si *pData* se establece en NULL y la columna correspondiente al campo enlazado no es un tipo de valor grande, **bcp_colptr** se produce un error.  
  
 Para obtener más información sobre los tipos de valores grandes, consulte [bcp_bind](bcp-bind.md)**.**  
  
 *idxServerCol*  
 Es la posición ordinal de la columna en la tabla de base de datos en la que se copian los datos. La primera columna de una tabla es la columna 1. La posición ordinal de una columna se notifica mediante [SQLColumns](../native-client-odbc-api/sqlcolumns.md).  
  
## <a name="returns"></a>Devuelve  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Notas  
 El **bcp_colptr** función le permite cambiar la dirección de origen de datos de una determinada columna al copiar los datos a SQL Server con [bcp_sendrow](bcp-sendrow.md).  
  
 Inicialmente, el puntero a los datos de usuario se establece mediante una llamada a **bcp_bind**. Si cambia la dirección de datos de la variable de programa entre las llamadas a **bcp_sendrow**, puede llamar a **bcp_colptr** para restablecer el puntero a los datos. La siguiente llamada a **bcp_sendrow** envía los datos dirigidos por la llamada a **bcp_colptr**.  
  
 Debe haber un independiente **bcp_colptr** llamada para cada columna en la tabla cuya dirección de datos desea modificar.  
  
## <a name="see-also"></a>Vea también  
 [Funciones de copia masiva](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  