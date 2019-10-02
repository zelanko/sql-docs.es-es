---
title: bcp_getcolfmt | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_getcolfmt
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_getcolfmt function
ms.assetid: f8bdada5-7b2d-4475-8c98-f93e9d77b130
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 40e7f63438bbe6ff68284aa573e1307b17087234
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2019
ms.locfileid: "71707545"
---
# <a name="bcp_getcolfmt"></a>bcp_getcolfmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Se utiliza para buscar el valor de propiedad del formato de columna.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RETCODE bcp_getcolfmt (  
        HDBC hdbc,  
        INT field,  
        INT property,  
        void* pValue,  
        INT cbvalue,  
        INT* pcbLen);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
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
  
## <a name="remarks"></a>Comentarios  
 Los valores de propiedad del formato de columna se muestran en el tema [bcp_setcolfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setcolfmt.md) . Los valores de propiedad del formato de columna se establecen llamando a la función **bcp_setcolfmt** , y se utiliza la función **bcp_getcolfmt** para buscar el valor de propiedad del formato de columna.  
  
 Los cambios de comportamiento pueden observarse al establecer conexión con un equipo servidor de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (o versiones posteriores) en comparación con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, vea [Metadata Discovery](../../relational-databases/native-client/features/metadata-discovery.md).  
  
## <a name="bcp_getcolfmt-support-for-enhanced-date-and-time-features"></a>bcp_getcolfmt admite las características mejoradas de fecha y hora  
 Los tipos utilizados con la propiedad **BCP_FMT_TYPE** para los tipos de fecha y hora se especifican en [cambios de copia masiva para los tipos &#40;de fecha y&#41;hora mejorados OLE DB y ODBC](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 Para obtener más información, vea [mejoras &#40;de fecha y&#41;hora ODBC](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Vea también  
 [Funciones de copia masiva](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
