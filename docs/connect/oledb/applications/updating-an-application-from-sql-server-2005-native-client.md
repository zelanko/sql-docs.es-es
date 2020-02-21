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
ms.openlocfilehash: 7915b9fb74f05057e05eef022d7f9b0e4ccdd21f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67989247"
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>Actualizar una aplicación desde SQL Server 2005 Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  En este tema se describen los cambios importantes en OLE DB Driver for SQL Server desde [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  

 Al realizar una actualización de los Componentes de Microsoft Data Access (MDAC) al controlador OLE DB para SQL Server, también es posible que observe algunas diferencias de comportamiento. Para más información, consulte [Actualización de una aplicación a OLE DB Driver for SQL Server desde MDAC](../../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).  

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 se incluyó en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 se incluyó en [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.5 se incluyó en [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 se incluyó en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] y [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)].  

|Comportamiento cambiado en OLE DB Driver for SQL Server en comparación con [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client|Descripción|  
|------------------------------------------------------------------------------------|-----------------|  
|OLE DB solamente rellena los datos hasta la escala definida.|Para las conversiones en las que los datos convertidos se envían al servidor, OLE DB Driver for SQL Server solamente rellena los datos con ceros a la derecha hasta la longitud máxima de los valores **datetime**. En SQL Server Native Client 9.0 los datos se rellenaban hasta 9 dígitos.|  
|Valide DBTYPE_DBTIMESTAMP para ICommandWithParameter::SetParameterInfo.|OLE DB Driver for SQL Server implementa el requisito de OLE DB para *bScale* en ICommandWithParameter::SetParameterInfo para establecerse en la precisión de fracciones de segundo para DBTYPE_DBTIMESTAMP.|  
|El procedimiento almacenado **sp_columns** ahora devuelve **"NO"** en lugar de **"NO "** para la columna IS_NULLABLE.|En OLE DB Driver for SQL Server, el procedimiento almacenado **sp_columns** ahora devuelve **"NO"** en lugar de **"NO "** para la columna IS_NULLABLE.|  
|Se devuelve un error distinto cuando la fecha se encuentra fuera del intervalo.|Para el tipo **datetime**, OLE DB Driver for SQL Server devuelve un número de error distinto al que se devolvía en versiones anteriores para una fecha que se encuentre fuera del intervalo de fechas admitido.<br /><br /> Concretamente, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 devolvía 22007 para todos los valores de año fuera del intervalo en conversiones de cadena a **datetime**, y OLE DB Driver for SQL Server devuelve 22008 cuando la fecha se encuentra dentro del intervalo admitido por **datetime2** pero fuera del intervalo admitido por **datetime** o **smalldatetime**.|  
|El valor **datetime** trunca las fracciones de segundo y no se redondea si el redondeo cambia el día.|En versiones anteriores a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, el comportamiento del cliente para los valores **datetime** que se enviaban al servidor era redondearlos a la fracción 1/300 de segundo más próxima. En OLE DB Driver for SQL Server, este mismo escenario provoca un truncamiento de fracciones de segundo si al redondear cambia el día.|  
|Posible truncamiento de segundos para el valor **datetime**.|Una aplicación compilada con el controlador OLE DB para SQL Server que se conecta a un servidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2005 truncará segundos y fracciones de segundo para la parte de hora de los datos enviados al servidor si se enlaza con una columna datetime con un identificador de tipo de DBTYPE_DBTIMESTAMP (OLE DB) o SQL_TIMESTAMP (ODBC) y una escala de 0.<br /><br /> Por ejemplo:<br /><br /> Datos de entrada: 1994-08-21 21:21:36.000<br /><br /> Datos insertados: 1994-08-21 21:21:00.000|  
|La conversión de datos OLE DB de DBTYPE_DBTIME a DBTYPE_DATE ya no puede hacer que cambie el día.|En versiones anteriores a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, si la parte correspondiente a la hora de DBTYPE_DATE se encontraba a medio segundo de la medianoche, el código de conversión de OLE DB hacía que el día cambiara. A partir de OLE DB Driver for SQL Server, el día no cambiará (las fracciones de segundo se truncan y no se redondean).|  
|Cambios en la conversión IBCPSession::BCColFmt.|En OLE DB Driver for SQL Server, cuando se usa IBCPSession::BCOColFmt para convertir SQLDATETIME o SQLDATETIME en un tipo de cadena, se exporta un valor fraccionario. Por ejemplo, al convertir un tipo SQLDATETIME en un tipo SQLNVARCHARMAX, las versiones anteriores a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 devolvían<br /> 1989-02-01 00:00:00.<br />El controlador OLE DB para SQL Server devuelve <br />1989-02-01 00:00:00.0000000.|  
|Ahora, las aplicaciones personalizadas que utilizan la API de BCP pueden recibir una advertencia.|La API de BCP generará un mensaje de advertencia si la longitud de los datos es mayor que la longitud especificada en un campo para todos los tipos. Anteriormente, esta advertencia solo se recibía para los tipos de caracteres, pero no se emitía para todos los tipos.|  
|Si se inserta una cadena vacía en un **sql_variant** enlazado como un tipo de fecha y hora, se genera un error.|En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0, al insertar una cadena vacía en un elemento **sql_variant** enlazado como un tipo de fecha y hora no se generaba ningún error. OLE DB Driver for SQL Server genera un error en esta situación.|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] puede devolver resultados diferentes cuando se ejecuta un desencadenador.|Los cambios introducidos en [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] pueden hacer que una aplicación devuelva otros resultados de una instrucción que ha producido la ejecución de un desencadenador cuando **NOCOUNT OFF** estaba activo. En esta situación, es posible que la aplicación genere un error. Para resolver este error, establezca **NOCOUNT ON** en el desencadenador.|  

## <a name="see-also"></a>Consulte también   
 [Controlador OLE DB para SQL Server](../../oledb/oledb-driver-for-sql-server.md)
