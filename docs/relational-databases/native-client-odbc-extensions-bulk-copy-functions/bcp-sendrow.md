---
title: bcp_sendrow | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: bcp_sendrow
apilocation: sqlncli11.dll
apitype: DLLExport
helpviewer_keywords: bcp_sendrow function
ms.assetid: ddbdb4bd-ad4e-4bf1-9a75-656aa26ce10a
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0caf3ad75ae1362252d23b1fc0489e5fcf5bdc32
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="bcpsendrow"></a>bcp_sendrow
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Envía una fila de datos de las variables de programa a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RETCODE bcp_sendrow (  
    HDBC hdbc);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HDBC*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
## <a name="returns"></a>Devuelve  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Comentarios  
 El **bcp_sendrow** función genera una fila desde variables de programa y lo envía a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Antes de llamar a **bcp_sendrow**, debe realizar llamadas al [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) para especificar las variables de programa que contiene los datos de fila.  
  
 Si se llama a **bcp_bind** especificando un tipo de datos largo, de longitud variable, por ejemplo un parámetro *eDataType* de SQLTEXT y un parámetro *pData* no NULL, **bcp_sendrow** envía el valor entiredata, igual que para cualquier otro tipo de datos. Si es, sin embargo, **bcp_bind** tiene un valor nulo *pData* parámetro, **bcp_sendrow** devuelve el control a la aplicación inmediatamente después de que todas las columnas con datos especificados se envían a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A continuación, puede llamar la aplicación [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) varias veces para enviar los datos largos, de longitud variable a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], un fragmento a la vez. Para obtener más información, consulte [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md).  
  
 Cuando **bcp_sendrow** se usa para filas de copia de las variables del programa en de forma masiva [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tablas, las filas se confirman sólo cuando el usuario llama [bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md) o [bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md) . El usuario puede llamar a **bcp_batch** una vez cada  *n*  filas o cuando se produzcan períodos de inactividad entre períodos de los datos entrantes. Si nunca se llama a **bcp_batch** , las filas se confirman cuando se llama a **bcp_done** .  
  
 Para obtener información sobre una separación de cambio de copia masiva a partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], consulte [realizar operaciones de copia masiva &#40; ODBC &#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md).  
  
## <a name="see-also"></a>Vea también  
 [Funciones de copia masiva](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
