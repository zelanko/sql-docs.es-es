---
title: bcp_sendrow | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
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
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2810dd25a14f35ed275a7d1117fc21d7946cc90e
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37423544"
---
# <a name="bcpsendrow"></a>bcp_sendrow
  Envía una fila de datos de las variables de programa a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RETCODE bcp_sendrow (  
    HDBC   
hdbc  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *HDBC*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
## <a name="returns"></a>Devuelve  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Notas  
 El **bcp_sendrow** función genera una fila a las variables de programa y lo envía a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Antes de llamar a **bcp_sendrow**, debe hacer llamadas a [bcp_bind](bcp-bind.md) para especificar las variables de programa que contiene los datos de fila.  
  
 Si se llama a **bcp_bind** especificando un tipo de datos largo, de longitud variable, por ejemplo un parámetro *eDataType* de SQLTEXT y un parámetro *pData* no NULL, **bcp_sendrow** envía el valor entiredata, igual que para cualquier otro tipo de datos. Si es, sin embargo, **bcp_bind** tiene un valor nulo *pData* parámetro, **bcp_sendrow** devuelve el control a la aplicación inmediatamente después de envían todas las columnas con datos especificados a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A continuación, puede llamar la aplicación [bcp_moretext](bcp-moretext.md) varias veces para enviar los datos de largo, de longitud variable [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], un fragmento a la vez. Para obtener más información, consulte [bcp_moretext](bcp-moretext.md).  
  
 Cuando **bcp_sendrow** se usa para la copia masiva de filas de las variables de programa en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tablas, las filas se confirman sólo cuando el usuario llama a [bcp_batch](bcp-batch.md) o [bcp_done](bcp-done.md) . El usuario puede elegir llamar a **bcp_batch** una vez cada *n* filas o cuando haya un periodo de inactividad entre períodos de entrada de datos. Si nunca se llama a **bcp_batch** , las filas se confirman cuando se llama a **bcp_done** .  
  
 Para obtener información sobre una separación de cambio de copia masiva a partir [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], consulte [realizar operaciones de copia masiva &#40;ODBC&#41;](../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md).  
  
## <a name="see-also"></a>Vea también  
 [Funciones de copia masiva](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
