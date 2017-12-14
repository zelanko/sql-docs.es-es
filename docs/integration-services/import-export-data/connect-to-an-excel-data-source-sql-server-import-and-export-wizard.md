---
title: "Conectarse a un origen de datos de Excel (Asistente para importación y exportación de SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 43fbaca0-36d8-4583-9056-af7010209b87
caps.latest.revision: "12"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2aeb225037970b8a77169db18c204ecf6d4c19d6
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="connect-to-an-excel-data-source-sql-server-import-and-export-wizard"></a>Conectarse a un origen de datos de Excel (Asistente para importación y exportación de SQL Server)
En este tema se muestra cómo conectarse a un origen de datos de **Microsoft Excel** desde la página **Elegir un origen de datos** o **Elegir un destino** del Asistente para importación y exportación de SQL Server.

En la siguiente captura de pantalla se muestra una conexión de ejemplo a un libro de Microsoft Excel.

![Conexión de Excel](../../integration-services/import-export-data/media/excel-connection.png) 

## <a name="options-to-specify"></a>Opciones para especificar

> [!NOTE]
> Las opciones de conexión de este proveedor de datos son las mismas independientemente de si Excel es el origen o el destino. Es decir, las opciones que ve son las mismas en ambas páginas **Elegir un origen de datos** y **Elegir un destino** del asistente.

**Ruta de acceso del archivo Excel**  
 Especificar la ruta de acceso y el nombre del archivo de Excel. Por ejemplo:
-   Para un archivo en el equipo local, **C:\\MyData.xlsx**.
-   Para un archivo en un recurso compartido de red, **\\\\Sales\\Database\\Northwind.xlsx**.

O bien, haga clic en **Examinar**.  
  
 **Examinar**  
 Busque la hoja de cálculo desde el cuadro de diálogo **Abrir**.  

> [!NOTE]
> El asistente no puede abrir un archivo de Excel protegido mediante contraseña.

 **Versión de Excel**  
Seleccione la versión de Excel que usa el libro de origen.

> [!IMPORTANT]
> Es posible que tenga que descargar e instalar archivos adicionales para conectarse a archivos de Excel. Para obtener más información, vea [Obtener los archivos que necesita para conectarse a Excel](#officeDownloads) en esta página.

**La primera fila tiene nombres de columna**  
Indique si la primera fila de los datos contiene nombres de columna.
-   Si los datos no contienen nombres de columna, pero se habilita esta opción, el asistente trata la primera fila de los datos de origen como los nombres de columna.
-   Si los datos contienen nombres de columna, pero se deshabilita esta opción, el asistente trata la fila de nombres de columna como la primera fila de datos.

Si especifica que los datos no tienen nombres de columna, el asistente usa F1, F2, etc., como encabezados de columna.

## <a name="i-dont-see-excel-in-the-list-of-data-sources"></a>No veo Excel en la lista de orígenes de datos
Si no ve Excel en la lista de orígenes de datos, ¿comprobó que está ejecutando el asistente de 64 bits? Los proveedores para Excel y Access son normalmente de 32 bits y no son visibles en el asistente de 64 bits. Ejecute al asistente de 32 bits en su lugar.

> [!NOTE]
> Para usar la versión de 64 bits del Asistente para importación y exportación de SQL Server, tendrá que instalar SQL Server. SQL Server Data Tools (SSDT) y SQL Server Management Studio (SSMS) son aplicaciones de 32 bits y solo instalan archivos de 32 bits, incluida la versión de 32 bits del asistente.

## <a name="officeDownloads"></a>Obtener los archivos que necesita para conectarse a Excel  
Es posible que tenga que descargar los componentes de conectividad para orígenes de datos de Microsoft Office, incluidos Excel y Access, si aún no están instalados. Descargue la versión más reciente de los componentes de conectividad para los archivos de Access y Excel aquí: [Microsoft Access Database Engine 2016 Redistributable](https://www.microsoft.com/download/details.aspx?id=54920).
  
La versión más reciente de los componentes puede abrir los archivos creados con versiones anteriores de los programas de Excel.

Si el equipo tiene una versión de Office de 32 bits, tendrá que instalar la versión de 32 bits de los componentes, y también debe asegurarse de que ejecuta el paquete en el modo de 32 bits.

Si tiene una suscripción de Office 365, asegúrese de descargar Access Database Engine 2016 Redistributable y no Microsoft Access 2016 Runtime. Al ejecutar el instalador, verá un mensaje de error que indica que no se puede instalar la descarga en paralelo con componentes para hacer clic y ejecutar de Office. Para omitir este mensaje de error, ejecute la instalación en modo silencioso abriendo una ventana del símbolo del sistema y ejecutando el archivo .EXE que descargó con el modificador `/quiet`. Por ejemplo:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="see-also"></a>Vea también
[Elegir un origen de datos](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Elegir un destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

