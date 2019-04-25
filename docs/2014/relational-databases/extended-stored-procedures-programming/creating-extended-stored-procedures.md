---
title: Crear procedimientos almacenados extendidos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- warnings [SQL Server]
- extended stored procedures [SQL Server], debugging
- extended stored procedures [SQL Server], creating
- messages [SQL Server], extended stored procedures
ms.assetid: 9f7c0cdb-6d88-44c0-b049-29953ae75717
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0d0343113b350c48cbc42ec5b79bbd0b849f2860
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62512639"
---
# <a name="creating-extended-stored-procedures"></a>Crear procedimientos almacenados extendidos
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] En su lugar, utilice la integración con CLR.  
  
 Un procedimiento almacenado extendido es una función con un prototipo:  
  
 SRVRETCODE *xp_extendedProcName* **(** SRVPROC **\*);**  
  
 El uso del prefijo xp_ es opcional. Los nombres de procedimiento almacenado extendido distinguen mayúsculas de minúsculas cuando se hace referencia a ellos en instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)], independientemente de la página de códigos o criterio de ordenación que se haya instalado en el servidor. Cuando genere un archivo DLL:  
  
-   Si se necesita un punto de entrada, escriba una función DllMain.  
  
     Esta función es opcional; si no se proporciona en código fuente, el compilador vincula su propia versión, que solo devuelve TRUE. Si se proporciona una función DllMain, el sistema operativo llama a esta función cuando se adjunta o se separa un proceso o subproceso en el archivo DLL.  
  
-   Deben exportarse todas las funciones a las que se llama desde el exterior del archivo DLL (todas las funciones Efunction de procedimiento almacenado extendido).  
  
     Puede exportar una función indicando su nombre en la sección EXPORTS de un archivo .def o se puede anteponer al nombre de función en el código fuente con __declspec (dllexport), una extensión de compilador de Microsoft (tenga en cuenta que \__declspec() comienza con dos caracteres de subrayado).  
  
 Estos archivos son necesarios para crear un archivo DLL de procedimientos almacenados extendidos.  
  
|Archivo|Descripción|  
|----------|-----------------|  
|Srv.h|Archivo de encabezado de la API Procedimiento almacenado extendido|  
|Opends60.lib|Biblioteca de importación de Opends60.dll|  
  
 Para crear un archivo DLL de procedimientos almacenados extendidos, cree un proyecto de tipo biblioteca de vínculos dinámicos. Para obtener más información sobre la forma de crear un archivo DLL, vea la documentación del entorno de desarrollo.  
  
 Se recomienda encarecidamente que todos los archivos DLL de procedimientos almacenados extendidos implementen y exporten la siguiente función:  
  
```  
__declspec(dllexport) ULONG __GetXpVersion()  
{  
   return ODS_VERSION;  
}  
```  
  
> [!NOTE]  
>  __declspec(dllexport) es una extensión de compilador específica de Microsoft. Si el compilador no admite esta directiva, debe exportar esta función en el archivo DEF, bajo la sección EXPORTS.  
  
 Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se inicia con el seguimiento de la marca - T260 o si un usuario con privilegios de administrador del sistema ejecuta DBCC TRACEON (260) y almacena extendido DLL de procedimiento no admite __GetXpVersion (), un mensaje de advertencia (Error 8131: Procedimiento almacenado extendido '%' DLL no exporta \__GetXpVersion().) se imprime en el registro de errores. (Tenga en cuenta que \__GetXpVersion() comienza con dos caracteres de subrayado.)  
  
 Si el archivo DLL de procedimientos almacenados extendidos exporta __GetXpVersion() pero la versión devuelta por la función es menor que la que requiere el servidor, en el registro de errores se imprime un mensaje de advertencia que indica la versión devuelta por la función y la versión esperada por el servidor. Si recibe este mensaje, se devuelve un valor incorrecto de \__GetXpVersion(), o bien se compila con una versión anterior de srv.h.  
  
> [!NOTE]  
>  No debe llamarse a SetErrorMode, una función Win32 de [!INCLUDE[msCoName](../../includes/msconame-md.md)], en procedimientos almacenados extendidos.  
  
 Se recomienda que un procedimiento almacenado extendido de ejecución prolongada llame periódicamente a srv_got_attention para que el procedimiento pueda finalizarse si se elimina la conexión o se anula el lote.  
  
 Para depurar un archivo DLL de procedimientos almacenados extendidos, cópielo en el directorio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Binn. Para especificar el archivo ejecutable para la sesión de depuración, escriba la ruta de acceso y el nombre de la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] archivo ejecutable (por ejemplo, C:\Program Files\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL\Binn\Sqlservr.exe). Para obtener información acerca de los argumentos de sqlservr, vea [sqlservr (aplicación)](../../tools/sqlservr-application.md).  
  
## <a name="see-also"></a>Vea también  
 [srv_got_attention &#40;API procedimiento almacenado extendido&#41;](../extended-stored-procedures-reference/srv-got-attention-extended-stored-procedure-api.md)  
  
  
