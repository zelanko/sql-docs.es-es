---
title: Extensión SQL Server Profiler
description: Aprenda a instalar y usar la extensión SQL Server Profiler (versión preliminar), una solución de seguimiento de SQL Server fácil de usar similar a SSMS Profiler.
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu, maghan, sstein
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: e6e71f00748fa9d0fc4b803d8268d8a8b23284fc
ms.sourcegitcommit: 7035d9471876c70b99c58bf9b46af5cce6e9c66c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2020
ms.locfileid: "87522449"
---
# <a name="sql-server-profiler-extension-preview"></a>Extensión SQL Server Profiler (versión preliminar)

La extensión SQL Server Profiler (versión preliminar) proporciona una sencilla solución de seguimiento de SQL Server similar a SQL Server Management Studio (SSMS) Profiler, aunque se compila mediante Eventos extendidos. SQL Server Profiler es muy fácil de usar y tiene buenos valores predeterminados para las configuraciones de seguimiento más comunes. La experiencia de usuario está optimizada para examinar eventos y ver el texto de Transact-SQL (T-SQL) asociado. SQL Server Profiler para Azure Data Studio también supone buenos valores predeterminados para recopilar actividades de ejecución de T-SQL con una experiencia de usuario fácil de usar. Esta extensión está actualmente en versión preliminar.

**Casos de uso comunes de SQL Profiler:**

- Seguir los pasos de consultas con problemas para buscar la causa de los mismos.
- Buscar y diagnosticar consultas de ejecución lenta.
- Capturar la serie de instrucciones de Transact-SQL que ha causado un problema.
- Supervisar el rendimiento de SQL Server para optimizar cargas de trabajo.
- Establecer correlaciones entre contadores de rendimiento para diagnosticar problemas.


## <a name="install-the-sql-server-profiler-extension"></a>Instalar la extensión SQL Server Profiler

1. Para abrir el administrador de extensiones y acceder a las extensiones disponibles, seleccione el icono de extensiones, o bien seleccione **Extensiones** en el menú **Ver**.
2. Seleccione una extensión disponible para ver sus detalles.

   ![Administrador de extensiones de Profiler](media/extensions/sql-server-profiler-extension/profiler-extension.png)

1. Seleccione la extensión que quiera e **instálela**.
2. Seleccione **Recargar** para habilitar la extensión (solo es necesario la primera vez que se instala una extensión).

## <a name="start-profiler"></a>Inicio de Profiler

1. Para iniciar Profiler, primero establezca una conexión con un servidor en la pestaña Servidores.
2. Después de establecer una conexión, escriba **Alt + P** para iniciar Profiler.
3. Para iniciar Profiler, escriba **Alt + S**. Ahora puede empezar a ver eventos extendidos.
    ![Administrador de extensiones de Profiler](media/extensions/sql-server-profiler-extension/view-profiler.png)    
1. Para detener Profiler, escriba **Alt + S**. Este atajo de teclado sirve para la alternancia.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre Profiler y los eventos extendidos, vea [Eventos extendidos](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events).





