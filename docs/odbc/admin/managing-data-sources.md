---
title: Gestión de orígenes de datos ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- deleting data sources [ODBC], ODBC data source administrator
- data sources [ODBC], ODBC data source administrator
- adding data sources [ODBC], ODBC data source administrator
- removing data sources [ODBC], ODBC data source administrator
- ODBC data source administrator [ODBC], data source management
ms.assetid: 67cc4945-4850-4eb4-8da6-b835ddaeca4c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5069ac9a5babc3071c52d73d5b56b21729a5d8a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307216"
---
# <a name="managing-data-sources"></a>Administrar orígenes de datos
Después de instalar un controlador ODBC desde el programa de instalación del controlador, puede definir uno o varios orígenes de datos para él. El nombre del origen de datos (DSN) debe proporcionar una descripción única de los datos; por ejemplo, *Nómina* o *Proveedores*. Los orígenes de datos de usuario y del sistema que se definen para todos los controladores instalados actualmente se enumeran en las fichas **DSN de** usuario o **DSN** del sistema del cuadro de diálogo Administrador de orígenes de **datos ODBC.** Los orígenes de datos de archivo de un directorio determinado se enumeran en la pestaña **DSN** de archivo; el directorio que se mostrará se introduce en el cuadro **Buscar en** de la ficha **DSN** de archivo.  
  
> [!NOTE]  
>  Para administrar un origen de datos que se conecta a un controlador de 32 bits en la plataforma de 64 bits, utilice c:-windows-sysWOW64-odbcad32.exe. Para administrar un origen de datos que se conecta a un controlador de 64 bits, utilice c:-windows-system32-odbcad32.exe. En **Herramientas administrativas** en un sistema operativo Windows 8 de 64 bits, hay iconos para el cuadro de diálogo Administrador de **orígenes** de datos ODBC de 32 y 64 bits.  
  
 Si utiliza el archivo odbcad32.exe de 64 bits para configurar o quitar un DSN que se conecta a un controlador de 32 bits, por ejemplo, **Driver do Microsoft Access (\*.mdb),** recibirá el siguiente mensaje de error:  
  
```  
The specified DSN contains an architecture mismatch between the Driver and Application  
```  
  
 Para resolver este error, utilice odbcad32.exe de 32 bits para configurar o quitar el DSN.  
  
 Un origen de datos asocia un controlador ODBC determinado con los datos a los que desea tener acceso a través de ese controlador. Por ejemplo, puede crear un origen de datos para utilizar el controlador ODBC dBASE para tener acceso a uno o varios archivos dBASE que se encuentran en un directorio específico del disco duro o de una unidad de red. Con el Administrador de orígenes de datos ODBC, puede agregar, modificar y eliminar orígenes de datos, como se describe en la tabla siguiente.  
  
|Acción|Descripción|  
|------------|-----------------|  
|Cargar orígenes de datos|Es posible agregar varios orígenes de datos, cada uno de los que asocia un controlador con algunos datos a los que desea tener acceso mediante ese controlador. Asigne a cada origen de datos un nombre que identifique de forma única ese origen de datos. Por ejemplo, si crea un origen de datos para un conjunto de archivos dBASE que contienen información del cliente, podría asignar al origen de datos el nombre "Clientes". Las aplicaciones suelen mostrar nombres de origen de datos para que los usuarios elijan.<br /><br /> Agregar un origen de datos de archivo es ligeramente diferente de agregar orígenes de datos de usuario o del sistema. Para obtener más información, consulte el archivo de ayuda Administrador de orígenes de datos ODBC.|  
|Modificación de fuentes de datos|En función de sus requisitos, es posible que sea necesario volver a configurar los orígenes de datos. Puede restablecer las opciones haciendo clic en **Configurar** en cualquier cuadro de diálogo de configuración del controlador.|  
|Eliminación de orígenes de datos|Haga clic en **Quitar** después de seleccionar un origen de datos.|  
  
 Para obtener más información acerca de los orígenes de datos de archivo, vea Conexión mediante [orígenes](../../odbc/reference/develop-app/connecting-using-file-data-sources.md) de datos de archivo o la [función SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="see-also"></a>Consulte también  
 [Administrador de orígenes de datos ODBC](../../odbc/admin/odbc-data-source-administrator.md)
