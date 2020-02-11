---
title: Realizar operaciones de copia masiva (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 25144e13b4e129209356d0e4e4ebe37f9a3c5d1c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63200818"
---
# <a name="performing-bulk-copy-operations-odbc"></a>Realizar operaciones de copia masiva (ODBC)
  ODBC estándar no admite directamente las operaciones de copia masiva de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versión 7.0 o posteriores, el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client admite las funciones de DB-Library que realizan las operaciones de copia masiva de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta extensión específica del controlador proporciona una ruta de acceso sencilla de actualizar para las aplicaciones de DB-Library existentes que usan las funciones de copia masiva. El soporte técnico de copia masiva especializado se encuentra en los archivos siguientes:  
  
-   sqlncli.h  
  
     Incluye prototipos de función y definiciones de constante para las funciones de copia masiva. sqlncli.h debe estar incluido en la aplicación ODBC que realiza las operaciones de copia masiva y encontrarse en la ruta de inclusión de la aplicación cuando se compila.  
  
-   sqlncli11.lib  
  
     Debe estar en la ruta de acceso de la biblioteca del vinculador y estar especificado como un archivo que se va a vincular. sqlncli11.lib se distribuye con el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
-   sqlncli11.dll  
  
     Debe estar presente en el momento de la ejecución. sqlncli11.dll se distribuye con el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
> [!NOTE]  
>  La función **SQLBulkOperations** de ODBC no tiene ninguna relación [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con las funciones de copia masiva. Las aplicaciones deben utilizar las funciones de copia masiva específicas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="minimally-logging-bulk-copies"></a>Registrar mínimamente las copias masivas  
 Con el modelo de recuperación completo, todas las operaciones de inserción de filas que se efectúan durante la carga masiva se registran por completo en el registro de transacciones. Cuando la carga es de un gran volumen de datos, esto puede causar que el registro de transacciones se llene rápidamente. Bajo ciertas condiciones, es posible un registro mínimo. El registro mínimo reduce la posibilidad de que una operación de carga masiva llene el espacio del registro y es más eficaz también que el registro completo.  
  
 Para obtener información sobre el uso del registro mínimo, consulte [requisitos previos para el registro mínimo durante la importación en bloque](../import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
## <a name="remarks"></a>Observaciones  
 Al utilizar bcp.exe en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o posterior, podrían aparecer errores en situaciones donde no había errores en versiones anteriores a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Esto es porque en las versiones posteriores, bcp.exe no realiza ya la conversión de tipos de datos implícita. En versiones anteriores a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], bcp.exe convertía los datos numéricos al tipo de datos money, si la tabla de destino tenía el tipo de datos money. Sin embargo, en esa situación, bcp.exe simplemente truncaba los campos adicionales. A partir [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]de, si los tipos de datos no coinciden entre el archivo y la tabla de destino, BCP. exe producirá un error si hay datos que tendrían que truncarse para ajustarse a la tabla de destino. Para resolver este error, corrija los datos para que coincidan con el tipo de datos de destino. Opcionalmente, utilice bcp.exe desde una versión anterior a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Utilizar archivos de datos y archivos de formato](using-data-files-and-format-files.md)  
  
-   [Copia masiva de variables de programa](bulk-copying-from-program-variables.md)  
  
-   [Administrar tamaños de lote de copia masiva](managing-bulk-copy-batch-sizes.md)  
  
-   [Copia masiva de datos de texto e imagen](bulk-copying-text-and-image-data.md)  
  
-   [Convertir un programa de copia masiva de DB-Library a ODBC](converting-from-db-library-to-odbc-bulk-copy.md)  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)   
 [Importar y exportar datos en bloque &#40;SQL Server&#41;](../import-export/bulk-import-and-export-of-data-sql-server.md)  
  
  
