---
title: default trace enabled (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], traces
- traces [SQL Server], logs
- default trace enabled option
ms.assetid: 1322d668-44f4-469e-8fd6-e0d02a81c8f2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d5e85a3685804fa834c9a92887a46c72b7cb69a7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62811320"
---
# <a name="default-trace-enabled-server-configuration-option"></a>default trace enabled (opción de configuración del servidor)
  Utilice la opción **default trace enabled** para habilitar o deshabilitar los archivos predeterminados de registro de seguimiento. La funcionalidad de registro de seguimiento predeterminado ofrece un registro completo y persistente de la actividad y los cambios principalmente relacionados con las opciones de configuración.  
  
> [!WARNING]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use eventos extendidos en su lugar.  
  
## <a name="purpose"></a>Finalidad  
 Los seguimientos predeterminados ofrecen ayuda para la solución de problemas a los administradores de bases de datos al garantizar que disponen de los datos de registro necesarios para diagnosticar los problemas la primera vez que ocurren.  
  
## <a name="viewing"></a>Ver  
 Los registros de seguimiento predeterminados se pueden abrir y examinar mediante [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] o se pueden consultar a través de [!INCLUDE[tsql](../../includes/tsql-md.md)] utilizando la función de sistema `fn_trace_gettable` . [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] puede abrir los archivos de registro de seguimiento predeterminados igual que si fueran archivos de salida de seguimiento normales. Los registros de seguimiento predeterminados se almacenan de forma predeterminada en el directorio `\MSSQL\LOG` mediante un archivo de seguimiento de sustitución. El nombre base del archivo predeterminado de registro de seguimiento es `log.trc`. En una instalación estándar de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el seguimiento predeterminado está habilitado y se transforma por tanto en TraceID 1. Si se habilita después de la instalación y después de crear otros seguimientos, el TraceID puede adoptar un número mayor.  
  
 Para obtener más información sobre el uso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler para ver este archivo de seguimiento, vea [Abrir un archivo de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)  
  
### <a name="example"></a>Ejemplo:  
 La instrucción siguiente abre el registro de seguimiento predeterminado en la ubicación predeterminada:  
  
```  
SELECT *   
FROM fn_trace_gettable  
('C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\LOG\log.trc', default);  
GO  
  
```  
  
## <a name="configuring"></a>Configuración  
 Si se selecciona el valor 1 para la opción **default trace enabled** , se habilita **Default Trace**. El valor predeterminado de esta opción es 1 (ON). El valor 0 desactiva el seguimiento.  
  
 **default trace enabled** es una opción avanzada. Si está usando el procedimiento almacenado del sistema **sp_configure** para cambiar la configuración, solo podrá cambiar la opción **Seguimiento predeterminado habilitado** cuando **Mostrar opciones avanzadas** esté configurado en 1. La configuración surte efecto inmediatamente, sin necesidad de reiniciar un servidor.  
  
## <a name="see-also"></a>Vea también  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
