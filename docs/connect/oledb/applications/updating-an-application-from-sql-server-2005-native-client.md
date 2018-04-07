---
title: Actualizar una aplicación de SQL Server 2005 Native Client | Documentos de Microsoft
description: Actualizar una aplicación de SQL Server 2005 Native Client
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, updating applications
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e583abd0a5d84d4842a441fcb8093bbfcf6b9b26
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>Actualizar una aplicación desde SQL Server 2005 Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Este tema describen los cambios en el controlador de OLE DB para SQL Server desde [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  

 Al actualizar desde Microsoft Data Access Components (MDAC) a controlador de OLE DB para SQL Server, también puede ver algunas diferencias de comportamiento. Para obtener más información, consulte [actualizar una aplicación a controlador de OLE DB para SQL Server de MDAC](../../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).  

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 incluidos con [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 incluidos con [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.5 se incluyó en [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 se incluyó en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] y [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)].  

|Cambió el comportamiento en el controlador de OLE DB para SQL Server en comparación con [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client|Description|  
|------------------------------------------------------------------------------------|-----------------|  
|OLE DB solamente rellena los datos hasta la escala definida.|Para las conversiones donde los datos convertidos se envían al servidor, el controlador OLE DB para SQL Server rellena los ceros finales en datos solo hasta la longitud máxima de **datetime** valores. En SQL Server Native Client 9.0 los datos se rellenaban hasta 9 dígitos.|  
|Validación de DBTYPE_DBTIMESTAMP para ICommandWithParameter::SetParameterInfo.|Controlador de OLE DB para SQL Server implementa el requisito de OLE DB para *bScale* en ICommandWithParameter::SetParameterInfo que se establecerá con precisión de fracciones de segundo para DBTYPE_DBTIMESTAMP.|  
|El **sp_columns** procedimiento almacenado ahora devuelve **"N"** en lugar de **"N"** para la columna IS_NULLABLE.|En el controlador OLE DB para SQL Server, **sp_columns** procedimiento almacenado ahora devuelve **"N"** en lugar de **"N"** para una columna IS_NULLABLE.|  
|SQLSetDescRec y SQLBindParameter, SQLBindCol ahora realizan una comprobación de coherencia.|Anteriores a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, establecimiento de SQL_DESC_DATA_PTR no producía la comprobación de coherencia para cualquier tipo de descriptor en SQLSetDescRec, SQLBindParameter o SQLBindCol.|  
|SQLCopyDesc ahora se realiza la comprobación de coherencia de descriptor.|Anteriores a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, SQLCopyDesc no hizo una comprobación de coherencia cuando el campo SQL_DESC_DATA_PTR se estableció en un registro concreto.|  
|SQLGetDescRec ya no es una descriptor comprobación de coherencia.|Anteriores a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, SQLGetDescRec realiza una comprobación de coherencia del descriptor cuando se establece el campo SQL_DESC_DATA_PTR. Esto último no era un requisito de la especificación de ODBC y, en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) y versiones posteriores, ya no se realiza esta comprobación de coherencia.|  
|Se devuelve un error distinto cuando la fecha se encuentra fuera del intervalo.|Para el **datetime** tipo, un número de error diferentes devueltos por controlador OLE DB para SQL Server para una fecha fuera del intervalo que se devolvió en versiones anteriores.<br /><br /> En concreto, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 devolvía 22007 para todos los valores de año de intervalo en conversiones de cadena a fuera **datetime**, y el controlador OLE DB para SQL Server devuelve 22008 cuando la fecha está dentro del intervalo admitido por **datetime2** , pero fuera del intervalo admitido por **datetime** o **smalldatetime**.|  
|**fecha y hora** valor trunca las fracciones de segundo y no de ida y vuelta if redondeo cambia el día.|Anteriores a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, el comportamiento de cliente **datetime** valores que se envían al servidor era redondearlos a más cercano 1/300 de segundo. En el controlador OLE DB para SQL Server, este mismo escenario provoca un truncamiento de fracciones de segundo si al redondear cambia el día.|  
|Posible truncamiento de segundos para **datetime** valor.|Una aplicación compilada con controlador de OLE DB para SQL Server que se conecta a un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] server 2005 truncará segundos y fracciones de segundo para la parte de hora de los datos enviados al servidor si enlaza a una columna de fecha y hora con un identificador de tipo de (DBTYPE_DBTIMESTAMP OLE DB) o SQL_TIMESTAMP (ODBC) y una escala de 0.<br /><br /> Por ejemplo:<br /><br /> Datos de entrada: 1994-08-21 21:21:36.000<br /><br /> Datos insertados: 1994-08-21 21:21:00.000|  
|La conversión de datos OLE DB de DBTYPE_DBTIME a DBTYPE_DATE ya no puede hacer que cambie el día.|En versiones anteriores a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, si la parte correspondiente a la hora de DBTYPE_DATE se encontraba a medio segundo de la medianoche, el código de conversión de OLE DB hacía que el día cambiara. En el controlador OLE DB para SQL Server, el día no cambiará (las fracciones de segundo se truncan y no se redondean).|  
|Cambios de conversión de IBCPSession::BCColFmt.|En el controlador OLE DB para SQL Server, cuando se usa IBCPSession::BCOColFmt para convertir SQLDATETIME o SQLDATETIME en un tipo de cadena, se exporta un valor fraccionario. Por ejemplo, al convertir un tipo SQLDATETIME en un tipo SQLNVARCHARMAX, versiones anteriores a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 devuelve<br /> 1989-02-01 00:00:00.<br />Devuelve el controlador OLE DB para SQL Server <br />1989-02-01 00:00:00.0000000.|  
|Ahora, las aplicaciones personalizadas que utilizan la API de BCP pueden recibir una advertencia.|La API de BCP generará un mensaje de advertencia si la longitud de los datos es mayor que la longitud especificada en un campo para todos los tipos. Anteriormente, esta advertencia solo se recibía para los tipos de caracteres, pero no se emitía para todos los tipos.|  
|Insertar una cadena vacía en un **sql_variant** enlazado como un tipo de fecha y hora genera un error.|En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0, insertar una cadena vacía en un **sql_variant** enlazado como un tipo de fecha y hora no generaba un error. Controlador OLE DB para SQL Server genera un error en esta situación.|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] puede devolver resultados diferentes cuando se ejecuta un desencadenador.|Cambios realizados en [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] pueden hacer que una aplicación para que devuelva resultados diferentes de una instrucción que ha causado un desencadenador que se ejecuta cuando **NOCOUNT OFF** estaba activo. En esta situación, es posible que la aplicación genere un error. Para resolver este error, establezca **NOCOUNT ON** en la llamada SQLMoreResults para avanzar al siguiente de resultados o el desencadenador.|  

## <a name="see-also"></a>Vea también   
 [Programación del controlador OLE DB para SQL Server](../../oledb/oledb-driver-for-sql-server-programming.md)
