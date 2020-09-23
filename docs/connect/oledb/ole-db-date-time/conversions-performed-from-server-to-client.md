---
title: Conversiones realizadas de servidor a cliente | Microsoft Docs
description: Obtenga información sobre las conversiones de fecha y hora realizadas entre SQL Server y una aplicación cliente escrita con OLE DB Driver for SQL Server.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- conversions [OLE DB], server to client
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 83d09f15b916f164aa63105bd494d12a18ca8abf
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862360"
---
# <a name="conversions-performed-from-server-to-client"></a>Conversiones realizadas de servidor a cliente
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  En este artículo se describen las conversiones de fecha y hora realizadas entre [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] (o posterior) y una aplicación cliente escrita con el controlador OLE DB para SQL Server.  
  
## <a name="conversions"></a>Conversiones  
 En la tabla siguiente se describen las conversiones entre el tipo devuelto al cliente y el tipo del enlace. Para los parámetros de salida, si se ha llamado a ICommandWithParameters::SetParameterInfo y el tipo especificado en *pwszDataSourceType* no coincide con el tipo real del servidor, el servidor realizará una conversión implícita y el tipo devuelto al cliente coincidirá con el tipo especificado mediante ICommandWithParameters::SetParameterInfo. Esto puede conducir a resultados de conversión inesperados cuando las reglas de conversión del servidor son distintas de las descritas en este artículo. Por ejemplo, cuando se debe proporcionar una fecha predeterminada, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utiliza 1900-1-1 en lugar de 1899-12-30.  
  
|A -><br /><br /> De|DATE|DBDATE|DBTIME|DBTIME2|DBTIMESTAMP|DBTIMESTAMPOFFSET|FILETIME|BYTES|VARIANT|SSVARIANT|BSTR|STR|WSTR|  
|----------------------|----------|------------|------------|-------------|-----------------|-----------------------|--------------|-----------|-------------|---------------|----------|---------|----------|  
|Date|1, 7|Aceptar|-|-|1|1, 3|1, 7|-|Aceptar (VT_BSTR)|Aceptar|Aceptar|4|4|  
|Time|5, 6, 7|-|9|Aceptar|6|3, 6|5, 6|-|Aceptar (VT_BSTR)|Aceptar|Aceptar|4|4|  
|Smalldatetime|7|8|9, 10|10|Aceptar|3|7|-|7 (VT_DATE)|Aceptar|Aceptar|4|4|  
|Datetime|5, 7|8|9, 10|10|Aceptar|3|7|-|7 (VT_DATE)|Aceptar|Aceptar|4|4|  
|Datetime2|5, 7|8|9, 10|10|7|3|5, 7|-|Aceptar (VT_BSTR)|Aceptar|Aceptar|4|4|  
|Datetimeoffset|5, 7, 11|8, 11|9, 10, 11|10, 11|7, 11|Aceptar|5, 7, 11|-|Aceptar (VT_BSTR)|Aceptar|Aceptar|4|4|  
|Char, Varchar,<br /><br /> Nchar, Nvarchar|7, 13|12|12, 9|12|12|12|7, 13|N/D|N/D|N/D|N/D|N/D|N/D|  
|Sql_variant<br /><br /> (datetime)|7|8|9, 10|10|Aceptar|3|7|-|7 (VT_DATE)|Aceptar|Aceptar|4|4|  
|Sql_variant<br /><br /> (smalldatetime)|7|8|9, 10|10|Aceptar|3|7|-|7 (VT_DATE)|Aceptar|Aceptar|4|4|  
|Sql_variant<br /><br /> (date)|1, 7|Aceptar|2|2|1|1, 3|1, 7|-|OK (VT_BSTR)|Aceptar|Aceptar|4|4|  
|Sql_variant<br /><br /> (time)|5, 6, 7|2|6|Aceptar|6|3, 6|5, 6|-|OK (VT_BSTR)|Aceptar|Aceptar|4|4|  
|Sql_variant<br /><br /> (datetime2)|5, 7|8|9, 10|10|Aceptar|3|5, 7|-|OK (VT_BSTR)|Aceptar|Aceptar|4|4|  
|Sql_variant<br /><br /> (datetimeoffset)|5, 7, 11|8, 11|9, 10, 11|10, 11|7, 11|Aceptar|5, 7, 11|-|OK (VT_BSTR)|Aceptar|Aceptar|4|4|  
  
## <a name="key-to-symbols"></a>Clave de los símbolos  
  
|Símbolo|Significado|  
|------------|-------------|  
|Aceptar|No es necesaria la conversión.|  
|-|No se admite la conversión. Si el enlace se valida cuando se llama a IAccessor::CreateAccessor, DBBINDSTATUS_UPSUPPORTEDCONVERSION se devuelve en *rgStatus*. Cuando se aplaza la comprobación de descriptor de acceso, se establece DBSTATUS_E_BADACCESSOR.|  
|1|Los campos de hora se establecen en cero.|  
|2|Se establece DBSTATUS_E_CANTCONVERTVALUE.|  
|3|La zona horaria se establece en cero.|  
|4|Si el búfer del cliente no es bastante grande, se establece DBSTATUS_S_TRUNCATED. Cuando el tipo de servidor incluye fracciones de segundo, el número de dígitos de la cadena de resultado coincide exactamente con la escala del tipo de servidor.|  
|5|Se omite el truncamiento de los segundos o de las fracciones de segundo.|  
|6|La fecha está establecida en la fecha actual, a menos que el origen sea un literal de hora de cadena y el destino sea DBTYPE_DATE. En este caso, se utiliza 1899-12-30.|  
|7|Si se produce un desbordamiento del valor, se establece DBSTATUS_E_DATAOVERFLOW.|  
|8|Se omiten los campos de hora.|  
|9|Se omiten los campos de fracciones de segundo.|  
|10|Se omite el componente de fecha.|  
|11|Se convierte la hora en la zona horaria del cliente. Si se produce un error durante esta conversión se establece DBSTATUS_E_DATAOVERFLOW.|  
|12|La cadena se analiza como un literal ISO y se convierte al tipo de destino. Si se produce un error, la cadena se analiza como un literal de fecha OLE (que también tiene componentes de hora) y se convierte de una fecha OLE (DBTYPE_DATE) al tipo de destino. La cadena debe cumplir la sintaxis de literales del tipo de destino permitido para que el análisis de formato ISO sea correcto. Para que el análisis de OLE sea correcto, la cadena debe cumplir la sintaxis reconocida por OLE. Si no se puede analizar la cadena, se establece DBSTATUS_E_CANTCONVERTVALUE. Si algún valor de componente está fuera del intervalo, se establece DBSTATUS_E_DATAOVERFLOW.|  
|13|La cadena se analiza como un literal ISO y se convierte al tipo de destino. Si se produce un error, la cadena se analiza como un literal de fecha OLE (que también tiene componentes de hora) y se convierte de una fecha OLE (DBTYPE_DATE) al tipo de destino. La cadena debe cumplir la sintaxis de los literales de fecha y hora, a menos que el destino sea DBTYPE_DATE o DBTYPE_DBTIMESTAMP. Si éste es el caso, se permite un literal de fecha y hora o fecha para que el análisis de formato ISO sea correcto. Para que el análisis de OLE sea correcto, la cadena debe cumplir la sintaxis reconocida por OLE. Si no se puede analizar la cadena, se establece DBSTATUS_E_CANTCONVERTVALUE. Si algún valor de componente está fuera del intervalo, se establece DBSTATUS_E_DATAOVERFLOW.|  
  
## <a name="see-also"></a>Consulte también  
 [Enlaces y conversiones &#40;OLE DB&#41;](../../oledb/ole-db-date-time/conversions-ole-db.md)  
  
  
