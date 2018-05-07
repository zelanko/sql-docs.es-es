---
title: Actualizar una aplicación de SQL Server 2005 Native Client | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, updating applications
ms.assetid: 1e1e570c-7f14-4e16-beab-c328e3fbdaa8
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 32ebeaefe034128943f081251cc9c40e34e88ee7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>Actualizar una aplicación desde SQL Server 2005 Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  En este tema se describen los cambios importantes en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con respecto a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Al realizar una actualización de Microsoft Data Access Components (MDAC) a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, también es posible que observe algunas diferencias de comportamiento. Para obtener más información, consulte [actualizar una aplicación a SQL Server Native Client de MDAC](../../../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 incluidos con [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 incluidos con [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.5 se incluyó en [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 se incluyó en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] y [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)].  
  
|Cambios de comportamiento en SQL Server Native Client desde [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]|Description|  
|------------------------------------------------------------------------------------|-----------------|  
|OLE DB solamente rellena los datos hasta la escala definida.|Para que los datos convertidos se envían al servidor, las conversiones [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (a partir de [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) rellena ceros finales en los datos sólo hasta la longitud máxima de **datetime** valores. En SQL Server Native Client 9.0 los datos se rellenaban hasta 9 dígitos.|  
|Validación de DBTYPE_DBTIMESTAMP para ICommandWithParameter::SetParameterInfo.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (a partir de [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) implementa el requisito de OLE DB para *bScale* en ICommandWithParameter::SetParameterInfo que se establecerá con precisión de fracciones de segundo para DBTYPE_DBTIMESTAMP.|  
|El **sp_columns** procedimiento almacenado ahora devuelve **"N"** en lugar de **"N"** para la columna IS_NULLABLE.|A partir de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]), **sp_columns** procedimiento almacenado ahora devuelve **"N"** en lugar de **"N"** para una columna IS_NULLABLE .|  
|SQLSetDescRec y SQLBindParameter, SQLBindCol ahora realizan una comprobación de coherencia.|Anteriores a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, establecimiento de SQL_DESC_DATA_PTR no producía la comprobación de coherencia para cualquier tipo de descriptor en SQLSetDescRec, SQLBindParameter o SQLBindCol.|  
|SQLCopyDesc ahora se realiza la comprobación de coherencia de descriptor.|Anteriores a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, SQLCopyDesc no hizo una comprobación de coherencia cuando el campo SQL_DESC_DATA_PTR se estableció en un registro concreto.|  
|SQLGetDescRec ya no es una descriptor comprobación de coherencia.|Anteriores a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, SQLGetDescRec realiza una comprobación de coherencia del descriptor cuando se establece el campo SQL_DESC_DATA_PTR. Esto último no era un requisito de la especificación de ODBC y, en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) y versiones posteriores, ya no se realiza esta comprobación de coherencia.|  
|Se devuelve un error distinto cuando la fecha se encuentra fuera del intervalo.|Para el **datetime** tipo, se devolverá un número de error diferentes mediante [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (a partir de [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) para un fuera del intervalo de fechas que se devolvió en versiones anteriores.<br /><br /> En concreto, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 devolvía 22007 para todos los valores de año de intervalo en conversiones de cadena a fuera **datetime**, y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client a partir de la versión 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) devuelve 22008 cuando la fecha está dentro del intervalo admitido por **datetime2** , pero fuera del intervalo admitido por **datetime** o **smalldatetime**.|  
|**fecha y hora** valor trunca las fracciones de segundo y no de ida y vuelta if redondeo cambia el día.|Anteriores a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, el comportamiento de cliente **datetime** valores que se envían al servidor era redondearlos a más cercano 1/300 de segundo. A partir de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, este mismo escenario provoca un truncamiento de fracciones de segundo si al redondear cambia el día.|  
|Posible truncamiento de segundos para **datetime** valor.|Una aplicación compilada con [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client (o posterior) que se conecta a un servidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2005 truncará segundos y fracciones de segundo para la parte de hora de los datos enviados al servidor si se enlaza con una columna de fecha y hora con un identificador de tipo DBTYPE_DBTIMESTAMP (OLE DB) o SQL_TIMESTAMP (ODBC) y una escala de 0.<br /><br /> Por ejemplo:<br /><br /> Datos de entrada: 1994-08-21 21:21:36.000<br /><br /> Datos insertados: 1994-08-21 21:21:00.000|  
|La conversión de datos OLE DB de DBTYPE_DBTIME a DBTYPE_DATE ya no puede hacer que cambie el día.|En versiones anteriores a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, si la parte correspondiente a la hora de DBTYPE_DATE se encontraba a medio segundo de la medianoche, el código de conversión de OLE DB hacía que el día cambiara. A partir de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, el día no cambiará (las fracciones de segundo se truncan y no se redondean).|  
|Cambios de conversión de IBCPSession::BCColFmt.|A partir de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, cuando usa IBCPSession::BCOColFmt para convertir SQLDATETIME o SQLDATETIME en un tipo de cadena, un valor fraccionario se exporta. Por ejemplo, al convertir un tipo SQLDATETIME en un tipo SQLNVARCHARMAX, las versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client devolvían<br /><br /> 1989-02-01 00:00:00. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 y versiones posteriores devuelven 1989-02-01 00:00:00.0000000.|  
|El tamaño de los datos enviados debe coincidir con la longitud especificada en SQL_LEN_DATA_AT_EXEC.|Cuando se utiliza SQL_LEN_DATA_AT_EXEC, el tamaño de los datos debe coincidir con la longitud especificada en SQL_LEN_DATA_AT_EXEC. Puede usar SQL_DATA_AT_EXEC, pero resulta mucho más ventajoso desde el punto de vista del rendimiento utilizar SQL_LEN_DATA_AT_EXEC.|  
|Ahora, las aplicaciones personalizadas que utilizan la API de BCP pueden recibir una advertencia.|La API de BCP generará un mensaje de advertencia si la longitud de los datos es mayor que la longitud especificada en un campo para todos los tipos. Anteriormente, esta advertencia solo se recibía para los tipos de caracteres, pero no se emitía para todos los tipos.|  
|Insertar una cadena vacía en un **sql_variant** enlazado como un tipo de fecha y hora genera un error.|En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0, insertar una cadena vacía en un **sql_variant** enlazado como un tipo de fecha y hora no generaba un error. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 (y posterior) genera un error en esta situación.|  
|Validación de parámetros SQL_C_TYPE_TIMESTAMP y DBTYPE_DBTIMESTAMP más estricta.|Anteriores a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client, **datetime** los valores se redondean para ajustarse a la escala de **datetime** y **smalldatetime** columnas por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client (y posteriores) aplica reglas de validación más estrictas, que se definen en la especificación básica de ODBC para las fracciones de segundo. Si un valor de parámetro no puede convertirse en el tipo SQL utilizando la escala especificada o no puede implicarse mediante el enlace del cliente sin que se produzca un truncamiento de los dígitos finales, se devuelve un error.|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] puede devolver resultados diferentes cuando se ejecuta un desencadenador.|Cambios realizados en [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] pueden hacer que una aplicación para que devuelva resultados diferentes de una instrucción que ha causado un desencadenador que se ejecuta cuando **NOCOUNT OFF** estaba activo. En esta situación, es posible que la aplicación genere un error. Para resolver este error, establezca **NOCOUNT ON** en la llamada SQLMoreResults para avanzar al siguiente de resultados o el desencadenador.|  
  
## <a name="see-also"></a>Vea también  
 [Programación de SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
