---
title: bcp_sendrow | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_sendrow
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_sendrow function
ms.assetid: ddbdb4bd-ad4e-4bf1-9a75-656aa26ce10a
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9278a388fa6beb52dc747d310bea4a2ce32c600e
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705312"
---
# <a name="bcp_sendrow"></a>bcp_sendrow
  Envía una fila de datos de las variables de programa a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RETCODE bcp_sendrow (  
    HDBC   
hdbc  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
## <a name="returns"></a>Devoluciones  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Observaciones  
 La función **bcp_sendrow** genera una fila a partir de las variables de programa y la envía a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Antes de llamar a **a bcp_sendrow**, debe hacer llamadas a [bcp_bind](bcp-bind.md) para especificar las variables de programa que contienen los datos de la fila.  
  
 Si se llama a **bcp_bind** especificando un tipo de datos largo, de longitud variable, por ejemplo un parámetro *eDataType* de SQLTEXT y un parámetro *pData* no NULL, **bcp_sendrow** envía el valor entiredata, igual que para cualquier otro tipo de datos. Si, no obstante, **bcp_bind** tiene un parámetro *pData* NULL, **bcp_sendrow** devuelve inmediatamente el control a la aplicación inmediatamente después de enviar todas las columnas con datos especificados a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A continuación, la aplicación puede llamar repetidamente a [bcp_moretext](bcp-moretext.md) para enviar los datos largos, de longitud variable a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], un fragmento a la vez. Para obtener más información, vea [bcp_moretext](bcp-moretext.md).  
  
 Cuando se utiliza **bcp_sendrow** para la copia masiva de filas de variables de programa en tablas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , las filas solamente se confirman cuando el usuario llama a [a bcp_batch](bcp-batch.md) o a [bcp_done](bcp-done.md). El usuario puede elegir llamar a **bcp_batch** una vez cada *n* filas o cuando haya un periodo de inactividad entre períodos de entrada de datos. Si nunca se llama a **bcp_batch** , las filas se confirman cuando se llama a **bcp_done** .  
  
 Para obtener información sobre un cambio importante en la copia masiva a partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , vea [realizar operaciones de copia masiva &#40;ODBC&#41;](../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md).  
  
## <a name="see-also"></a>Consulte también  
 [Bulk Copy Functions](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
