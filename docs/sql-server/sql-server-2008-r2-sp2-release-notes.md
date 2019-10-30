---
title: Notas de la versión de SQL Server 2008 R2 SP2 | Microsoft Docs
ms.prod: sql
ms.technology: install
ms.custom: ''
ms.date: 10/15/2019
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server 2008 R2 SP2
- Release Notes, SQL Server 2008 R2 SP2
ms.assetid: e2bd3de7-674c-4ea7-8d53-bb40bba86fae
author: craigg-msft
ms.author: craigg
monikerRange: = sql-server-2014 || = sqlallproducts-allversions
ms.openlocfilehash: 61afc55e04f7cd317e11c7db527dc97fb80fc7be
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2019
ms.locfileid: "72904261"
---
# <a name="sql-server-2008-r2-sp2-release-notes"></a>SQL Server 2008 R2 SP2 Release Notes
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
En estas Notas de la versión se describen los problemas conocidos con los que debe familiarizarse antes de instalar o de solucionar problemas de Microsoft SQL Server 2008 R2 Service Pack 2. Este documento se aplica a todas las ediciones de SQL Server 2008 R2 SP2 y solamente está disponible en línea. Se actualiza periódicamente.  
  
## <a name="10-whats-new-in-service-pack-2"></a>1.0 Novedades del Service Pack 2  
Se ha agregado la vista de administración dinámica (DMV) **sys.dm_db_stats_properties**. Puede usar esta DMV con el fin de devolver propiedades de estadísticas para un tabla o vista indizada determinadas en la base de datos actual. Por ejemplo, esta DMV devuelve el número de filas que se muestrearon y el número de pasos del histograma.  
  
## <a name="20-before-you-install"></a>2.0 Antes de la instalación  
Para obtener información acerca de cómo instalar las actualizaciones de [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] , vea [Documentación de mantenimiento de SQL Server 2008 R2](https://msdn.microsoft.com/library/dd638062(SQL.105).aspx).  
  
Para obtener una introducción e información acerca de cómo instalar SQL Server 2008 R2, vea el documento Léame de SQL Server 2008 R2. El documento Léame está disponible en el disco de instalación. También puede encontrar más información en los [foros de SQL Server](https://social.msdn.microsoft.com/Forums/category/sqlserver/).
  
### <a name="21-choose-the-correct-file-to-download-and-install"></a>2.1 Elegir el archivo correcto para su descarga e instalación  
Use la tabla siguiente para determinar qué archivo va a descargar e instalar. Compruebe que cumple los requisitos del sistema correctos antes de instalar el Service Pack. Los requisitos del sistema se proporcionan en las páginas de descarga cuyos vínculos aparecen en la tabla.  
  
|Si la versión que tiene instalada actualmente es...|Y desea...|Descargue e instale...|  
|-------------------------------------------|----------------------|---------------------------|  
|Una versión de 32 bits de cualquier edición de SQL Server 2008 R2 o SQL Server 2008 R2 SP1|Actualizar a la versión de 32 bits de SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x86-ENU desde [aquí](https://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|Una versión de 32 bits de cualquier edición de 2008 R2 RTM Express o SQL Server 2008 R2 SP1 Express|Actualizar a la versión de 32 bits de SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x86-ENU.exe desde [aquí](https://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|Una versión de 32 bits únicamente del cliente y de las herramientas de administración para SQL Server 2008 R2 o SQL Server 2008 R2 SP1 (lo cual incluye SQL Server 2008 R2 Management Studio)|Actualizar el cliente y herramientas de administración a la versión de 32 bits de SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x86-ENU.exe desde [aquí](https://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|Una versión de 32 bits de SQL Server 2008 R2 Management Studio Express o SQL Server 2008 R2 SP1 Management Studio Express|Actualizar a la versión de 32 bits de SQL Server 2008 R2 SP2 Management Studio Express|SQLManagementStudio_x86_ENU.exe desde [aquí](https://go.microsoft.com/fwlink/p/?LinkId=251791)|  
|Una versión de 32 bits de cualquier edición de SQL Server 2008 R2 o SQL Server 2008 R2 SP1 **y** una versión de 32 bits del cliente y herramientas de administración (lo cual incluye SQL Server 2008 R2 RTM Management Studio)|Actualizar todos los productos a la versión de 32 bits de SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x86-ENU.exe desde [aquí](https://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|Una versión de 32 bits de una o más herramientas del [Microsoft SQL Server 2008 R2 RTM Feature Pack](https://www.microsoft.com/download/en/details.aspx?id=16978)|Actualizar las herramientas a la versión del Microsoft SQL Server 2008 R2 SP2 Feature Pack|Uno o más archivos del [Microsoft SQL Server 2008 R2 SP2 Feature Pack](https://go.microsoft.com/fwlink/?LinkId=251792)|  
|No instalar la versión de 32 bits de SQL Server 2008 R2|Instalar Server 2008 R2 junto con el SP2|Vaya a [SQL Server 2008 R2 SP2 - Express Edition](https://go.microsoft.com/fwlink/?LinkId=251791) y siga las instrucciones.|  
|No instalar la versión de 32 bits de SQL Server 2008 R2 Management Studio|Instalar SQL Server 2008 R2 Management Studio junto con el SP2|SQLManagementStudio_x86_ENU.exe desde [aquí](https://go.microsoft.com/fwlink/p/?LinkId=251791) para instalar SQL Server 2008 R2 SP2 Management Studio Express Edition de forma gratuita.|  
|Una versión de 64 bits de cualquier edición de SQL Server 2008 R2 o SQL Server 2008 R2 SP1|Actualizar a la versión de 64 bits de SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x64-ENU o SQLServer2008R2SP2-KB2630455-IA64-ENU.exe desde [aquí](https://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|Una versión de 64 bits de cualquier edición de 2008 R2 RTM Express o SQL Server 2008 R2 SP1 Express|Actualizar a la versión de 64 bits de SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x64-ENU.exe o SQLServer2008R2SP2-KB2630455-IA64-ENU.exe desde [aquí](https://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|Una versión de 64 bits únicamente del cliente y de las herramientas de administración para SQL Server 2008 R2 o SQL Server 2008 R2 SP1 (lo cual incluye SQL Server 2008 R2 Management Studio)|Actualizar el cliente y herramientas de administración a la versión de 64 bits de SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x64-ENU.exe o SQLServer2008R2SP2-KB2630455-IA64-ENU.exe desde [aquí](https://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|Una versión de 64 bits de SQL Server 2008 R2 Management Studio Express o SQL Server 2008 R2 SP1 Management Studio Express|Actualizar a la versión de 64 bits de SQL Server 2008 R2 SP2 Management Studio Express|SQLManagementStudio_x64_ENU.exe desde [aquí](https://go.microsoft.com/fwlink/p/?LinkId=251791)|  
|Una versión de 64 bits de cualquier edición de SQL Server 2008 R2 o SQL Server 2008 R2 SP1 **y** una versión de 64 bits del cliente y herramientas de administración (lo cual incluye SQL Server 2008 R2 RTM Management Studio)|Actualizar todos los productos a la versión de 64 bits de SQL Server 2008 R2 SP2|SQLServer2008R2SP2-KB2630458-x64-ENU.exe desde [aquí](https://go.microsoft.com/fwlink/p/?LinkId=251790)|  
|Una versión de 64 bits de una o más herramientas del [Microsoft SQL Server 2008 R2 RTM Feature Pack](https://www.microsoft.com/download/en/details.aspx?id=16978)|Actualizar las herramientas a la versión de 64 bits del Microsoft SQL Server 2008 R2 SP2 Feature Pack|Uno o más archivos del [Microsoft SQL Server 2008 R2 SP2 Feature Pack](https://go.microsoft.com/fwlink/?LinkId=251792)|  
|No instalar la versión de 64 bits de SQL Server 2008 R2|Instalar Server 2008 R2 junto con el SP2|Vaya a [SQL Server 2008 R2 SP2 - Express Edition](https://go.microsoft.com/fwlink/?LinkId=251791) y siga las instrucciones.|  
|No instalar la versión de 64 bits de SQL Server 2008 R2 Management Studio|Instalar SQL Server 2008 R2 Management Studio junto con el SP2|SQLManagementStudio_x64_ENU.exe desde [aquí](https://go.microsoft.com/fwlink/p/?LinkId=251791) para instalar SQL Server 2008 R2 SP2 Management Studio Express Edition de forma gratuita.|  
  
### <a name="22-setup-might-fail-if-sqagtresdll-is-locked-by-another-process"></a>2.2 Posibles errores en el programa de instalación si otro proceso ha bloqueado SQAGTRES.dll  
**Problema:** Es posible que se produzca el siguiente error en una operación del programa de instalación de SQL Server: `Upgrading of cluster resource C:\Program Files\Microsoft SQL Server\MSSQL10_50.<Instance name>\MSSQL\Binn\SQAGTRES.DLL on machine <Computer name> failed with Win32Exception. Please look at inner exception for details.` La causa raíz es que otro proceso ha bloqueado C:\Windows\system32\SQAGTRES.DLL y el programa de instalación no ha podido actualizarlo.  
  
**Solución**: cambie el nombre de C:\Windows\system32\SQAGTRES.DLL a uno temporal como C:\Windows\system32\SQAGTRES_antiguo.DLL y, después, seleccione la opción Reintentar en el mensaje de error de la instalación. De esta forma el programa de instalación podrá continuar. Después de reiniciar, podrá eliminar el archivo temporal C:\Windows\system32\SQAGTRES_antiguo.DLL.  
  
## <a name="30-known-issues-fixed-in-this-service-pack"></a>3.0 Problemas conocidos corregidos en este Service Pack  
Para obtener una lista completa de errores y de problemas conocidos corregidos en este Service Pack, vea este [artículo maestro de KB](https://support.microsoft.com/kb/2630455).  
  
## <a name="see-also"></a>Consulte también  
[Cómo determinar la versión y la edición de SQL Server](https://support.microsoft.com/kb/321185)  
  
