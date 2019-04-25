---
title: Generar archivos de volcado para la ejecución de paquetes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 61ef1731-cb3a-4afb-b4a4-059b04aeade0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8022532dcb038b7c9a5839acb0541337ac3d5001
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62766158"
---
# <a name="generating-dump-files-for-package-execution"></a>Generar archivos de volcado para la ejecución de paquetes
  En [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], puede crear archivos de volcado de depuración que proporcionen información sobre la ejecución de un paquete. La información de estos archivos puede ayudarle a solucionar los problemas de ejecución del paquete.  
  
> [!NOTE]  
>  Los archivos de volcado de depuración podrían contener información confidencial. Para proteger la información confidencial, puede utilizar una lista de control de acceso (ACL) con objeto de restringir el acceso a los archivos o copiarlos en una carpeta con acceso restringido. Por ejemplo, antes de enviar los archivos de depuración a los servicios de soporte al cliente de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , se recomienda que quite cualquier información sensible o confidencial.  
  
 Al implementar un proyecto en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , puede crear archivos de volcado que proporcionen información sobre la ejecución de paquetes incluidos en el proyecto. Cuando finaliza el proceso de ISServerExec.exe, se crean los archivos de volcado. Puede especificar que un archivo de volcado se cree cuando aparezcan errores durante la ejecución del paquete; para ello, seleccione la opción **Volcado de errores** en el cuadro de diálogo **Ejecutar paquete** . También puede utilizar los siguientes procedimientos almacenados:  
  
-   [catalog.set_execution_parameter_value &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database)  
  
     Llame a este procedimiento almacenado para configurar un archivo de volcado que se creará cuando se produzca algún error o evento y cuando se produzcan eventos específicos durante la ejecución de un paquete.  
  
-   [catalog.create_execution_dump](/sql/integration-services/system-stored-procedures/catalog-create-execution-dump)  
  
     Llame a este procedimiento almacenado para hacer que se detenga un paquete en ejecución y crear un archivo de volcado.  
  
 Si está implementando paquetes con el modelo de implementación de paquetes, puede crear archivos de volcado de depuración mediante la utilidad **dtexec** o la utilidad **dtutil** para especificar una opción de volcado de depuración en la línea de comandos. Para obtener más información, consulte [dtexec Utility](../packages/dtexec-utility.md) y [dtutil Utility](../dtutil-utility.md). Para obtener más información acerca del modelo de implementación de paquetes, consulte [implementación de proyectos y paquetes](../packages/deploy-integration-services-ssis-projects-and-packages.md) y [la implementación del paquete &#40;SSIS&#41;](../packages/legacy-package-deployment-ssis.md).  
  
## <a name="debug-dump-file-format"></a>Formato de los archivos de volcado de depuración  
 Cuando se especifica una opción de volcado de depuración, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea los archivos de volcado de depuración siguientes:  
  
-   Un archivo de volcado de depuración .mdmp. Es un archivo binario.  
  
-   El archivo de volcado de depuración .tmp. Es un archivo de texto con formato.  
  
 De forma predeterminada, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] almacena estos archivos en la carpeta *\<unidad>:* \Archivos de programa\Microsoft SQL Server\110\Shared\ErrorDumps.  
  
 En la tabla siguiente solo se describen determinadas secciones del archivo .tmp. El archivo .tmp incluye datos adicionales que no se incluyen en la tabla.  
  
|Tipo de información|Descripción|Ejemplo|  
|-------------------------|-----------------|-------------|  
|Entorno|Versión del sistema operativo, datos de uso de la memoria, identificador de proceso y nombre de imagen de proceso. La información del entorno se encuentra al principio del archivo .tmp.|# SSIS Textual Dump taken at 9/13/2007 1:50:34 PM<br /><br /> #PID 4120<br /><br /> #Image Name [C:\Program Files\Microsoft SQL Server\110\DTS\Binn\DTExec.exe]<br /><br /> # OS major=6 minor=0 build=6000<br /><br /> # Running on 2 amd64 processors under WOW64<br /><br /> # Memory: 58% in use. Physical: 845M/2044M  Paging: 2404M/4095M (avail/total)|  
|Ruta de acceso y versión de la biblioteca de vínculos dinámicos (DLL)|Ruta de acceso y número de versión de cada DLL que el sistema carga durante el procesamiento de un paquete.|# Loaded Module: c:\bb\Sql\DTS\src\bin\debug\i386\DTExec.exe (10.0.1069.5)<br /><br /> # Loaded Module: C:\Windows\SysWOW64\ntdll.dll (6.0.6000.16386)<br /><br /> # Loaded Module: C:\Windows\syswow64\kernel32.dll (6.0.6000.16386)|  
|Mensajes recientes|Mensajes recientes emitidos por el sistema. Incluye la fecha y hora, el tipo, la descripción y el identificador de subproceso de cada mensaje.|[M:1]   Ring buffer entry:              (*pRecord)<br /><br /> [D:2]      <<\<CRingBufferLogging::RingBufferLoggingRecord>>> ( \@ 0282F1A8 )<br /><br /> [E:3]         Time Stamp: 2007-09-13 13:50:32.786      (szTimeStamp)<br /><br /> [E:3]         Thread ID: 2368           (ThreadID)<br /><br /> [E:3]         Event Name: OnError                        (EventName)<br /><br /> [E:3]         Source Name:                (SourceName)<br /><br /> [E:3]         Source ID:                        (SourceID)<br /><br /> [E:3]         Execution ID:                 (ExecutionGUID)<br /><br /> [E:3]         Data Code: -1073446879              (DataCode)<br /><br /> [E:3]         Description: Falta el componente, no está registrado, no puede actualizarse o faltan interfaces necesarias. La información de contacto para este componente es "".|  
  
## <a name="related-content"></a>Contenido relacionado  
 [Ejecutar paquete (cuadro de diálogo)](../execute-package-dialog-box.md)  
  
  
