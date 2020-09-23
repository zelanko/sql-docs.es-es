---
title: Conversiones realizadas de cliente a servidor | Microsoft Docs
description: Obtenga información sobre las conversiones de fecha y hora realizadas entre una aplicación cliente escrita con OLE DB Driver for SQL Server y SQL Server.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- conversions [OLE DB], client to server
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c5a43604c485c2baf7bb5b4430303db7fedd9bd8
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88860221"
---
# <a name="conversions-performed-from-client-to-server"></a>Conversiones realizadas de cliente a servidor
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  En este artículo se describen las conversiones de fecha y hora realizadas entre una aplicación cliente escrita con el controlador OLE DB para SQL Server y [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] (o posterior).  
  
## <a name="conversions"></a>Conversiones  
 En este artículo, se describen las conversiones realizadas en el cliente. Si el cliente especifica una precisión de fracciones de segundos para un parámetro que difiere de la definida en el servidor, la conversión del cliente puede producir un error cuando el servidor permita llevar a cabo la operación. En concreto, el cliente trata cualquier truncamiento de fracciones de segundo como un error, mientras que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] redondea los valores de hora al segundo entero más próximo.  
  
 Si no se llama a ICommandWithParameters::SetParameterInfo, los enlaces de DBTYPE_DBTIMESTAMP se convierten como si fueran **datetime2**.  
  
|A -><br /><br /> De|DBDATE (date)|DBTIME (time)|DBTIME2 (time)|DBTIMESTAMP (smalldatetime)|DBTIMESTAMP (datetime)|DBTIMESTAMP (datetime2)|DBTIMESTAMPOFFSET (datetimeoffset)|STR|WSTR|SQLVARIANT<br /><br /> (sql_variant)|  
|----------------------|---------------------|---------------------|----------------------|-----------------------------------|------------------------------|-------------------------------|------------------------------------------|---------|----------|-------------------------------------|  
|DATE|1, 2|1, 3, 4|4, 12|1, 12|1, 12|1, 12|1, 5, 12|1, 12|1, 12|1, 12<br /><br /> datetime2(0)|  
|DBDATE|1|-|-|1, 6|1, 6|1, 6|1, 5, 6|1, 10|1, 10|1<br /><br /> date|  
|DBTIME|-|1|1|1, 7|1, 7|1, 7|1, 5, 7|1, 10|1, 10|1<br /><br /> Time(0)|  
|DBTIME2|-|1, 3|1|1, 7, 10, 14|1, 7, 10, 15|1, 7, 10|1, 5, 7, 10|1, 10, 11|1, 10, 11|1<br /><br /> Time(7)|  
|DBTIMESTAMP|1, 2|1, 3, 4|1, 4, 10|1, 10, 14|1, 10, 15|1, 10|1, 5, 10|1, 10,11|1, 10, 11|1, 10<br /><br /> datetime2(7)|  
|DBTIMESTAMPOFFSET|1, 2, 8|1, 3, 4, 8|1, 4, 8, 10|1, 8, 10, 14|1, 8, 10, 15|1, 8, 10|1, 10|1, 10, 11|1, 10, 11|1, 10<br /><br /> datetimeoffset(7)|  
|FILETIME|1, 2|1, 3, 4|1, 4, 13|1, 13|1, 13|1, 13|1, 5, 13|1, 13|1, 10|1, 13<br /><br /> datetime2(3)|  
|BYTES|-|-|-|-|-|-|-|N/D|N/D|N/D|  
|VARIANT|1|1|1|1, 10|1, 10|1, 10|1, 10|N/D|N/D|1, 10|  
|SSVARIANT|1, 16|1, 16|1, 16|1, 10, 16|1, 10, 16|1, 10, 16|1, 10, 16|N/D|N/D|1, 16|  
|BSTR|1, 9|1, 9|1, 9, 10|1, 9, 10|1, 9, 10|1, 9, 10|1, 9, 10|N/D|N/D|N/D|  
|STR|1, 9|1, 9|1, 9, 10|1, 9, 10|1, 9, 10|1, 9, 10|1, 9, 10|N/D|N/D|N/D|  
|WSTR|1, 9|1, 9|1, 9, 10|1, 9, 10|1, 9, 10|1, 9, 10|1, 9, 10|N/D|N/D|N/D|  
  
## <a name="key-to-symbols"></a>Clave de los símbolos  
  
|Símbolo|Significado|  
|------------|-------------|  
|-|No se admite la conversión. Si el enlace se valida cuando se llama a IAccessor::CreateAccessor, DBBINDSTATUS_UPSUPPORTEDCONVERSION se devuelve en *rgStatus*. Cuando se aplaza la comprobación de descriptor de acceso, se establece DBSTATUS_E_BADACCESSOR.|  
|N/D|No aplicable.|  
|1|Si los datos proporcionados no son válidos, se establece DBSTATUS_E_CANTCONVERTVALUE. Los datos de entrada se validan antes de que se apliquen las conversiones, de modo que aunque un componente vaya a ser omitido por una conversión subsiguiente, deberá seguir siendo válido para que la conversión se produzca con éxito.|  
|2|Se omiten los campos de hora.|  
|3|Las fracciones de segundo deben ser cero o se establece DBSTATUS_E_DATAOVERFLOW.|  
|4|Se omite el componente de fecha.|  
|5|La zona horaria se establece en el valor de zona horaria del cliente.|  
|6|La hora se establece en cero.|  
|7|La fecha se establece en la fecha actual.|  
|8|La hora se convierte a UTC. Si se produce un error durante esta conversión, se establece DBSTATUS_E_CANTCONVERTVALUE.|  
|9|La cadena se analiza como un literal ISO y se convierte al tipo de destino. Si se produce un error, la cadena se analiza como un literal de fecha OLE (que también tiene componentes de hora) y se convierte de una fecha OLE (DBTYPE_DATE) al tipo de destino.<br /><br /> Si el tipo de destino es DBTIMESTAMP, **smalldatetime**, **datetime**o **datetime2**, la cadena debe seguir la sintaxis para fecha, hora o literales **datetime2** , o la sintaxis reconocida por OLE. Si la cadena es un literal de fecha, todos los componentes de hora se establecen en cero. Si la cadena es un literal de hora, la fecha se establece en la fecha actual.<br /><br /> Para todos los demás tipos de destino, la cadena debe seguir la sintaxis de los literales del tipo de destino.|  
|10|Si se produce un truncamiento con pérdida de datos, se establece DBSTATUS_E_DATAOVERFLOW. Para las conversiones de cadenas, la comprobación de desbordamiento solamente es posible si la cadena cumple la sintaxis ISO. Si la cadena es un literal de fecha OLE, las fracciones de segundo se redondean.<br /><br /> Para conversiones de DBTIMESTAMP (datetime) a smalldatetime, el controlador OLE DB para SQL Server truncará silenciosamente el valor de los segundos en lugar de producir el error DBSTATUS_E_DATAOVERFLOW.|  
|11|El número de dígitos de fracciones de segundo (la escala) se determina según el tamaño de la columna de destino, de acuerdo con la tabla siguiente. Si el tamaño de las columnas es mayor que el intervalo de la tabla, se presupone una escala de 9. Esta conversión debería permitir hasta nueve dígitos en las fracciones de segundo, que es el máximo permitido por OLE DB.<br /><br /> Sin embargo, si el tipo de origen es DBTIMESTAMP y las fracciones de segundo son cero, no se generan dígitos de fracciones de segundo ni separador decimal. Este comportamiento asegura la compatibilidad con versiones anteriores para aplicaciones desarrolladas utilizando proveedores OLE DB anteriores.<br /><br /> Un tamaño de columna de ~0 implica un tamaño ilimitado en OLE DB (9 dígitos, a menos que sea aplicable la regla de 3 dígitos para DBTIMESTAMP).|  
|12|Se mantiene la semántica de conversión anterior a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] para DBTYPE_DATE. Las fracciones de segundo se truncan en cero.|  
|13|Se mantiene la semántica de conversión anterior a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] para DBTYPE_FILETIME. Si usa la API FileTimeToSystemTime de Windows, la precisión de fracciones de segundo se limita a 1 milisegundo.|  
|14|Se mantiene la semántica de conversión anterior a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] para **smalldatetime**. Los segundos se establecen en cero.|  
|15|Se mantiene la semántica de conversión anterior a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] para **datetime**. Los segundos se redondean a la fracción 1/300 de segundo más próxima.|  
|16|El comportamiento de conversión de un valor (de un tipo determinado) incrustado en una estructura de cliente de SSVARIANT y el comportamiento del mismo valor y tipo cuando no está incrustado en una estructura de cliente de SSVARIANT son iguales.|  
  
| Tipo | Longitud (en caracteres) | Escala |  
| ---- | ----------------- | ----- |  
|DBTIME2|8, 10..18|0,1..9|  
|DBTIMESTAMP|19, 21..29|0,1..9|  
|DBTIMESTAMPOFFSET|26, 28..36|0,1..9|  
  
## <a name="see-also"></a>Consulte también  
 [Enlaces y conversiones &#40;OLE DB&#41;](../../oledb/ole-db-date-time/conversions-ole-db.md)  
  
  
