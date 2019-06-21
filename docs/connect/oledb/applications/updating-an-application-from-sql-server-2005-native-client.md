---
title: Actualizar una aplicación desde SQL Server 2005 Native Client | Microsoft Docs
description: Actualizar una aplicación desde SQL Server 2005 Native Client
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, updating applications
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 17280079f493d8abbad2f8ffb76d25c2a0ba868f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66771072"
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>Actualizar una aplicación desde SQL Server 2005 Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Este tema describen los cambios importantes en el controlador de OLE DB para SQL Server desde [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  

 Al realizar una actualización de los Componentes de Microsoft Data Access (MDAC) al controlador OLE DB para SQL Server, también es posible que observe algunas diferencias de comportamiento. Para obtener más información, consulte [actualizar una aplicación a controlador de OLE DB para SQL Server de MDAC](../../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).  

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 se incluyó en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 se incluyó en [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.5 se incluyó en [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 se incluyó en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] y [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)].  

|Puede cambiar el comportamiento en el controlador de OLE DB para SQL Server en comparación con [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client|Descripción|  
|------------------------------------------------------------------------------------|-----------------|  
|OLE DB solamente rellena los datos hasta la escala definida.|Para las conversiones donde los datos convertidos se envían al servidor, el controlador OLE DB para SQL Server rellena los ceros finales en datos solo hasta la longitud máxima de **datetime** valores. En SQL Server Native Client 9.0 los datos se rellenaban hasta 9 dígitos.|  
|Validación de DBTYPE_DBTIMESTAMP para ICommandWithParameter::SetParameterInfo.|Controlador OLE DB para SQL Server implementa el requisito de OLE DB para *bScale* en ICommandWithParameter::SetParameterInfo debe establecerse en una precisión de fracciones para DBTYPE_DBTIMESTAMP.|  
|El **sp_columns** procedimiento almacenado ahora devuelve **"NO"** en lugar de **"NO"** para la columna IS_NULLABLE.|En el controlador OLE DB para SQL Server, **sp_columns** procedimiento almacenado ahora devuelve **"NO"** en lugar de **"NO"** para una columna IS_NULLABLE.|  
|Se devuelve un error distinto cuando la fecha se encuentra fuera del intervalo.|Para el **datetime** tipo, un número de error diferentes se devolverá por controlador de OLE DB para SQL Server para una fecha fuera del intervalo que se devolvió en versiones anteriores.<br /><br /> En concreto, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 devolvía 22007 para todos los valores fuera del intervalo año en las conversiones de cadena a **datetime**, y el controlador OLE DB para SQL Server devuelve 22008 cuando la fecha está dentro del intervalo admitido por **datetime2** pero fuera del intervalo admitido por **datetime** o **smalldatetime**.|  
|El valor **datetime** trunca las fracciones de segundo y no se redondea si el redondeo cambia el día.|En versiones anteriores a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, el comportamiento del cliente para los valores **datetime** que se enviaban al servidor era redondearlos a la fracción 1/300 de segundo más próxima. En el controlador OLE DB para SQL Server, este mismo escenario provoca un truncamiento de fracciones de segundo si al redondear cambia el día.|  
|Posible truncamiento de segundos para **datetime** valor.|Una aplicación compilada con el controlador OLE DB para SQL Server que se conecta a un servidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2005 truncará segundos y fracciones de segundo para la parte de hora de los datos enviados al servidor si se enlaza con una columna datetime con un identificador de tipo de DBTYPE_DBTIMESTAMP (OLE DB) o SQL_TIMESTAMP (ODBC) y una escala de 0.<br /><br /> Por ejemplo:<br /><br /> Datos de entrada: 1994-08-21 21:21:36.000<br /><br /> Datos insertados: 1994-08-21 21:21:00.000|  
|La conversión de datos OLE DB de DBTYPE_DBTIME a DBTYPE_DATE ya no puede hacer que cambie el día.|En versiones anteriores a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, si la parte correspondiente a la hora de DBTYPE_DATE se encontraba a medio segundo de la medianoche, el código de conversión de OLE DB hacía que el día cambiara. En el controlador OLE DB para SQL Server, el día no cambiará (fracciones de segundo se truncan y no se redondean).|  
|Cambios en la conversión IBCPSession::BCColFmt.|En el controlador OLE DB para SQL Server, cuando se usa IBCPSession::BCOColFmt para convertir SQLDATETIME o SQLDATETIME en un tipo de cadena, un valor fraccionario se exporta. Por ejemplo, al convertir un tipo SQLDATETIME en un tipo SQLNVARCHARMAX, las versiones anteriores a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 devolvían<br /> 1989-02-01 00:00:00.<br />El controlador OLE DB para SQL Server devuelve <br />1989-02-01 00:00:00.0000000.|  
|Ahora, las aplicaciones personalizadas que utilizan la API de BCP pueden recibir una advertencia.|La API de BCP generará un mensaje de advertencia si la longitud de los datos es mayor que la longitud especificada en un campo para todos los tipos. Anteriormente, esta advertencia solo se recibía para los tipos de caracteres, pero no se emitía para todos los tipos.|  
|Si se inserta una cadena vacía en un **sql_variant** enlazado como un tipo de fecha y hora, se genera un error.|En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0, al insertar una cadena vacía en un elemento **sql_variant** enlazado como un tipo de fecha y hora no se generaba ningún error. Controlador OLE DB para SQL Server genera un error en esta situación.|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] puede devolver resultados diferentes cuando se ejecuta un desencadenador.|Los cambios introducidos en [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] pueden hacer que una aplicación devuelva otros resultados de una instrucción que ha producido la ejecución de un desencadenador cuando **NOCOUNT OFF** estaba activo. En esta situación, es posible que la aplicación genere un error. Para resolver este error, establezca **NOCOUNT ON** en el desencadenador.|  

## <a name="see-also"></a>Consulte también   
 [Controlador OLE DB para SQL Server](../../oledb/oledb-driver-for-sql-server.md)
