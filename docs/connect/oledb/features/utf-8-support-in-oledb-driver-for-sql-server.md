---
title: Compatibilidad de UTF-8 con el controlador OLE DB para SQL Server | Microsoft Docs
description: Compatibilidad de UTF-8 con el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: v-kaywon
ms.author: v-kaywon
ms.openlocfilehash: 4a30b233190817faee581106db5c8a18695a00d1
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2019
ms.locfileid: "59583018"
---
# <a name="utf-8-support-in-ole-db-driver-for-sql-server"></a>Compatibilidad de UTF-8 con el controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

El controlador OLE DB de Microsoft para SQL Server (versión 18.2.1) agrega compatibilidad con la codificación del servidor UTF-8. Para obtener información sobre la compatibilidad con UTF-8 de SQL Server, consulte:
- [Collation and Unicode Support](../../../relational-databases/collations/collation-and-unicode-support.md)
- [Compatibilidad con UTF-8](../../../sql-server/what-s-new-in-sql-server-ver15.md#utf-8-support-ctp-23)

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
  
## <a name="see-also"></a>Consulte también  
[Controlador OLE DB para las características de SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md) 

[Compatibilidad de UTF-16 con el controlador OLE DB para SQL Server](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)    
  
  
