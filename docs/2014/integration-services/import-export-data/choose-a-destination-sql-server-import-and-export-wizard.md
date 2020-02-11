---
title: Elegir un destino (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.chooseadestination.f1
ms.assetid: 1898be15-3e69-42d3-8ecb-3733c9f6c8e3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 746aed7f49b0db51f46a32fdf040eb5b9e968dd2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62768030"
---
# <a name="choose-a-destination-sql-server-import-and-export-wizard"></a>Elegir un destino (Asistente para importación y exportación de SQL Server)
  Use la página **elegir un destino** para especificar el destino de los datos que desea copiar.  
  
 Para obtener más información acerca de este asistente, vea [Asistente para importación y exportación de SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para obtener información sobre las opciones para iniciar el asistente, así como los permisos necesarios para ejecutar el asistente correctamente, vea [ejecutar el Asistente para importación y exportación de SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 La finalidad del Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es copiar datos desde un origen a un destino. El asistente también puede crear una base de datos y tablas de destino. Sin embargo, si tiene que copiar diversas bases de datos o tablas, u otros tipos de objetos de bases de datos, debe utilizar el Asistente para copiar bases de datos. Para más información, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="static-options"></a>Opciones estáticas  
 **Destino**  
 Elija el proveedor de datos que coincide con el formato de almacenamiento de datos del destino. Es posible que haya más de un proveedor disponible para el origen de datos. Por ejemplo, con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, el proveedor de datos de .NET Framework para SQL Server o el proveedor de OLE DB de Microsoft para SQL Server.  
  
> [!NOTE]  
>  Para guardar datos en un destino ODBC, seleccione el proveedor de datos de .NET Framework para ODBC.  
  
 La propiedad **origen de datos** tiene un número variable de opciones, que cambian en función de los proveedores instalados en el equipo. Las siguientes tablas enumeran las opciones que se aplican a algunos destinos frecuentemente utilizados. Para otros proveedores, vea la documentación específica del proveedor.  
  
## <a name="dynamic-options"></a>Opciones dinámicas  
 En las secciones siguientes se muestran las opciones disponibles para varios orígenes de datos. Aquí no encontrará todos los destinos disponibles en la lista desplegable Destino.  
  
### <a name="destination--sql-server-native-client-or-microsoft-ole-db-provider-for-sql-server"></a>Destino = Proveedor OLE DB de Microsoft para SQL Server o SQL Server Native Client  
 **Nombre del servidor**  
 Escriba el nombre del servidor que recibirá los datos o elija un servidor de la lista.  
  
 **Usar autenticación de Windows**  
 Especifique si el paquete debe utilizar la autenticación de Microsoft Windows para iniciar una sesión en la base de datos. Para obtener una mayor seguridad, es recomendable utilizar la autenticación de Windows.  
  
 **Usar autenticación SQL Server**  
 Especifique si el paquete debe usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la autenticación de para iniciar sesión en la base de datos. Si usa la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe proporcionar un nombre de usuario y una contraseña.  
  
 **Nombre de usuario**  
 Especifique un nombre de usuario para la conexión de la base de datos cuando utilice la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Contraseña**  
 Proporcione la contraseña para la conexión de la base de datos cuando use la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Base de datos**  
 Seleccione en la lista de bases de datos de la instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o cree una nueva base de datos haciendo clic en **nueva**.  
  
 **Actualizar**  
 Para restaurar la lista de bases de datos disponibles, haga clic en **Actualizar**.  
  
 **Nuevo**  
 Cree una nueva base de datos de destino mediante el cuadro de diálogo **crear base de datos** .  
  
### <a name="destination--flat-file-destination"></a>Destino = Destino de archivo plano  
 **Nombre de archivo**  
 Especifique la ruta de acceso y el nombre de archivo correspondiente al archivo en el que almacenará los datos. O bien, haga clic en **Examinar** para buscar un archivo.  
  
 **Browse**  
 Busque un archivo mediante el cuadro de diálogo **Abrir**.  
  
 **Configuración regional**  
 Especifique el Id. de configuración regional (LCID) que define el criterio de ordenación de los caracteres y el formato de fecha y hora.  
  
 **Unicode**  
 Indique si se va a utilizar Unicode. Si utiliza Unicode, no es necesario que especifique una página de códigos.  
  
 **Página de códigos**  
 Especifique la página de códigos correspondiente al idioma que desea utilizar.  
  
 **Aplique**  
 Indique si se utiliza formato delimitado, de ancho fijo o derecho irregular.  
  
|Value|Descripción|  
|-----------|-----------------|  
|Delimitado|Las columnas se separan mediante un delimitador, que se especifica en la página **Columnas** .|  
|Ancho fijo|Las columnas tienen un ancho fijo.|  
|Derecho irregular|Los archivos de derecho irregular son archivos en los que todas las columnas tienen un ancho fijo, a excepción de la última, que está delimitada por el delimitador de filas.|  
  
 **Calificador de texto**  
 Escriba el calificador de texto que desea utilizar. Puede, por ejemplo, especificar que el texto de cada columna se encierre entre comillas.  
  
 **Nombres de columna de la primera fila de datos**  
 Indique si desea mostrar los nombres de las columnas de la primera fila de datos.  
  
### <a name="destination--microsoft-excel"></a>Destino = Microsoft Excel  
  
> [!NOTE]  
>  Seleccione **Microsoft Excel** solo si desea conectarse a un origen de datos que use Excel 2003 o una versión anterior. Para conectarse a un origen de datos que usa Excel 2007, seleccione **Microsoft Office 12,0 acceso motor de base de datos proveedor de OLE DB**, haga clic en **propiedades**y, a continuación, en la pestaña **todo** del cuadro de diálogo Propiedades de vínculo `Excel 12.0`de **datos** , para **propiedades extendidas**, escriba.  
  
 **Ruta de acceso del archivo Excel**  
 Especifique la ruta de acceso y el nombre de archivo del libro en el que se almacenarán los datos ( \\por ejemplo, C:\MyData.xls, \Sales\Database\Northwind.xls). O bien, haga clic en **Examinar** para buscar un libro.  
  
 **Browse**  
 Busque un libro de Excel mediante el cuadro de diálogo **abrir** .  
  
 **Versión de Excel**  
 Seleccione la versión de Excel que utiliza el libro de destino.  
  
> [!NOTE]  
>  Al exportar datos a un destino de [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] , el asistente utiliza el componente Destino de Excel de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obtener información sobre algunas consideraciones de uso y problemas conocidos, vea [Excel Destination](../data-flow/excel-destination.md).  
  
### <a name="destination--microsoft-access"></a>Destino = Microsoft Access  
  
> [!NOTE]  
>  Seleccione **Microsoft Access** solo si desea conectarse a una base de datos que use Access 2003 o una versión anterior. Para conectarse a una base de datos que usa Access 2007, seleccione **Microsoft Office 12,0 Access motor de base de datos proveedor de OLE DB**.  
  
 **Nombre de archivo**  
 Especifique la ruta de acceso y el nombre de archivo del archivo de base de datos en el que se almacenarán \\los datos (por ejemplo, C:\MyData.mdb, \Sales\Database\Northwind.mdb). O bien, haga clic en **Examinar** para buscar un archivo de base de datos.  
  
 **Browse**  
 Busque el archivo de base de datos mediante el cuadro de diálogo **abrir** .  
  
 **Nombre de usuario**  
 Especifique un nombre de usuario válido para la conexión de base de datos si hay un archivo de información de grupo de trabajo asociado a la base de datos.  
  
 **Contraseña**  
 Especifique una contraseña de usuario para la conexión de base de datos si hay un archivo de información de grupo de trabajo asociado a la base de datos. Sin embargo, si la base de datos está protegida con una misma contraseña para todos los usuarios, debe proporcionar este valor en el cuadro de diálogo **Propiedades del vínculo de datos** , al que se obtiene acceso desde el botón **Avanzadas** .  
  
 **Avanzadas**  
 Especifique las opciones avanzadas, como la contraseña de la base de datos o un archivo de información del grupo de trabajo no predeterminado, mediante el cuadro de diálogo **Propiedades de vínculo de datos**. Para obtener más información sobre las propiedades de proveedor OLE DB, busque en la sección sobre acceso a datos de [MSDN Library](https://go.microsoft.com/fwlink/?linkid=62553).  
  
  
