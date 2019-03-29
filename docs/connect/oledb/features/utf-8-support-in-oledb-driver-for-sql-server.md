---
title: Compatibilidad de UTF-8 con el controlador OLE DB para SQL Server | Microsoft Docs
description: Compatibilidad de UTF-8 con el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 03/27/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: v-kaywon
ms.author: v-kaywon
ms.openlocfilehash: b7f138438d522c9da1b7ef74acbaf963e17d6144
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58492607"
---
# <a name="utf-8-support-in-ole-db-driver-for-sql-server"></a>Compatibilidad de UTF-8 con el controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Controlador OLE DB de Microsoft para SQL Server (versión 18.2.1) agrega compatibilidad con la codificación UTF-8 del servidor. Para obtener información sobre la compatibilidad con UTF-8 de SQL Server, consulte:
- [Collation and Unicode Support](../../../relational-databases/collations/collation-and-unicode-support.md)
- [Compatibilidad con UTF-8](../../../sql-server/what-s-new-in-sql-server-ver15.md#utf-8-support-ctp-23)

## <a name="data-insertion-into-a-utf-8-encoded-char-or-varchar-column"></a>Inserción de datos en un UTF-8 codificada columna CHAR o VARCHAR
Al crear un búfer de parámetro de entrada para la inserción, se describe el búfer mediante el uso de una matriz de [estructuras DBBINDING](https://go.microsoft.com/fwlink/?linkid=2071182). Cada estructura DBBINDING asocia un solo parámetro para el búfer del consumidor y contiene información como la longitud y el tipo del valor de datos. Un búfer de parámetro de entrada de tipo CHAR, el *wType* de DBBINDING estructura debe establecerse en DBTYPE_STR. Un búfer de parámetro de entrada de tipo WCHAR, el *wType* de DBBINDING estructura debe establecerse en DBTYPE_WSTR.

Al ejecutar un comando con parámetros, el controlador crea información de tipo de datos de parámetro. Si el tipo de búfer de entrada y los datos del parámetro tipo de coincidencia, se realiza ninguna conversión en el controlador. En caso contrario, el controlador convierte el búfer de parámetro de entrada para el tipo de datos de parámetro. El tipo de datos de parámetro se puede establecer explícitamente por el usuario mediante una llamada a [ICommandWithParameters:: SetParameterInfo](https://go.microsoft.com/fwlink/?linkid=2071577). Si no se proporciona la información, el controlador deriva la información de tipo de datos de parámetro (a) al recuperar los metadatos de columna desde el servidor cuando se prepara la instrucción o (b) al intentar una conversión predeterminada del tipo de datos de parámetro de entrada.

El búfer de parámetro de entrada puede convertirse a la intercalación de columna del servidor, el controlador o el servidor según el tipo de datos de búfer de entrada y el tipo de datos de parámetro. Durante la conversión, pueden perderse datos si la página de códigos del cliente o la página de códigos de intercalación de base de datos no puede representar todos los caracteres del búfer de entrada. La tabla siguiente describe el proceso de conversión al insertar datos en un UTF-8 habilita columna:

|Tipo de búfer de datos|Tipo de datos de parámetro|Conversión|Medida de usuario|
|---             |---                |---       |---            |
|DBTYPE_STR|DBTYPE_STR|Conversión de servidor de página de códigos del cliente a la página de códigos de intercalación de base de datos; conversión de servidor de página de códigos de intercalación de base de datos a la página de códigos de intercalación de columna.|Asegúrese de que la página de códigos del cliente y la página de códigos de intercalación de base de datos pueden representar todos los caracteres de los datos de entrada. Por ejemplo, para insertar un carácter polaco, se pudo establecer la página de códigos del cliente a 1250 (ANSI Europa Central), y la intercalación de base de datos podría usar polaco como el designador de intercalación (por ejemplo, Polish_100_CI_AS_SC) o ser UTF-8 habilitados.|
|DBTYPE_STR|DBTYPE_WSTR|Conversión de controlador de página de códigos del cliente a la codificación UTF-16; conversión de servidor de la codificación UTF-16 en la página de códigos de intercalación de columna.|Asegúrese de que la página de códigos del cliente puede representar todos los caracteres de los datos de entrada. Por ejemplo, para insertar un carácter polaco, la página de códigos del cliente pudo establecerse 1250 (ANSI Europa Central).|
|DBTYPE_WSTR|DBTYPE_STR|Conversión de controlador de codificación UTF-16 en la página de códigos de intercalación de base de datos; conversión de servidor de página de códigos de intercalación de base de datos a la página de códigos de intercalación de columna.|Asegúrese de que la página de códigos de intercalación de base de datos puede representar todos los caracteres de los datos de entrada. Por ejemplo, para insertar un carácter polaco, la página de códigos de intercalación de base de datos podría usar polaco como el designador de intercalación (por ejemplo, Polish_100_CI_AS_SC) o ser UTF-8 habilitados.|
|DBTYPE_WSTR|DBTYPE_WSTR|Conversión de servidor de UTF-16 en la página de códigos de intercalación de columna.|Ninguno.|

## <a name="data-retrieval-from-a-utf-8-encoded-char-or-varchar-column"></a>Recuperación de datos desde un UTF-8 codificada columna CHAR o VARCHAR
Al crear un búfer para los datos recuperados, se describe el búfer mediante el uso de una matriz de [estructuras DBBINDING](https://go.microsoft.com/fwlink/?linkid=2071182). Cada estructura DBBINDING asocia una sola columna en la fila recuperada. Para recuperar los datos de columna como CHAR, establezca el *wType* de la estructura DBBINDING en DBTYPE_STR. Para recuperar los datos de columna como WCHAR, establezca el *wType* de la estructura DBBINDING en DBTYPE_WSTR.

Para el indicador de tipo de búfer de resultados DBTYPE_STR, el controlador convierte los datos con codificación UTF-8 para el cliente de codificación. El usuario debe asegurarse de que el cliente de codificación puede representar los datos de la columna de UTF-8, en caso contrario, puede producirse pérdida de datos.

Para el indicador de tipo de búfer de resultados DBTYPE_WSTR, el controlador convierte los datos con codificación UTF-8 para la codificación UTF-16.
  
## <a name="see-also"></a>Consulte también  
[Controlador OLE DB para las características de SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md) 

[Compatibilidad de UTF-16 con el controlador OLE DB para SQL Server](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)    
  
  
