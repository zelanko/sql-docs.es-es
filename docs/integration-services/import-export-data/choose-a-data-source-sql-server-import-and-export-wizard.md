---
title: Elegir un origen de datos (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.chooseadatasource.f1
ms.assetid: ebf28a62-dfc1-4b39-9db5-df1919e5fccb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b707b2b31c15c565353f0ff581ca1f4d7308a25b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "71951941"
---
# <a name="choose-a-data-source-sql-server-import-and-export-wizard"></a>Elegir un origen de datos (Asistente para importación y exportación de SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Después de la página de bienvenida, el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra **Elegir un origen de datos**. En esta página, debe proporcionar información sobre el origen de los datos y la manera de conectarse a él.
  
Para más información sobre los orígenes de datos que puede usar, vea [¿Qué orígenes de datos y destinos puedo usar?](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

> [!NOTE]
> El Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa SQL Server Integration Services (SSIS). Por lo tanto, las mismas limitaciones que se aplican a SSIS, también se aplican al asistente.  Por ejemplo, las columnas ErrorCode y ErrorColumn, que se agregan de forma predeterminada, como se describe en [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).

## <a name="screen-shot-of-the-choose-a-data-source-page"></a>Captura de pantalla de la página Seleccionar un origen de datos 
En la imagen siguiente, se muestra la primera parte de la página **Seleccionar un origen de datos** del asistente. El resto de la página tiene un número variable de opciones que dependen del origen de datos que elija aquí.

![Elegir origen](../../integration-services/import-export-data/media/choose-source.png)

## <a name="choose-a-data-source"></a>Elegir un origen de datos
 **Origen de datos**  
Especifique el origen de datos seleccionando un proveedor de datos que pueda conectarse al origen.

-   **El proveedor de datos que necesita resulta obvio debido a su nombre**, ya que el nombre del proveedor suele contener el nombre del origen de datos; por ejemplo, el origen de los *archivos planos*, Microsoft *Excel*, Microsoft *Access*, el proveedor de datos .Net Framework para *SqlServer* o el proveedor de datos .Net Framework para *Oracle*.

-   **Si tiene un controlador ODBC para su origen de datos**, seleccione el proveedor de datos .NET Framework para ODBC. A continuación, escriba la información específica del controlador. Los controladores ODBC no aparecen en la lista desplegable de los orígenes de datos. El proveedor de datos .Net Framework para ODBC actúa como un contenedor para el controlador ODBC. Para obtener más información, consulte [Conectarse a un origen de datos ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

-   **Es posible que haya más de un proveedor disponible para el origen de datos.** Normalmente, puede seleccionar cualquier proveedor que funcione con su origen. Por ejemplo, para conectarse a Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede usar el proveedor de datos .NET Framework para SQL Server o el controlador ODBC para SQL Server. (Hay otros proveedores que aún aparecen en la lista, pero que ya no se admiten). 

## <a name="my-data-source-isnt-in-the-list"></a>Mi origen de datos no está en la lista.
-   **Puede que tenga que descargar el proveedor de datos** desde Microsoft o desde un tercero. La lista de los proveedores de datos disponibles que están en la lista **Origen de datos** incluye solamente los proveedores instalados en el equipo. Para más información sobre los orígenes de datos que puede usar, vea [¿Qué orígenes de datos y destinos puedo usar?](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

-   **¿Tiene un controlador ODBC para el origen de datos?** Los controladores ODBC no aparecen en la lista desplegable de los orígenes de datos. Si tiene un controlador ODBC para su origen de datos, seleccione el proveedor de datos .NET Framework para ODBC. A continuación, escriba la información específica del controlador. El proveedor de datos .Net Framework para ODBC actúa como un contenedor para el controlador ODBC. Para obtener más información, consulte [Conectarse a un origen de datos ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

-   **Proveedores de 64 bits y 32 bits.** Si está ejecutando el asistente de 64 bits, no podrá ver los orígenes de datos que tengan instalado únicamente un proveedor de 32 bits y viceversa.

> [!NOTE]
> Para usar la versión de 64 bits del asistente para importación y exportación de SQL Server, tendrá que instalar SQL Server. SQL Server Data Tools (SSDT) y SQL Server Management Studio (SSMS) son aplicaciones de 32 bits y solo instalan archivos de 32 bits, incluida la versión de 32 bits del asistente.

## <a name="after-you-choose-a-data-source"></a>Después de seleccionar un origen de datos
Después de elegir un origen de datos, el resto de la página **Elegir un origen de datos** tiene un número variable de opciones que dependen del proveedor de datos que elija.

Para conectarse a un origen de datos de uso frecuente, consulte una de las páginas siguientes.
-   [Conectarse a SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar con Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a archivos planos (archivos de texto)](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse con ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a Azure Blob Storage](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [Conectarse a PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)

Para obtener más información sobre cómo conectarse a un origen de datos que no aparezca en esta lista, consulte [The Connection Strings Reference (Referencia de cadenas de conexión)](https://www.connectionstrings.com/). Este sitio de terceros contiene cadenas de conexión de ejemplo y más información acerca de los proveedores de datos y la conexión que estos necesitan.

## <a name="whats-next"></a>¿Qué sigue?
 Después de proporcionar información sobre el origen de datos y la manera de conectarse a él, la página siguiente es **Elegir un destino**. En esta página, debe proporcionar información sobre el destino de datos y la manera de conectarse a él. Para más información, vea [Elegir un destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md).

## <a name="see-also"></a>Consulte también
[Comenzar con este sencillo ejemplo del Asistente para importar y exportar](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

[!INCLUDE[get-help-options](../../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../../includes/paragraph-content/contribute-to-content.md)]
