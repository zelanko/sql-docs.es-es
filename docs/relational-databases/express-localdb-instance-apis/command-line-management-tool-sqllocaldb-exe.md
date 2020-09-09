---
description: 'Herramienta de administración de la línea de comandos: SqlLocalDB.exe'
title: 'Herramienta de administración de la línea de comandos: SqlLocalDB.exe | Microsoft Docs'
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apilocation:
- sqluserinstance.dll
ms.assetid: dd0882b1-a8a9-447a-8bdf-0f9d7f36d336
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4b2140dc74bd9e30bb4c707681aa9b491f8ea272
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548903"
---
# <a name="command-line-management-tool-sqllocaldbexe"></a>Herramienta de administración de la línea de comandos: SqlLocalDB.exe
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  SqlLocalDB.exe es una sencilla herramienta que permite al usuario administrar con facilidad instancias de LocalDB desde la línea de comandos. Se implementa como un contenedor simple en la API de instancia de LocalDB. Como en numerosas herramientas de SQL Server similares (por ejemplo, SQLCMD), los parámetros se pasan a SqlLocalDB como argumentos de la línea de comandos y la salida se envía a la consola.  
  
 SqlLocalDB permite a los desarrolladores de software usar LocalDB sin tener que escribir código para llamar a la API o sin depender en otras herramientas para que hagan el trabajo por ellos.  
  
## <a name="sqllocaldb-options"></a>Opciones de SqlLocalDB  
 SqlLocalDB admite las opciones siguientes.  
  
|Opción|Qué hace|  
|------------|------------------|  
|`-?`|Imprime texto de ayuda.|  
|`create\|c "instance name" [version-number] [-s]`|Crea una instancia de LocalDB con un nombre y una versión determinados.<br /><br /> Si se omite el parámetro [versión-número], toma el valor predeterminado de la versión de compilación de SqlLocalDB.<br /><br /> -s inicia la nueva instancia de LocalDB una vez se haya creado.|  
|`delete\|d "instance name"`|Elimina la instancia de LocalDB con el nombre especificado.|  
|`start\|s "instance name"`|Inicia la instancia de LocalDB con el nombre especificado.|  
|`stop\|p "instance name" [-i\|-k]`|Detiene la instancia de LocalDB con el nombre especificado, cuando las consultas actuales terminan de ejecutarse.<br /><br /> -i solicita el cierre de la instancia de LocalDB con la opción de NOWAIT.<br /><br /> -k elimina el proceso de la instancia de LocalDB sin ponerse en contacto con ella.|  
|`share\|h ["owner SID or account"] "private name" "shared name"`|Comparte la instancia privada especificada con el nombre compartido especificado. Si se omite el SID del usuario o el nombre de la cuenta, usa de forma predeterminada el usuario actual.|  
|`unshare\|u "shared name"`|No comparte la instancia compartida de LocalDB especificada.|  
|`info\|i`|Enumera todas las instancias existentes de LocalDB que son propiedad del usuario actual y todas las instancias de LocalDB compartidas.|  
|`info\|i "instance name"`|Imprime información sobre la instancia de LocalDB especificada.|  
|`versions\|v`|Enumera todas las versiones de LocalDB que se hayan instalado en el equipo.|  
|||  
|`trace\|t on\|off`|Activa y desactiva el seguimiento.|  
  
 SqlLocalDB trata los espacios como delimitadores; debe escribir entre comillas los nombres de instancia que contienen espacios y caracteres especiales. Por ejemplo:  
  
 `SqlLocalDB create "My instance name with spaces"`  
  
  
