---
title: Elegir un origen de datos (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.chooseadatasource.f1
ms.assetid: ebf28a62-dfc1-4b39-9db5-df1919e5fccb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b6e399cf6c145f36febd9b32ae7a84c54741bb43
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58381222"
---
# <a name="choose-a-data-source-sql-server-import-and-export-wizard"></a>Elegir un origen de datos (Asistente para importación y exportación de SQL Server)
  Use la **elegir un origen de datos** página para especificar el origen de los datos que se van a copiar.  
  
 Para obtener más información acerca de este asistente, vea [Asistente para importación y exportación de SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para obtener información sobre las opciones para iniciar el asistente y sobre los permisos necesarios para ejecutar el asistente correctamente, consulte [ejecutar la importación de SQL Server y el Asistente para exportación de](start-the-sql-server-import-and-export-wizard.md).  
  
 La finalidad del Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es copiar datos desde un origen a un destino. El asistente también puede crear una base de datos y tablas de destino. Sin embargo, si tiene que copiar diversas bases de datos o tablas, u otros tipos de objetos de bases de datos, debe utilizar el Asistente para copiar bases de datos. Para más información, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opciones  
 **Origen de datos**  
 Elija el proveedor de datos que se corresponda con el formato de almacenamiento de datos del origen. Es posible que haya más de un proveedor disponible para el origen de datos. Por ejemplo, con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, el proveedor de datos de .NET Framework para SQL Server o el proveedor Microsoft OLE DB para SQL Server.  
  
 La propiedad **Origen de datos** tiene un número variable de opciones que depende de los proveedores instalados en el equipo. En las tablas siguientes se indican las opciones para algunos de los destinos utilizados con mayor frecuencia. Para otros proveedores, vea la documentación específica del proveedor.  
  
## <a name="dynamic-options"></a>Opciones dinámicas  
 En las secciones siguientes se muestran las opciones disponibles para varios orígenes de datos. Aquí no se indican todos los orígenes de datos disponibles en el menú desplegable Origen de datos.  
  
### <a name="data-source--sql-server-native-client-and-microsoft-ole-db-provider-for-sql-server"></a>Origen de datos = Proveedor Microsoft OLE DB para SQL Server y SQL Server Native Client  
 **Nombre del servidor**  
 Escriba el nombre del servidor que contiene los datos o elija un servidor de la lista.  
  
 **Utilizar autenticación de Windows**  
 Especifique si el paquete debe utilizar la autenticación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] para iniciar sesión en la base de datos. Para obtener una mayor seguridad, es recomendable utilizar la autenticación de Windows.  
  
 **Utilizar autenticación de SQL Server**  
 Especifique si el paquete debe utilizar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación para iniciar sesión en la base de datos. Si usa la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe proporcionar un nombre de usuario y una contraseña.  
  
 **Nombre de usuario.**  
 Especifique un nombre de usuario para la conexión de la base de datos cuando utilice la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Contraseña**  
 Proporcione la contraseña para la conexión de la base de datos cuando use la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Base de datos**  
 Seleccione una base de datos de la lista de bases de datos de la instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Actualizar**  
 Para restaurar la lista de bases de datos disponibles, haga clic en **Actualizar**.  
  
### <a name="data-source--net-framework-data-provider-for-sql-server"></a>Origen de datos = Proveedor de datos de .NET Framework para servidor SQL Server  
 Esta página presenta una lista alfabética de opciones para el proveedor de datos de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Las opciones más importantes se indican en la tabla siguiente.  
  
 **Origen de datos**  
 Escriba el nombre del servidor que contiene los datos o elija un servidor de la lista.  
  
 **Catálogo original**  
 Escriba el nombre de la base de datos de origen.  
  
 **Seguridad integrada**  
 Especifique `True` para establecer la conexión mediante la autenticación integrada de Windows (opción recomendada) o `False` para conectarse utilizando la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si especifica `False`, debe especificar un Id. de usuario y una contraseña. El valor predeterminado es `False`.  
  
 **Id. de usuario**  
 Especifique un nombre de usuario para la conexión de la base de datos cuando utilice la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Contraseña**  
 Proporcione la contraseña para la conexión de la base de datos cuando use la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Las opciones adicionales que aparecen al seleccionar este proveedor no son necesarias para establecer conexión correctamente con la base de datos de origen de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener una descripción de estas opciones adicionales, vea la documentación del Proveedor de datos de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el kit de desarrollo de software de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] .  
  
### <a name="data-source--microsoft-excel"></a>Origen de datos = Microsoft Excel  
  
> [!NOTE]  
>  Seleccione **Microsoft Excel** únicamente si desea conectarse a un origen de datos que utiliza Excel 2003 o versiones anteriores. Para conectarse a un origen de datos que usa Excel 2007, seleccione **Microsoft Office 12.0 Access Database Engine OLE DB Provider**, haga clic en **propiedades**y, a continuación, en el **todas** pestaña de la **Propiedades de vínculo de datos** diálogo cuadro, escriba `Excel 12.0` como el valor de **propiedades extendidas**.  
  
 **Ruta de acceso del archivo Excel**  
 Especifique la ruta de acceso y el nombre de archivo correspondientes a la hoja de cálculo desde la que se importarán los datos. Por ejemplo, **C:\MyData.xls, \\\Sales\Database\Northwind.xls**. O bien, haga clic en **Examinar**.  
  
 **Examinar**  
 Busque la hoja de cálculo desde el cuadro de diálogo **Abrir**.  
  
 **Versión de Excel**  
 Seleccione la versión de Excel en la que se ha almacenado el origen de datos.  
  
> [!NOTE]  
>  Al importar datos desde un origen de [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)], el asistente utiliza el componente de origen de Excel de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Para obtener más información sobre consideraciones de uso y problemas conocidos, vea [Excel Source](../data-flow/excel-source.md).  
  
### <a name="data-source--microsoft-access"></a>Origen de datos = Microsoft Access  
  
> [!NOTE]  
>  Seleccione **Microsoft Access** únicamente si desea conectarse a una base de datos que use Access 2003 o versiones anteriores. Para conectarse a una base de datos que use Access 2007, seleccione **Microsoft Office 12.0 Access Database Engine OLE DB Provider** en su lugar.  
  
 **Nombre de archivo**  
 Especifique la ruta de acceso y el nombre de archivo correspondientes al archivo de base de datos desde el que se importarán los datos. Por ejemplo, **C:\MyData.mdb, \\\Sales\Database\Northwind.mdb**. O bien, haga clic en **Examinar**.  
  
 **Examinar**  
 Busque el archivo de base de datos desde el cuadro de diálogo **Abrir**.  
  
 **Nombre de usuario.**  
 Especifique un nombre de usuario válido para la conexión de base de datos si hay un archivo de información de grupo de trabajo asociado a la base de datos.  
  
 **Contraseña**  
 Especifique una contraseña de usuario para la conexión de base de datos si hay un archivo de información de grupo de trabajo asociado a la base de datos. Si la base de datos está protegida con una única contraseña para todos los usuarios, debe proporcionar este valor en el cuadro de diálogo **Propiedades de vínculo de datos** , al que puede obtener acceso haciendo clic en **Avanzadas**.  
  
 **Avanzadas**  
 Puede desear especificar opciones avanzadas, como la contraseña de la base de datos o un archivo de información de grupo de trabajo no predeterminado, mediante la **propiedades de vínculo de datos** cuadro de diálogo. Para obtener más información acerca de las propiedades del proveedor OLE DB, busque en la sección de acceso a datos de la [biblioteca MSDN](https://go.microsoft.com/fwlink/?linkid=62553).  
  
### <a name="data-source--flat-file-source"></a>Origen de datos = Origen de archivo plano  
 Vea los temas siguientes para obtener información acerca de las opciones para un origen de datos de archivo plano.  
  
 [Editor del administrador de conexiones de archivos planos &#40;página General&#41;](../general-page-of-integration-services-designers-options.md)  
  
 [Editor del administrador de conexiones de archivos planos &#40;página Columnas&#41;](../flat-file-connection-manager-editor-columns-page.md)  
  
 [Editor del administrador de conexiones de archivos planos &#40;página Avanzadas&#41;](../flat-file-connection-manager-editor-advanced-page.md)  
  
 [Editor del administrador de conexiones de archivos planos &#40;página Vista previa&#41;](../flat-file-connection-manager-editor-preview-page.md)  
  
  
