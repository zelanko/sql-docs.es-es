---
title: Elija un origen de datos (SQL Server importar y exportar) | Documentos de Microsoft
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
- sql13.dts.impexpwizard.chooseadatasource.f1
ms.assetid: ebf28a62-dfc1-4b39-9db5-df1919e5fccb
caps.latest.revision: 124
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 80d35cb294fd900611c73ca37bba2a66baef0767
ms.contentlocale: es-es
ms.lasthandoff: 08/28/2017

---
# <a name="choose-a-data-source-sql-server-import-and-export-wizard"></a>Elegir un origen de datos (Asistente para importación y exportación de SQL Server)
  Después de la página de bienvenida, el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra **Elegir un origen de datos**. En esta página, debe proporcionar información sobre el origen de datos y la manera de conectarse a él.
  
Para más información sobre los orígenes de datos que puede usar, vea [¿Qué orígenes de datos y destinos puedo usar?](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

## <a name="screen-shot-of-the-choose-a-data-source-page"></a>Captura de pantalla de la página Seleccionar un origen de datos 
En la captura de pantalla siguiente, se muestra la primera parte de la página **Seleccionar un origen de datos** del asistente. El resto de la página tiene un número variable de opciones que dependen del origen de datos que elija aquí.

![Elegir origen](../../integration-services/import-export-data/media/choose-source.png)

## <a name="choose-a-data-source"></a>Elegir un origen de datos
 **Origen de datos**  
Especifique el origen de datos seleccionando un proveedor de datos que pueda conectarse al origen.

-   **El proveedor de datos que necesita es normalmente obvio con su nombre**, ya que el nombre del proveedor suele contener el nombre del origen de datos: por ejemplo, *archivos planos* origen, Microsoft *Excel*, Microsoft *acceso*, .net Framework Data Provider para *SqlServer*, .net Framework Data Provider para *Oracle*.

-   **Si tiene un controlador ODBC para el origen de datos**, seleccione .net Framework Data Provider para ODBC. A continuación, escriba la información específica del controlador. Controladores ODBC no aparezcan en la lista desplegable de orígenes de datos. .Net Framework Data Provider para ODBC actúa como un contenedor para el controlador ODBC. Para obtener más información, consulte [conectar a un origen de datos ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

-   **Es posible que haya más de un proveedor disponible para el origen de datos.** Normalmente, puede seleccionar cualquier proveedor que funcione con su origen. Por ejemplo, para conectarse a Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede usar el proveedor de datos de .NET Framework para SQL Server o el controlador ODBC de SQL Server. (Otros proveedores también todavía están en la lista pero ya no se admiten). 

## <a name="my-data-source-isnt-in-the-list"></a>Un origen de datos no está en la lista
-   **Puede que tenga que descargar el proveedor de datos** de Microsoft o de otros fabricantes. La lista de proveedores de datos disponibles en la **origen de datos** lista incluye solo los proveedores instalados en el equipo. Para más información sobre los orígenes de datos que puede usar, vea [¿Qué orígenes de datos y destinos puedo usar?](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

-   **¿Tiene un controlador ODBC para el origen de datos?** Controladores ODBC no aparezcan en la lista desplegable de orígenes de datos. Si tiene un controlador ODBC para el origen de datos, seleccione .net Framework Data Provider para ODBC. A continuación, escriba la información específica del controlador. .Net Framework Data Provider para ODBC actúa como un contenedor para el controlador ODBC. Para obtener más información, consulte [conectar a un origen de datos ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

-   **proveedores de 64 bits y 32 bits.** Si se está ejecutando el Asistente de 64 bits, no podrá ver los orígenes de datos para el que está instalado un proveedor de 32 bits y viceversa.

> [!NOTE]
> Para usar la versión de 64 bits de la importación de SQL Server y el Asistente para exportación, tendrá que instalar a SQL Server. SQL Server Data Tools (SSDT) y SQL Server Management Studio (SSMS) son aplicaciones de 32 bits y solo instalan archivos de 32 bits, incluida la versión de 32 bits del asistente.

## <a name="after-you-choose-a-data-source"></a>Después de seleccionar un origen de datos
Después de elegir un origen de datos, el resto de la **elegir un origen de datos** página tiene un número variable de opciones que dependen del proveedor de datos que elija.

Para conectarse a un origen de datos de uso frecuente, consulte una de las páginas siguientes.
-   [Conectarse a SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar con Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a los archivos sin formato (archivos de texto)](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar con Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar con ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse al almacenamiento de blobs de Azure](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [Conectarse a PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)

Para obtener información sobre cómo conectarse a un origen de datos que no aparece aquí, consulte [la referencia de las cadenas de conexión](https://www.connectionstrings.com/). Este sitio de terceros contiene las cadenas de conexión de ejemplo y obtener más información acerca de los proveedores de datos y la información de conexión que se necesiten.

## <a name="whats-next"></a>¿Qué debe hacer a continuación?  
 Después de proporcionar información sobre el origen de datos y la manera de conectarse a él, la página siguiente es **Elegir un destino**. En esta página, debe proporcionar información sobre el destino de datos y la manera de conectarse a él. Para más información, vea [Elegir un destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md).
 
## <a name="see-also"></a>Vea también
[Comenzar con este sencillo ejemplo del Asistente para importar y exportar](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)



