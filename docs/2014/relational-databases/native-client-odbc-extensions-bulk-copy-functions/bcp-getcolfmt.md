---
title: bcp_getcolfmt | Documentos de Microsoft
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
- bcp_getcolfmt
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_getcolfmt function
ms.assetid: f8bdada5-7b2d-4475-8c98-f93e9d77b130
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1dcae7d7934221e1df720869d09aa6abcf958c04
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107196"
---
# <a name="bcpgetcolfmt"></a>bcp_getcolfmt
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
 *HDBC*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
 *field*  
 Es el número de columnas para las que se recupera la propiedad.  
  
 *property*  
 Es una de las constantes de propiedad.  
  
 *pValue*  
 Es el puntero al búfer del que se recupera el valor de propiedad.  
  
 *cbValue*  
 Es la longitud del búfer de propiedad en bytes.  
  
 *pcbLen*  
 Puntero a la longitud de los datos que se devuelven en el búfer de propiedad.  
  
## <a name="returns"></a>Devuelve  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Notas  
 Valores de propiedad de formato de columna se muestran en la [bcp_setcolfmt](bcp-setcolfmt.md) tema. Los valores de propiedad del formato de columna se establecen llamando a la función **bcp_setcolfmt** , y se utiliza la función **bcp_getcolfmt** para buscar el valor de propiedad del formato de columna.  
  
 Cambios de comportamiento pueden observarse al conectarse a un [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (o posterior) equipo del servidor, en comparación con versiones anteriores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versiones. Para obtener más información, consulte [de detección de metadatos](../native-client/features/metadata-discovery.md).  
  
## <a name="bcpgetcolfmt-support-for-enhanced-date-and-time-features"></a>bcp_getcolfmt admite las características mejoradas de fecha y hora  
 Los tipos utilizados con el `BCP_FMT_TYPE` propiedad para los tipos de fecha y hora son como se especifica en [cambios en la copia masiva para tipos mejorada de fecha y hora &#40;OLE DB y ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 Para obtener más información, consulte [fecha y hora mejoras &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Vea también  
 [Funciones de copia masiva](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  