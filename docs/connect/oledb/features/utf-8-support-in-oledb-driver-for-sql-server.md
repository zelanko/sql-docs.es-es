---
title: Compatibilidad de UTF-8 con el controlador OLE DB para SQL Server | Microsoft Docs
description: Compatibilidad de UTF-8 con el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 04/23/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: v-kaywon
ms.author: v-kaywon
ms.openlocfilehash: fb596365f284a141b5e57bfc8601427fe603d73d
ms.sourcegitcommit: 49f3d12c0a46d98b82513697a77a461340f345e1
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70392018"
---
# <a name="utf-8-support-in-ole-db-driver-for-sql-server"></a>Compatibilidad de UTF-8 con el controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

El controlador OLE DB de Microsoft para SQL Server (versión 18.2.1) agrega compatibilidad con la codificación del servidor UTF-8. Para obtener información sobre la compatibilidad con UTF-8 de SQL Server, consulte:
- [Collation and Unicode Support](../../../relational-databases/collations/collation-and-unicode-support.md)
- [Compatibilidad con UTF-8](#ctp23)

> [!IMPORTANT]
> Microsoft OLE DB driver for SQL Server usa la función [GetACP](https://docs.microsoft.com/windows/win32/api/winnls/nf-winnls-getacp) para determinar la codificación del búfer de entrada DBTYPE_STR. No se admiten los escenarios en los que GetACP devuelve una codificación UTF-8. Si el búfer necesita almacenar datos Unicode, el tipo de datos del búfer debe establecerse en DBTYPE_WSTR (codificación UTF-16).

## <a name="data-insertion-into-a-utf-8-encoded-char-or-varchar-column"></a>Inserción de datos en una columna CHAR o VARCHAR codificada con UTF-8
Al crear un búfer de parámetro de entrada para la inserción, se describe el búfer mediante el uso de una matriz de [estructuras DBBINDING](https://go.microsoft.com/fwlink/?linkid=2071182). Cada estructura DBBINDING asocia un solo parámetro al búfer del consumidor y contiene información como la longitud y el tipo del valor de datos. Para un búfer de parámetro de entrada de tipo CHAR, el valor *wType* de la estructura DBBINDING debe establecerse en DBTYPE_STR. Para un búfer de parámetro de entrada de tipo WCHAR, el valor *wType* de la estructura DBBINDING debe establecerse en DBTYPE_WSTR.

Al ejecutar un comando con parámetros, el controlador crea información de tipo de datos de parámetro. Si el tipo de búfer de entrada y el tipo de datos del parámetro coinciden, no se realiza ninguna conversión en el controlador. En caso contrario, el controlador convierte el búfer del parámetro de entrada en el tipo de datos de parámetro. El tipo de datos de parámetro se puede establecer explícitamente por el usuario mediante una llamada a [ICommandWithParameters::SetParameterInfo](https://go.microsoft.com/fwlink/?linkid=2071577). Si no se proporciona la información, el controlador deriva la información del tipo de datos de parámetro mediante a) la recuperación de los metadatos de columna desde el servidor cuando se prepara la instrucción, o b) el intento de realizar una conversión predeterminada desde el tipo de datos de parámetro de entrada.

El búfer de parámetro de entrada puede convertirse a la intercalación de columna del servidor por el controlador o el servidor, según el tipo de datos del búfer de entrada y el tipo de datos de parámetro. Durante la conversión, pueden perderse datos si la página de código del cliente o la página de código de intercalación de la base de datos no puede representar todos los caracteres en el búfer de entrada. La tabla siguiente describe el proceso de conversión al insertar datos en una columna habilitada para UTF-8:

|Tipo de datos del búfer|Tipo de datos de parámetro|Conversión|Precaución del usuario|
|---             |---                |---       |---            |
|DBTYPE_STR|DBTYPE_STR|Conversión del servidor de la página de códigos del cliente a la página de códigos de intercalación de la base de datos; conversión del servidor de la página de códigos de intercalación de base de datos a la página de códigos de intercalación de columna.|Asegúrese de que la página de códigos del cliente y la página de códigos de intercalación de base de datos pueden representar todos los caracteres de los datos de entrada. Por ejemplo, para insertar un carácter polaco, la página de códigos del cliente podría establecerse en 1250 (ANSI Europa Central), y la intercalación de la base de datos podría usar el polaco como el designador de intercalación (por ejemplo, Polish_100_CI_AS_SC) o estar habilitada para UTF-8.|
|DBTYPE_STR|DBTYPE_WSTR|Conversión de controlador de página de códigos del cliente a codificación UTF-16; conversión de servidor de la codificación UTF-16 a la página de códigos de intercalación de columna.|Asegúrese de que la página de códigos del cliente puede representar todos los caracteres de los datos de entrada. Por ejemplo, para insertar un carácter polaco, la página de códigos del cliente podría establecerse en 1250 (ANSI Europa Central).|
|DBTYPE_WSTR|DBTYPE_STR|Conversión del servidor de la codificación UTF-16 a la página de códigos de intercalación de la base de datos; conversión del servidor de la página de códigos de intercalación de base de datos a la página de códigos de intercalación de columna.|Asegúrese de que la página de códigos de intercalación de base de datos pueden representar todos los caracteres de los datos de entrada. Por ejemplo, para insertar un carácter polaco, la página de códigos de intercalación de la base de datos podría usar el polaco como el designador de intercalación (por ejemplo, Polish_100_CI_AS_SC) o estar habilitada para UTF-8.|
|DBTYPE_WSTR|DBTYPE_WSTR|Conversión de servidor de UTF-16 a la página de códigos de intercalación de columna.|Ninguno.|

## <a name="data-retrieval-from-a-utf-8-encoded-char-or-varchar-column"></a>Recuperación de datos de una columna CHAR o VARCHAR codificada con UTF-8
Al crear un búfer para datos recuperados, se describe el búfer mediante el uso de una matriz de [estructuras DBBINDING](https://go.microsoft.com/fwlink/?linkid=2071182). Cada estructura DBBINDING asocia una sola columna en la fila recuperada. Para recuperar los datos de columna como CHAR, establezca el valor *wType* de la estructura DBBINDING en DBTYPE_STR. Para recuperar los datos de columna como WCHAR, establezca el valor *wType* de la estructura DBBINDING en DBTYPE_WSTR.

Para el indicador de tipo de búfer de resultados DBTYPE_STR, el controlador convierte los datos con codificación UTF-8 al cliente de codificación. El usuario debe asegurarse de que el cliente de codificación puede representar los datos de la columna de UTF-8, en caso contrario, puede producirse pérdida de datos.

Para el indicador de tipo de búfer de resultados DBTYPE_WSTR, el controlador convierte los datos con codificación UTF-8 a la codificación UTF-16.

<a name="ctp23"></a>

### <a name="utf-8-support-sql-server-2019-ctp-23"></a>Compatibilidad con UTF-8 (SQL Server 2019 CTP 2.3)

[!INCLUDE[ss2019](../../../includes/sssqlv15-md.md)] presenta la compatibilidad total para utilizar la ampliamente utilizada codificación de caracteres UTF-8 como codificación de importación o exportación, o bien como intercalación de columna o base de datos para los datos de texto. UTF-8 se permite en los tipos de datos `CHAR` y `VARCHAR`, y se habilita al crear o cambiar la intercalación de un objeto a una intercalación con el sufijo `UTF8`.

Por ejemplo, de `LATIN1_GENERAL_100_CI_AS_SC` a `LATIN1_GENERAL_100_CI_AS_SC_UTF8`. UTF-8 solo está disponible para las intercalaciones de Windows que admiten caracteres adicionales, tal y como se presentó en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. `NCHAR` y `NVARCHAR` solo permiten la codificación UTF-16 y no se han realizado cambios.

Esta característica puede proporcionar ahorros significativos de almacenamiento, según el juego de caracteres que se esté usando. Por ejemplo, si se cambia un tipo de datos de columna existente con cadenas ASCII (latinas) de `NCHAR(10)` a `CHAR(10)` utilizando una intercalación habilitada para UTF-8, se reducen a la mitad los requisitos de almacenamiento. Esto se debe a que `NCHAR(10)` requiere 20 bytes para el almacenamiento, mientras que `CHAR(10)` necesita 10 bytes para la misma cadena Unicode.

Para más información, consulte [Compatibilidad con la intercalación y Unicode](../../../relational-databases/collations/collation-and-unicode-support.md).

**CTP 2.1** agrega la posibilidad de seleccionar la intercalación de UTF-8 como valor predeterminado durante la configuración de [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)].

**CTP 2.2** agrega la posibilidad de usar la codificación de caracteres UTF-8 con la replicación de SQL Server.

**CTP 2.3** agrega la posibilidad de usar la codificación de caracteres UTF-8 con una replicación de BIN2 (UTF8_BIN2).

## <a name="see-also"></a>Consulte también  
[Controlador OLE DB para las características de SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md) 

[Compatibilidad de UTF-16 con el controlador OLE DB para SQL Server](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)    
  
  
