---
title: Elegir un destino (SQL Server importar y exportar) | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.chooseadestination.f1
ms.assetid: 1898be15-3e69-42d3-8ecb-3733c9f6c8e3
caps.latest.revision: 104
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 4ff3c7c8413bd6b535e1c5f95e2a7b06b397c053
ms.contentlocale: es-es
ms.lasthandoff: 08/28/2017

---
# <a name="choose-a-destination-sql-server-import-and-export-wizard"></a>Elegir un destino (Asistente para importación y exportación de SQL Server)
 Después de proporcionar información sobre el origen de datos y la manera de conectarse a él, el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra la página **Elegir un destino**. En esta página, debe proporcionar información sobre el destino de datos y la manera de conectarse a él.
  
Para obtener más información sobre los destinos de datos que puede usar, consulte [¿Qué orígenes de datos y destinos puedo usar?](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources). 

## <a name="screen-shot-of-the-destination-page"></a>Captura de pantalla de la página Destino
En la captura de pantalla siguiente, se muestra la primera parte de la página **Seleccionar un destino** del asistente. El resto de la página tiene un número variable de opciones que depende el destino que elija aquí.

![Elegir un destino](../../integration-services/import-export-data/media/choose-destination.png)

## <a name="choose-a-destination"></a>Elegir un destino
 **Destino**  
 Para especificar el destino, seleccione un proveedor de datos que pueda importar los datos al destino.
 
-   **El proveedor de datos que necesita es normalmente obvio con su nombre**, ya que el nombre del proveedor suele contener el nombre del destino: por ejemplo, *archivos planos* destino, Microsoft *Excel*, Microsoft *acceso*, .net Framework Data Provider para *SqlServer*, .net Framework Data Provider para *Oracle*.

-   **Si tiene un controlador ODBC para el destino**, seleccione .net Framework Data Provider para ODBC. A continuación, escriba la información específica del controlador. Controladores ODBC no aparezcan en la lista desplegable de destinos. .Net Framework Data Provider para ODBC actúa como un contenedor para el controlador ODBC. Para obtener más información, consulte [conectar a un origen de datos ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

-   **Es posible que haya más de un proveedor disponible para el destino.** Normalmente, puede seleccionar cualquier proveedor que funcione con su destino. Por ejemplo, para conectarse a Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede usar el proveedor de datos de .NET Framework para SQL Server o el controlador ODBC de SQL Server. (Otros proveedores también todavía están en la lista pero ya no se admiten). 

## <a name="my-destination-isnt-in-the-list"></a>El destino no está en la lista
-   **Puede que tenga que descargar el proveedor de datos** de Microsoft o de otros fabricantes. La lista de proveedores de datos disponibles en la **destino** lista incluye solo los proveedores instalados en el equipo. Para obtener información acerca de los destinos que puede utilizar, consulte [qué orígenes de datos y destinos ¿puedo usar?](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

-   **¿Tiene un controlador ODBC para el destino?** Controladores ODBC no aparezcan en la lista desplegable de destinos. Si tiene un controlador ODBC para el destino, seleccione .net Framework Data Provider para ODBC. A continuación, escriba la información específica del controlador. .Net Framework Data Provider para ODBC actúa como un contenedor para el controlador ODBC. Para obtener más información, consulte [conectar a un origen de datos ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

-   **proveedores de 64 bits y 32 bits.** Si se está ejecutando el Asistente de 64 bits, no podrá ver destinos para el que está instalado un proveedor de 32 bits y viceversa.

> [!NOTE]
> Para usar la versión de 64 bits de la importación de SQL Server y el Asistente para exportación, tendrá que instalar a SQL Server. SQL Server Data Tools (SSDT) y SQL Server Management Studio (SSMS) son aplicaciones de 32 bits y solo instalan archivos de 32 bits, incluida la versión de 32 bits del asistente.

## <a name="after-you-choose-a-destination"></a>Después de seleccionar un destino
Después de elegir un destino, el resto de la **elegir un destino** página tiene un número variable de opciones que dependen del proveedor de datos que elija.

Para conectarse a un destino de uso frecuente, consulte una de las páginas siguientes.
-   [Conectarse a SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar con Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a los archivos sin formato (archivos de texto)](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar con Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar con ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse al almacenamiento de blobs de Azure](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [Conectarse a PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)

Para obtener información sobre cómo conectarse a un destino que no aparece aquí, consulte [la referencia de las cadenas de conexión](https://www.connectionstrings.com/). Este sitio de terceros contiene las cadenas de conexión de ejemplo y obtener más información acerca de los proveedores de datos y la información de conexión que se necesiten.

## <a name="whats-next"></a>¿Qué debe hacer a continuación?  
 Después de proporcionar información sobre el destino de los datos y sobre cómo se conectará a estos, la página siguiente es **Especificar copia de tabla o consulta**. En esta página, especifique si quiere copiar una tabla completa o solo algunas filas. Para obtener más información, vea [Especificar copia de tabla o consulta](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md).  

## <a name="see-also"></a>Vea también
[Comenzar con este sencillo ejemplo del Asistente para importar y exportar](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)



