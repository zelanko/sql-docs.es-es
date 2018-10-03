---
title: bcp_colptr | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 269ab3c748557d1d2870195524310f2371b79c52
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48131005"
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
 Es un puntero a los datos que van a copiarse. Si el tipo de datos enlazado es el tipo de valor grande (como SQLTEXT o SQLIMAGE), *pData* puede ser NULL. Un valor NULL *pData* indica los valores de datos largos se enviarán a SQL Server en fragmentos utilizando [bcp_moretext](bcp-moretext.md).  
  
 Si *pData* se establece en NULL y la columna correspondiente al campo enlazado no es un tipo de valor grande, **bcp_colptr** se produce un error.  
  
 Para obtener más información sobre los tipos de valor grandes, consulte [bcp_bind](bcp-bind.md)**.**  
  
 *idxServerCol*  
 Es la posición ordinal de la columna en la tabla de base de datos en la que se copian los datos. La primera columna de una tabla es la columna 1. La posición ordinal de una columna se notifica mediante [SQLColumns](../native-client-odbc-api/sqlcolumns.md).  
  
## <a name="returns"></a>Devuelve  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Comentarios  
 El **bcp_colptr** función le permite cambiar la dirección de origen de datos para una determinada columna al copiar datos a SQL Server con [bcp_sendrow](bcp-sendrow.md).  
  
 Inicialmente, el puntero a los datos de usuario se establece mediante una llamada a **bcp_bind**. Si cambia la dirección de datos de la variable de programa entre las llamadas a **bcp_sendrow**, puede llamar a **bcp_colptr** para restablecer el puntero a los datos. La siguiente llamada a **bcp_sendrow** envía los datos dirigidos por la llamada a **bcp_colptr**.  
  
 Debe haber otro **bcp_colptr** llamada para cada columna en la tabla cuya dirección de datos desea modificar.  
  
## <a name="see-also"></a>Vea también  
 [Funciones de copia masiva](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
