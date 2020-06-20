---
title: bcp_getcolfmt | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_getcolfmt
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_getcolfmt function
ms.assetid: f8bdada5-7b2d-4475-8c98-f93e9d77b130
author: rothja
ms.author: jroth
ms.openlocfilehash: 294241eb586a70f4e0a826b1dce5d35879b3ee3e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85019515"
---
# <a name="bcp_getcolfmt"></a>bcp_getcolfmt
  Se utiliza para buscar el valor de propiedad del formato de columna.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RETCODE bcp_getcolfmt (  
HDBC   
hdbc  
,  
INT   
field  
,  
INT   
property  
,  
void*   
pValue  
,  
INT   
cbvalue,  
INT*   
pcbLen  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
 *campo*  
 Es el número de columnas para las que se recupera la propiedad.  
  
 *property*  
 Es una de las constantes de propiedad.  
  
 *pValue*  
 Es el puntero al búfer del que se recupera el valor de propiedad.  
  
 *cbValue*  
 Es la longitud del búfer de propiedad en bytes.  
  
 *pcbLen*  
 Puntero a la longitud de los datos que se devuelven en el búfer de propiedad.  
  
## <a name="returns"></a>Devoluciones  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Comentarios  
 Los valores de propiedad del formato de columna se muestran en el tema [bcp_setcolfmt](bcp-setcolfmt.md) . Los valores de propiedad del formato de columna se establecen llamando a la función **bcp_setcolfmt** , y se utiliza la función **bcp_getcolfmt** para buscar el valor de propiedad del formato de columna.  
  
 Los cambios de comportamiento pueden observarse al establecer conexión con un equipo servidor de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (o versiones posteriores) en comparación con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, vea [Detección de metadatos](../native-client/features/metadata-discovery.md).  
  
## <a name="bcp_getcolfmt-support-for-enhanced-date-and-time-features"></a>bcp_getcolfmt admite las características mejoradas de fecha y hora  
 Los tipos utilizados con la `BCP_FMT_TYPE` propiedad para los tipos de fecha y hora se especifican en [cambios de copia masiva para los tipos de fecha y hora mejorados &#40;OLE DB y&#41;ODBC ](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 Para obtener más información, vea [mejoras de fecha y hora &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Consulte también  
 [Bulk Copy Functions](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
