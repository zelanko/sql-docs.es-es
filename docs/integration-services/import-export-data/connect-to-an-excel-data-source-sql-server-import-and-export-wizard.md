---
title: Conectarse a un origen de datos de Excel (SQL Server importar y exportar) | Documentos de Microsoft
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 43fbaca0-36d8-4583-9056-af7010209b87
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: b4411fdd2337d93f15b149febf845fb7b0762c40
ms.contentlocale: es-es
ms.lasthandoff: 08/28/2017

---
# <a name="connect-to-an-excel-data-source-sql-server-import-and-export-wizard"></a>Conectarse a un origen de datos de Excel (importación de SQL Server y Asistente para exportación)
Este tema muestra cómo conectarse a un **Microsoft Excel** del origen de datos de la **elegir un origen de datos** o **elegir un destino** página de la importación de SQL Server y el Asistente para exportación.

En la siguiente captura de pantalla se muestra una conexión de ejemplo a un libro de Microsoft Excel.

![Conexión de Excel](../../integration-services/import-export-data/media/excel-connection.png) 

## <a name="options-to-specify"></a>Opciones para especificar

> [!NOTE]
> Las opciones de conexión para este proveedor de datos son los mismos si Excel es el origen o el destino. Es decir, las opciones que ve son los mismos en ambos el **elegir un origen de datos** y **elegir un destino** páginas del asistente.

**Ruta de acceso del archivo Excel**  
 Especifique la ruta de acceso y el nombre del archivo de Excel. Por ejemplo:
-   Para un archivo en el equipo local, **C:\\MyData.xlsx**.
-   Un archivo en un recurso compartido de red,  **\\ \\ventas\\base de datos\\Northwind.xlsx**.

O bien, haga clic en **Examinar**.  
  
 **Examinar**  
 Busque la hoja de cálculo desde el cuadro de diálogo **Abrir**.  

> [!NOTE]
> El asistente no puede abrir un archivo de Excel protegido mediante contraseña.

 **Versión de Excel**  
Seleccione la versión de Excel que usa el libro de origen.

> [!IMPORTANT]
> Tendrá que descargar e instalar archivos adicionales para conectarse a los archivos de Excel. Vea [obtener los archivos que necesita para conectarse a Excel](#officeDownloads) en esta página para obtener más información.

**La primera fila tiene nombres de columna**  
Indicar si la primera fila de datos contiene nombres de columna.
-   Si los datos no contienen nombres de columna, pero se habilita esta opción, el Asistente trata la primera fila de datos de origen como los nombres de columna.
-   Si los datos contienen nombres de columna, pero se deshabilita esta opción, el Asistente trata la fila de nombres de columna como la primera fila de datos.

Si especifica que los datos no tienen nombres de columna, el asistente usa F1, F2 y así sucesivamente, como encabezados de columna.

## <a name="i-dont-see-excel-in-the-list-of-data-sources"></a>No veo Excel en la lista de orígenes de datos
¿Si no ve Excel en la lista de orígenes de datos, se está ejecutando al Asistente de 64 bits? Los proveedores para Excel y Access son normalmente de 32 bits y no están visibles en el Asistente de 64 bits. Ejecute al Asistente de 32 bits en su lugar.

> [!NOTE]
> Para usar la versión de 64 bits de la importación de SQL Server y el Asistente para exportación, tendrá que instalar a SQL Server. SQL Server Data Tools (SSDT) y SQL Server Management Studio (SSMS) son aplicaciones de 32 bits y solo instalan archivos de 32 bits, incluida la versión de 32 bits del asistente.

## <a name="officeDownloads"></a>Obtener los archivos que necesita para conectarse a Excel  
Tendrá que descargar los componentes de conectividad para orígenes de datos de Microsoft Office, como Excel y Access, si no están instaladas. Descargar la versión más reciente de los componentes de conectividad para los archivos de Excel y Access aquí: [redistribuible de 2016 de motor de base de datos Microsoft acceso](https://www.microsoft.com/download/details.aspx?id=54920).
  
La versión más reciente de los componentes puede abrir archivos creados con versiones anteriores de Excel.

Si el equipo tiene una versión de 32 bits de Office, tendrá que instalar la versión de 32 bits de los componentes, y también tiene que asegurarse de que se ejecuta el paquete en modo de 32 bits.

Si tiene una suscripción de Office 365, asegúrese de que descargue el redistribuible de 2016 de motor de base de datos de acceso y no el Runtime de 2016 de Microsoft Access. Al ejecutar el programa de instalación, verá un mensaje de error que no se puede instalar la descarga en paralelo con componentes de hacer clic para ejecutar Office. Para pasar por alto este mensaje de error, ejecute la instalación en modo silencioso, abra una ventana del símbolo del sistema y ejecuta el. Un archivo ejecutable que se descargó con el `/quiet` cambiar. Por ejemplo:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="see-also"></a>Vea también
[Elija un origen de datos](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Elegir un destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


