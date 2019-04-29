---
title: Realizar operaciones de copia masiva (ODBC) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC]
- ODBC, bulk copy operations
- minimally logged operations [SQL Server Native Client]
- bulk copy [ODBC], about bulk copy
ms.assetid: 5c793405-487c-4f52-88b8-0091d529afb3
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 98b59d3b5d3c0679ec8fb060b66afa44a38c1262
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63013932"
---
# <a name="performing-bulk-copy-operations-odbc"></a>Realizar operaciones de copia masiva (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC estándar no admite directamente las operaciones de copia masiva de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versión 7.0 o posteriores, el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client admite las funciones de DB-Library que realizan las operaciones de copia masiva de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta extensión específica del controlador proporciona una ruta de acceso sencilla de actualizar para las aplicaciones de DB-Library existentes que usan las funciones de copia masiva. El soporte técnico de copia masiva especializado se encuentra en los archivos siguientes:  
  
-   sqlncli.h  
  
     Incluye prototipos de función y definiciones de constante para las funciones de copia masiva. sqlncli.h debe estar incluido en la aplicación ODBC que realiza las operaciones de copia masiva y encontrarse en la ruta de inclusión de la aplicación cuando se compila.  
  
-   sqlncli11.lib  
  
     Debe estar en la ruta de acceso de la biblioteca del vinculador y estar especificado como un archivo que se va a vincular. sqlncli11.lib se distribuye con el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
-   sqlncli11.dll  
  
     Debe estar presente en el momento de la ejecución. sqlncli11.dll se distribuye con el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
> [!NOTE]  
>  ODBC **SQLBulkOperations** función no tiene ninguna relación con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funciones de copia masiva. Las aplicaciones deben utilizar las funciones de copia masiva específicas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="minimally-logging-bulk-copies"></a>Registrar mínimamente las copias masivas  
 Con el modelo de recuperación completo, todas las operaciones de inserción de filas que se efectúan durante la carga masiva se registran por completo en el registro de transacciones. Cuando la carga es de un gran volumen de datos, esto puede causar que el registro de transacciones se llene rápidamente. Bajo ciertas condiciones, es posible un registro mínimo. El registro mínimo reduce la posibilidad de que una operación de carga masiva llene el espacio del registro y es más eficaz también que el registro completo.  
  
 Para obtener información sobre el uso de registro mínimo, vea [Prerequisites for Minimal Logging la importación en bloque](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
## <a name="remarks"></a>Comentarios  
 Al utilizar bcp.exe en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o posterior, podrían aparecer errores en situaciones donde no había errores en versiones anteriores a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Esto es porque en las versiones posteriores, bcp.exe no realiza ya la conversión de tipos de datos implícita. En versiones anteriores a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], bcp.exe convertía los datos numéricos al tipo de datos money, si la tabla de destino tenía el tipo de datos money. Sin embargo, en esa situación, bcp.exe simplemente truncaba los campos adicionales. A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], si los datos tipos no coinciden con el archivo y la tabla de destino, bcp.exe producirá un error si no hay ningún dato que tenga que truncarse para ajustarse a la tabla de destino. Para resolver este error, corrija los datos para que coincidan con el tipo de datos de destino. Opcionalmente, utilice bcp.exe desde una versión anterior a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Utilizar archivos de datos y archivos de formato](../../relational-databases/native-client-odbc-bulk-copy-operations/using-data-files-and-format-files.md)  
  
-   [Copia masiva de variables de programa](../../relational-databases/native-client-odbc-bulk-copy-operations/bulk-copying-from-program-variables.md)  
  
-   [Administrar tamaños de lote de copia masiva](../../relational-databases/native-client-odbc-bulk-copy-operations/managing-bulk-copy-batch-sizes.md)  
  
-   [Copia masiva de datos de texto e imagen](../../relational-databases/native-client-odbc-bulk-copy-operations/bulk-copying-text-and-image-data.md)  
  
-   [Convertir un programa de copia masiva de DB-Library a ODBC](../../relational-databases/native-client-odbc-bulk-copy-operations/converting-from-db-library-to-odbc-bulk-copy.md)  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [Importar y exportar datos en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)  
  
  
