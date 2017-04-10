---
title: "Conectarse a un libro de Excel | Microsoft Docs"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Excel [Integration Services]"
ms.assetid: d9746318-3669-4ce2-bbb0-4a1bd471c9dd
caps.latest.revision: 22
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 22
---
# Conectarse a un libro de Excel
  Para conectar un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a un libro de Microsoft Office Excel es necesario disponer de un administrador de conexiones.  
  
 Puede crear estos administradores de conexión desde el área de administradores de conexión en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] o desde el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Proveedores y controladores de archivo de Microsoft Excel y Access**  
  
 Tendrá que descargar los proveedores y controladores OLE DB para los archivos de Microsoft Office si no están instalados. Las versiones posteriores del proveedor pueden abrir archivos creados con versiones anteriores de Excel.  
  
 Si el equipo tiene una versión de Office de 32 bits, tendrá que instalar la versión de 32 bits de los controladores, y también debe asegurarse de que ejecuta el asistente o el paquete de Integration Services que se crea en el modo de 32 bits.  
  
|Versión de Microsoft Office|Descargar|  
|------------------------------|--------------|  
|2007|[Controlador de 2007 Office System: componentes de conectividad de datos](https://www.microsoft.com/en-us/download/details.aspx?id=23734)|  
|2010|[Microsoft Access 2010 Runtime](https://www.microsoft.com/en-us/download/details.aspx?id=10910)|  
|2013|[Microsoft Access 2013 Runtime](http://www.microsoft.com/en-us/download/details.aspx?id=39358)|  
  
### Para crear un administrador de conexiones con Excel desde el área de administradores de conexión  
  
1.  Abra el paquete en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Haga clic con el botón derecho en cualquier punto del área **Administradores de conexión** y luego seleccione **Nueva conexión**.  
  
3.  En el cuadro de diálogo **Agregar administrador de conexiones SSIS** , seleccione **Excel**y, a continuación, configure el administrador de conexiones.  
  
     Para obtener información sobre las opciones de configuración disponibles para este administrador de conexiones, vea [Excel Connection Manager Editor](../../integration-services/connection-manager/excel-connection-manager-editor.md).  
  
### Para crear una conexión con Excel desde el Asistente para importación y exportación de SQL Server  
  
1.  Inicie la versión de 32 bits del Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  En la página **Elegir un origen de datos** , seleccione **Microsoft Excel**en **Origen de datos**y, a continuación, configure la conexión con Excel.  
  
     Para obtener información sobre las opciones de configuración disponibles para este tipo de conexión, vea [Excel Connection Manager Editor](../../integration-services/connection-manager/excel-connection-manager-editor.md).  
  
## Vea también  
 [Conectarse a una base de datos de Access](../../integration-services/connection-manager/connect-to-an-access-database.md)  
  
  