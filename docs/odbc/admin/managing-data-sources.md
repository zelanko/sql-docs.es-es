---
title: Administrar orígenes de datos | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307216"
---
# <a name="managing-data-sources"></a>Administrar orígenes de datos
Después de instalar un controlador ODBC desde el programa de instalación del controlador, puede definir uno o varios orígenes de datos para él. El nombre del origen de datos (DSN) debe proporcionar una descripción única de los datos. por ejemplo, *Payroll* o *Accounts Payable*. Los orígenes de datos de usuario y del sistema definidos para todos los controladores instalados actualmente se muestran en las fichas **DSN de usuario** o **DSN de sistema** del cuadro de diálogo Administrador de **orígenes de datos ODBC** . Los orígenes de datos de archivo de un directorio determinado se muestran en la pestaña **DSN de archivo** ; el directorio que se va a mostrar se escribe en el cuadro **Buscar en** de la pestaña **DSN de archivo** .  
  
> [!NOTE]  
>  Para administrar un origen de datos que se conecta a un controlador de 32 bits en una plataforma de 64 bits, use c:\windows\sysWOW64\odbcad32.exe. Para administrar un origen de datos que se conecta a un controlador de 64 bits, use c:\windows\system32\odbcad32.exe. En **herramientas administrativas** en un sistema operativo Windows 8 de 64 bits, existen iconos para el cuadro de diálogo **Administrador de orígenes de datos ODBC** de 32 bits y de 64 bits.  
  
 Si usa el odbcad32. exe de 64 bits para configurar o quitar un DSN que se conecta a un controlador de 32 bits, por ejemplo, el **controlador haga Microsoft Access\*(. mdb)**, recibirá el mensaje de error siguiente:  
  
```  
The specified DSN contains an architecture mismatch between the Driver and Application  
```  
  
 Para resolver este error, use 32-bit odbcad32. exe para configurar o quitar el DSN.  
  
 Un origen de datos asocia un controlador ODBC determinado a los datos a los que desea obtener acceso a través de ese controlador. Por ejemplo, puede crear un origen de datos para utilizar el controlador ODBC dBASE con el fin de obtener acceso a uno o varios archivos dBASE que se encuentran en un directorio específico del disco duro o de una unidad de red. Con el administrador de orígenes de datos ODBC, puede Agregar, modificar y eliminar orígenes de datos, como se describe en la tabla siguiente.  
  
|Acción|Descripción|  
|------------|-----------------|  
|Cargar orígenes de datos|Es posible agregar varios orígenes de datos, cada uno de los cuales asocia un controlador con algunos datos a los que desea obtener acceso mediante ese controlador. Asigne a cada origen de datos un nombre que identifique de forma única a ese origen de datos. Por ejemplo, si crea un origen de datos para un conjunto de archivos dBASE que contienen información del cliente, podría asignar el nombre "Customers" al origen de datos. Normalmente, las aplicaciones muestran nombres de orígenes de datos para que los usuarios puedan elegir.<br /><br /> Agregar un origen de datos de archivo es ligeramente diferente de agregar orígenes de datos de usuario o del sistema. Para obtener más información, vea el archivo de ayuda del administrador de orígenes de datos ODBC.|  
|Modificar orígenes de datos|En función de sus requisitos, puede que sea necesario volver a configurar los orígenes de datos. Puede restablecer opciones haciendo clic en **configurar** en el cuadro de diálogo Configuración de cualquier controlador.|  
|Eliminar orígenes de datos|Haga clic en **quitar** después de seleccionar un origen de datos.|  
  
 Para obtener más información acerca de los orígenes de datos de archivo, vea [conectarse con orígenes de datos de archivo](../../odbc/reference/develop-app/connecting-using-file-data-sources.md) o la [función SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="see-also"></a>Consulte también  
 [Administrador de orígenes de datos ODBC](../../odbc/admin/odbc-data-source-administrator.md)
