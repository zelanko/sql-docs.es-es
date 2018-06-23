---
title: Actualizar una aplicación de SQL Server 2005 Native Client | Documentos de Microsoft
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, updating applications
ms.assetid: 1e1e570c-7f14-4e16-beab-c328e3fbdaa8
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1b064616079b968ee823f4eef6bc1a2b4a4718ea
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197410"
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>Actualizar una aplicación desde SQL Server 2005 Native Client
  En este tema se describen los cambios importantes en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con respecto a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Al realizar una actualización de Microsoft Data Access Components (MDAC) a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, también es posible que observe algunas diferencias de comportamiento. Para obtener más información, consulte [actualizar una aplicación a SQL Server Native Client de MDAC](updating-an-application-to-sql-server-native-client-from-mdac.md).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 incluidos con [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 incluidos con [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.5 se incluyó en [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 se incluyó en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] y [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)].  
  
|Cambios de comportamiento en SQL Server Native Client desde [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]|Descripción|  
|------------------------------------------------------------------------------------|-----------------|  
|OLE DB solamente rellena los datos hasta la escala definida.|Para las conversiones en las que los datos convertidos se envían al servidor, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (a partir de [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) solamente rellena los datos con ceros a la derecha hasta la longitud máxima de los valores `datetime`. En SQL Server Native Client 9.0 los datos se rellenaban hasta 9 dígitos.|  
|Validación de DBTYPE_DBTIMESTAMP para ICommandWithParameter::SetParameterInfo.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (a partir de [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) implementa el requisito de OLE DB para *bScale* en ICommandWithParameter::SetParameterInfo que se establecerá con precisión de fracciones de segundo para DBTYPE_DBTIMESTAMP.|  
|El `sp_columns` procedimiento almacenado ahora devuelve **"N"** en lugar de **"N"** para la columna IS_NULLABLE.|A partir de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]), `sp_columns` procedimiento almacenado ahora devuelve **"N"** en lugar de **"N"** para una columna IS_NULLABLE.|  
|SQLSetDescRec y SQLBindParameter, SQLBindCol ahora realizan una comprobación de coherencia.|Anteriores a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, establecimiento de SQL_DESC_DATA_PTR no producía la comprobación de coherencia para cualquier tipo de descriptor en SQLSetDescRec, SQLBindParameter o SQLBindCol.|  
|SQLCopyDesc ahora se realiza la comprobación de coherencia de descriptor.|Anteriores a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, SQLCopyDesc no hizo una comprobación de coherencia cuando el campo SQL_DESC_DATA_PTR se estableció en un registro concreto.|  
|SQLGetDescRec ya no es una descriptor comprobación de coherencia.|Anteriores a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, SQLGetDescRec realiza una comprobación de coherencia del descriptor cuando se establece el campo SQL_DESC_DATA_PTR. Esto último no era un requisito de la especificación de ODBC y, en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) y versiones posteriores, ya no se realiza esta comprobación de coherencia.|  
|Se devuelve un error distinto cuando la fecha se encuentra fuera del intervalo.|Para el tipo `datetime`, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (a partir de [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) devuelve un número de error distinto al que se devolvía en versiones anteriores para una fecha que se encuentre fuera del intervalo de fechas admitido.<br /><br /> Concretamente, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 devolvía 22007 para todos los valores de año fuera del intervalo en conversiones de cadenas a `datetime`, y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client a partir de la versión 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) devuelve 22008 cuando la fecha se encuentra dentro del intervalo admitido por `datetime2` pero fuera del intervalo admitido por `datetime` o `smalldatetime`.|  
|El valor `datetime` trunca las fracciones de segundo y no se redondea si el redondeo cambia el día.|En versiones anteriores a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, el comportamiento del cliente para los valores `datetime` que se enviaban al servidor era redondearlos a la fracción 1/300 de segundo más próxima. A partir de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, este mismo escenario provoca un truncamiento de fracciones de segundo si al redondear cambia el día.|  
|Posible truncamiento de segundos para el valor `datetime`.|Una aplicación compilada con [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client (o posterior) que se conecta a un servidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2005 truncará segundos y fracciones de segundo para la parte de hora de los datos enviados al servidor si se enlaza con una columna de fecha y hora con un identificador de tipo DBTYPE_DBTIMESTAMP (OLE DB) o SQL_TIMESTAMP (ODBC) y una escala de 0.<br /><br /> Por ejemplo:<br /><br /> Datos de entrada: 1994-08-21 21:21:36.000<br /><br /> Datos insertados: 1994-08-21 21:21:00.000|  
|La conversión de datos OLE DB de DBTYPE_DBTIME a DBTYPE_DATE ya no puede hacer que cambie el día.|En versiones anteriores a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, si la parte correspondiente a la hora de DBTYPE_DATE se encontraba a medio segundo de la medianoche, el código de conversión de OLE DB hacía que el día cambiara. A partir de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, el día no cambiará (las fracciones de segundo se truncan y no se redondean).|  
|Cambios de conversión de IBCPSession::BCColFmt.|A partir de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, cuando usa IBCPSession::BCOColFmt para convertir SQLDATETIME o SQLDATETIME en un tipo de cadena, un valor fraccionario se exporta. Por ejemplo, al convertir un tipo SQLDATETIME en un tipo SQLNVARCHARMAX, las versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client devolvían<br /><br /> 1989-02-01 00:00:00. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 y versiones posteriores devuelven 1989-02-01 00:00:00.0000000.|  
|El tamaño de los datos enviados debe coincidir con la longitud especificada en SQL_LEN_DATA_AT_EXEC.|Cuando se utiliza SQL_LEN_DATA_AT_EXEC, el tamaño de los datos debe coincidir con la longitud especificada en SQL_LEN_DATA_AT_EXEC. Puede usar SQL_DATA_AT_EXEC, pero resulta mucho más ventajoso desde el punto de vista del rendimiento utilizar SQL_LEN_DATA_AT_EXEC.|  
|Ahora, las aplicaciones personalizadas que utilizan la API de BCP pueden recibir una advertencia.|La API de BCP generará un mensaje de advertencia si la longitud de los datos es mayor que la longitud especificada en un campo para todos los tipos. Anteriormente, esta advertencia solo se recibía para los tipos de caracteres, pero no se emitía para todos los tipos.|  
|Si se inserta una cadena vacía en un `sql_variant` enlazado como un tipo de fecha y hora, se genera un error.|En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0, al insertar una cadena vacía en un elemento `sql_variant` enlazado como un tipo de fecha y hora no se generaba ningún error. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 (y posterior) genera un error en esta situación.|  
|Validación de parámetros SQL_C_TYPE_TIMESTAMP y DBTYPE_DBTIMESTAMP más estricta.|Anteriores a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client, `datetime` los valores se redondean para ajustarse a la escala de `datetime` y `smalldatetime` columnas por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client (y posteriores) aplica reglas de validación más estrictas, que se definen en la especificación básica de ODBC para las fracciones de segundo. Si un valor de parámetro no puede convertirse en el tipo SQL utilizando la escala especificada o no puede implicarse mediante el enlace del cliente sin que se produzca un truncamiento de los dígitos finales, se devuelve un error.|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] puede devolver resultados diferentes cuando se ejecuta un desencadenador.|Los cambios introducidos en [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] pueden hacer que una aplicación devuelva resultados diferentes de una instrucción que produjo la ejecución de un desencadenador cuando `NOCOUNT OFF` estaba activo. En esta situación, es posible que la aplicación genere un error. Para resolver este error, establezca `NOCOUNT ON` en la llamada SQLMoreResults para avanzar al siguiente de resultados o el desencadenador.|  
  
## <a name="see-also"></a>Vea también  
 [Programación de SQL Server Native Client](../sql-server-native-client-programming.md)  
  
  