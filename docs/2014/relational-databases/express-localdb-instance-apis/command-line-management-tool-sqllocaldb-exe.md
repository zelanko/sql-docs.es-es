---
title: 'Herramienta de administración de línea de comandos: SqlLocalDB.exe | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_location:
- sqluserinstance.dll
ms.assetid: dd0882b1-a8a9-447a-8bdf-0f9d7f36d336
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 58ea983555fdcb4bb177813db88d40f4bcc59c0e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52765477"
---
# <a name="command-line-management-tool-sqllocaldbexe"></a>Herramienta de administración de línea de comandos: SqlLocalDB.exe
  SqlLocalDB.exe es una sencilla herramienta que permite al usuario administrar con facilidad instancias de LocalDB desde la línea de comandos. Se implementa como un contenedor simple en la API de instancia de LocalDB. Como en numerosas herramientas de SQL Server similares (por ejemplo, SQLCMD), los parámetros se pasan a SqlLocalDB como argumentos de la línea de comandos y la salida se envía a la consola.  
  
 SqlLocalDB permite a los desarrolladores de software usar LocalDB sin tener que escribir código para llamar a la API o sin depender en otras herramientas para que hagan el trabajo por ellos.  
  
## <a name="sqllocaldb-options"></a>Opciones de SqlLocalDB  
 SqlLocalDB admite las opciones siguientes.  
  
|Opción|Lo que hace|  
|------------|------------------|  
|`-?`|Imprime texto de ayuda.|  
|`create&#124;c "instance name" [version-number] [-s]`|Crea una instancia de LocalDB con un nombre y una versión determinados.<br /><br /> Si se omite el parámetro [versión-número], toma el valor predeterminado de la versión de compilación de SqlLocalDB.<br /><br /> -s inicia la nueva instancia de LocalDB una vez se haya creado.|  
|`delete&#124;d "instance name"`|Elimina la instancia de LocalDB con el nombre especificado.|  
|`start&#124;s "instance name"`|Inicia la instancia de LocalDB con el nombre especificado.|  
|`stop&#124;p "instance name" [-i&#124;-k]`|Detiene la instancia de LocalDB con el nombre especificado, cuando las consultas actuales terminan de ejecutarse.<br /><br /> -i solicita el cierre de la instancia de LocalDB con la opción de NOWAIT.<br /><br /> -k elimina el proceso de la instancia de LocalDB sin ponerse en contacto con ella.|  
|`share&#124;h ["owner SID or account"] "private name" "shared name"`|Comparte la instancia privada especificada con el nombre compartido especificado. Si se omite el SID del usuario o el nombre de la cuenta, usa de forma predeterminada el usuario actual.|  
|`unshare&#124;u "shared name"`|No comparte la instancia compartida de LocalDB especificada.|  
|`info&#124;i`|Enumera todas las instancias existentes de LocalDB que son propiedad del usuario actual y todas las instancias de LocalDB compartidas.|  
|`info&#124;i "instance name"`|Imprime información sobre la instancia de LocalDB especificada.|  
|`versions&#124;v`|Enumera todas las versiones de LocalDB que se hayan instalado en el equipo.|  
|||  
|`trace&#124;t on&#124;off`|Activa y desactiva el seguimiento.|  
  
 SqlLocalDB trata los espacios como delimitadores; debe escribir entre comillas los nombres de instancia que contienen espacios y caracteres especiales. Por ejemplo:  
  
 `SqlLocalDB create "My instance name with spaces"`  
  
  
