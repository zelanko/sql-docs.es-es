---
title: Elegir un destino (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.chooseadestination.f1
ms.assetid: 1898be15-3e69-42d3-8ecb-3733c9f6c8e3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d0b5484de65a497df68ca4d87f6a67ec3581728c
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923088"
---
# <a name="choose-a-destination-sql-server-import-and-export-wizard"></a>Elegir un destino (Asistente para importación y exportación de SQL Server)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


 Después de proporcionar información sobre el origen de datos y la manera de conectarse a él, el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra la página **Elegir un destino**. En esta página, debe proporcionar información sobre el destino de datos y la manera de conectarse a él.
  
Para obtener más información sobre los destinos de datos que puede usar, consulte [¿Qué orígenes de datos y destinos puedo usar?](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources). 

## <a name="screen-shot-of-the-destination-page"></a>Captura de pantalla de la página Destino
En la captura de pantalla siguiente, se muestra la primera parte de la página **Seleccionar un destino** del asistente. El resto de la página tiene un número variable de opciones que dependen del destino que elija aquí.

![Elegir un destino](../../integration-services/import-export-data/media/choose-destination.png)

## <a name="choose-a-destination"></a>Elegir un destino
 **Destino**  
 Para especificar el destino, seleccione un proveedor de datos que pueda importar los datos al destino.
 
-   **El proveedor de datos que necesita resulta obvio debido a su nombre**, ya que el nombre del proveedor suele contener el nombre del destino; por ejemplo, el destino de los *archivos planos*, Microsoft *Excel*, Microsoft *Access*, el proveedor de datos .Net Framework para *SqlServer* o el proveedor de datos .Net Framework para *Oracle*.

-   **Si tiene un controlador ODBC del destino**, seleccione el proveedor de datos .NET Framework para ODBC. A continuación, escriba la información específica del controlador. Los controladores ODBC no aparecen en la lista desplegable de los destinos. El proveedor de datos .Net Framework para ODBC actúa como un contenedor para el controlador ODBC. Para obtener más información, consulte [Conectarse a un origen de datos ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

-   **Es posible que haya más de un proveedor disponible para el destino.** Normalmente, puede seleccionar cualquier proveedor que funcione con su destino. Por ejemplo, para conectarse a Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede usar el proveedor de datos .NET Framework para SQL Server o el controlador ODBC para SQL Server. (Hay otros proveedores que aún aparecen en la lista, pero que ya no se admiten). 

## <a name="my-destination-isnt-in-the-list"></a>El destino no está en la lista
-   **Puede que tenga que descargar el proveedor de datos** desde Microsoft o desde un tercero. La lista de los proveedores de datos disponibles en la lista **Destino** incluye solamente los proveedores instalados en el equipo. Para obtener más información sobre los destinos que puede usar, consulte [What data sources and destinations can I use? (¿Qué orígenes y destinos de datos puedo usar?)](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources).

-   **¿Tiene un controlador ODBC para su destino?** Los controladores ODBC no aparecen en la lista desplegable de los destinos. Si tiene un controlador ODBC del destino, seleccione el proveedor de datos .NET Framework para ODBC. A continuación, escriba la información específica del controlador. El proveedor de datos .Net Framework para ODBC actúa como un contenedor para el controlador ODBC. Para obtener más información, consulte [Conectarse a un origen de datos ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

-   **Proveedores de 64 bits y 32 bits.** Si está ejecutando el asistente de 64 bits, no podrá ver los destinos que tengan instalado un proveedor de 32 bits y viceversa.

> [!NOTE]
> Para usar la versión de 64 bits del asistente para importación y exportación de SQL Server, tendrá que instalar SQL Server. SQL Server Data Tools (SSDT) y SQL Server Management Studio (SSMS) son aplicaciones de 32 bits y solo instalan archivos de 32 bits, incluida la versión de 32 bits del asistente.

## <a name="after-you-choose-a-destination"></a>Después de seleccionar un destino
Después de elegir un destino, el resto de la página **Elegir un destino** tiene un número variable de opciones que dependen del proveedor de datos que elija.

Para conectarse a un destino de uso frecuente, consulte una de las páginas siguientes.
-   [Conectarse a SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar con Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a archivos planos (archivos de texto)](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse con ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a Azure Blob Storage](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [Conectarse a PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)

Para obtener más información sobre cómo conectarse a un destino que no aparezca en esta lista, consulte [The Connection Strings Reference (Referencia de cadenas de conexión)](https://www.connectionstrings.com/). Este sitio de terceros contiene cadenas de conexión de ejemplo y más información acerca de los proveedores de datos y la conexión que estos necesitan.

## <a name="whats-next"></a>¿Qué sigue?  
 Después de proporcionar información sobre el destino de los datos y sobre cómo se conectará a estos, la página siguiente es **Especificar copia de tabla o consulta**. En esta página, especifique si quiere copiar una tabla completa o solo algunas filas. Para obtener más información, vea [Especificar copia de tabla o consulta](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md).  

## <a name="see-also"></a>Consulte también
[Comenzar con este sencillo ejemplo del Asistente para importar y exportar](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


