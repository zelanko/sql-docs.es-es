---
title: Conectarse a un origen de datos de Access (SQL Server importar y exportar) | Documentos de Microsoft
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b44c159a-c33d-4f3c-bdb8-9832f35317c8
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 71bb3914e31259bc95a1116c2db03708c0442e8c
ms.contentlocale: es-es
ms.lasthandoff: 08/28/2017

---
# <a name="connect-to-an-access-data-source-sql-server-import-and-export-wizard"></a>Conectarse a un origen de datos de Access (importación de SQL Server y Asistente para exportación)
Este tema muestra cómo conectarse a un **Microsoft Access** del origen de datos de la **elegir un origen de datos** o **elegir un destino** página de la importación de SQL Server y el Asistente para exportación.

En la siguiente captura de pantalla se muestra una conexión de ejemplo a una base de datos de Microsoft Access. En este ejemplo, no tiene que escribir un nombre de usuario y una contraseña, porque la base de datos de destino no usa un archivo de información de grupo de trabajo.

![Conectar con Access](../../integration-services/import-export-data/media/connect-to-access.jpg)

## <a name="options-to-specify"></a>Opciones para especificar

> [!NOTE]
> Las opciones de conexión para este proveedor de datos son los mismos si el acceso es el origen o el destino. Es decir, las opciones que ve son los mismos en ambos el **elegir un origen de datos** y **elegir un destino** páginas del asistente.

**Origen de datos**  
La lista de proveedores de datos puede contener varias entradas para Microsoft Access. Seleccione la última versión instalada, o la versión que corresponda a la versión de Access que creó el archivo de base de datos.

|Origen de datos|Versión de Office|
|-------|-------|
|Microsoft Access (Microsoft.ACE.OLEDB.16.0)|Office 2016|
|Microsoft Access (Microsoft.ACE.OLEDB.15.0)|Office 2013|
|Microsoft Access (motor de base de datos de Microsoft Access)|Office 2010 y Office 2007|
|Microsoft Access (motor de base de datos de Microsoft Jet)|Versiones de Office anteriores a Office 2007|

> [!IMPORTANT]
> Tendrá que descargar e instalar archivos adicionales para conectarse a bases de datos de Access. Vea [obtener los archivos que necesita para conectarse a Access](#officeDownloads) en esta página para obtener más información.

 **Nombre de archivo**  
Especifique la ruta de acceso y nombre de archivo para el archivo de acceso. Por ejemplo, **C:\\MyData.mdb** para un archivo en el equipo local, o  **\\ \\ventas\\base de datos\\Northwind.mdb** para un archivo en un recurso compartido de red. O bien, haga clic en **Examinar**. 

 >   [!NOTE] 
 > Si hace clic en **examinar** para buscar el archivo de acceso, el **abiertos** filtros del cuadro de diálogo para archivos con la versión más antigua. MDB formato y extensión de archivo de forma predeterminada. Sin embargo el proveedor de datos también puede abrir archivos con las versiones más recientes. Extensión de archivo de formato y ACCDB.
  
 **Examinar**  
 Busque el archivo de base de datos desde el cuadro de diálogo **Abrir**.  
  
 **Nombre de usuario.**  
Si un archivo de información de grupo de trabajo está asociado a la base de datos, proporcione un nombre de usuario válido.  
  
 **Contraseña**  
Si un archivo de información de grupo de trabajo está asociado a la base de datos, proporcione la contraseña del usuario aquí.
 
Si la base de datos está protegida con una contraseña para todos los usuarios, consulte [es el archivo de base de datos protegida por contraseña?](#database_password).
  
 **Avanzadas**  
Especificar opciones avanzadas, como la contraseña de la base de datos o un archivo de información de grupo de trabajo no predeterminado, en la **propiedades de vínculo de datos** cuadro de diálogo.  

## <a name="i-dont-see-access-in-the-list-of-data-sources"></a>No veo acceso en la lista de orígenes de datos
¿Si no ve el acceso en la lista de orígenes de datos, se está ejecutando al Asistente de 64 bits? Los proveedores para Excel y Access son normalmente de 32 bits y no están visibles en el Asistente de 64 bits. Ejecute al Asistente de 32 bits en su lugar.

> [!NOTE]
> Para usar la versión de 64 bits de la importación de SQL Server y el Asistente para exportación, tendrá que instalar a SQL Server. SQL Server Data Tools (SSDT) y SQL Server Management Studio (SSMS) son aplicaciones de 32 bits y solo instalan archivos de 32 bits, incluida la versión de 32 bits del asistente.

## <a name="officeDownloads"></a>Obtener los archivos que necesita para conectarse a Access  
Tendrá que descargar los componentes de conectividad para orígenes de datos de Microsoft Office, como Access y Excel, si no están instaladas. Descargar la versión más reciente de los componentes de conectividad para los archivos de Access y Excel aquí: [redistribuible de 2016 de motor de base de datos Microsoft acceso](https://www.microsoft.com/download/details.aspx?id=54920).
  
La versión más reciente de los componentes puede abrir archivos creados con versiones anteriores de Access.

Si el equipo tiene una versión de 32 bits de Office, tendrá que instalar la versión de 32 bits de los componentes, y también tiene que asegurarse de que se ejecuta el paquete en modo de 32 bits.

Si tiene una suscripción de Office 365, asegúrese de que descargue el redistribuible de 2016 de motor de base de datos de acceso y no el Runtime de 2016 de Microsoft Access. Al ejecutar el programa de instalación, verá un mensaje de error que no se puede instalar la descarga en paralelo con componentes de hacer clic para ejecutar Office. Para pasar por alto este mensaje de error, ejecute la instalación en modo silencioso, abra una ventana del símbolo del sistema y ejecuta el. Un archivo ejecutable que se descargó con el `/quiet` cambiar. Por ejemplo:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="database_password"></a>¿Es el archivo de base de datos protegida con contraseña?
En algunos casos, una base de datos de Access está protegida con contraseña, pero no está utilizando un archivo de información de grupo de trabajo. Todos los usuarios deben proporcionar la misma contraseña, pero no tienen que especificar un nombre de usuario. Para proporcionar una contraseña de base de datos, haga lo siguiente.

1.  En el **elegir un origen de datos** o **elegir un destino** página, haga clic en el **avanzadas** para abrir el **propiedades de vínculo de datos** cuadro de diálogo.  
2.  En el **propiedades de vínculo de datos** cuadro de diálogo, seleccione la **todos los** ficha.  
3.  En la lista de propiedades y valores, seleccione **Jet OLEDB: Database Password**.   
    
    ![Especifique la contraseña de acceso, pantalla 1](../../integration-services/import-export-data/media/specify-access-password-screen-1.jpg) 
4.  Haga clic en **Editar valor** para abrir el **Modificar valor de propiedad** cuadro de diálogo.  
    
    ![Especifique la contraseña de acceso, pantalla 2](../../integration-services/import-export-data/media/specify-access-password-screen-2.jpg)
5.  En el **Modificar valor de propiedad** diálogo cuadro, escriba la contraseña de la base de datos.
6.  Haga clic en **Aceptar** en cada cuadro de diálogo para volver a la **elegir un origen de datos** o **elegir un destino** página del asistente y continuar.

## <a name="keep-your-autonumber-values-when-you-export-from-access"></a>Mantener los valores de autonumeración al exportar desde Access
Para permitir que los valores de identidad existentes en los datos de origen que va a insertar en una columna de identidad en la tabla de destino, elija la **Habilitar inserción de identidad** opción en el **asignaciones de columnas** cuadro de diálogo. De forma predeterminada, la columna de identidad de destino normalmente no le permite insertar valores existentes. Para mostrar la **asignaciones de columnas** cuadro de diálogo, seleccione **editar asignaciones** cuando llegue a la **seleccionar tablas de origen y vistas** página del asistente. Para buscar en estas páginas, vea [seleccionar tablas de origen y vistas](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) y [asignaciones de columnas](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).

Si las claves principales existentes están en una columna de identidad, una columna autonumérica o su equivalente, normalmente es necesario seleccionar esta opción para mantener los valores de clave principales existentes. De lo contrario, la columna de identidad de destino normalmente asigna nuevos valores.

## <a name="see-also"></a>Vea también
[Elija un origen de datos](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Elegir un destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


