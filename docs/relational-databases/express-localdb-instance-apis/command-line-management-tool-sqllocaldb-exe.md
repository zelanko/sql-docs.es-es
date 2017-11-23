---
title: "Herramienta de administración de línea de comandos: SqlLocalDB.exe | Documentos de Microsoft"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: localdb
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apilocation: sqluserinstance.dll
ms.assetid: dd0882b1-a8a9-447a-8bdf-0f9d7f36d336
caps.latest.revision: "9"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 8f2bac1f105f5d299fa97d11fa579226026134aa
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="command-line-management-tool-sqllocaldbexe"></a>Herramienta de administración de la línea de comandos: SqlLocalDB.exe
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]SqlLocalDB.exe es una sencilla herramienta que permite al usuario administrar fácilmente las instancias de LocalDB desde la línea de comandos. Se implementa como un contenedor simple en la API de instancia de LocalDB. Como en numerosas herramientas de SQL Server similares (por ejemplo, SQLCMD), los parámetros se pasan a SqlLocalDB como argumentos de la línea de comandos y la salida se envía a la consola.  
  
 SqlLocalDB permite a los desarrolladores de software usar LocalDB sin tener que escribir código para llamar a la API o sin depender en otras herramientas para que hagan el trabajo por ellos.  
  
## <a name="sqllocaldb-options"></a>Opciones de SqlLocalDB  
 SqlLocalDB admite las opciones siguientes.  
  
|Opción|Lo que hace|  
|------------|------------------|  
|`-?`|Imprime texto de ayuda.|  
|' create\|c "nombre de la instancia" [número de versión] [-s]'|Crea una instancia de LocalDB con un nombre y una versión determinados.<br /><br /> Si se omite el parámetro [versión-número], toma el valor predeterminado de la versión de compilación de SqlLocalDB.<br /><br /> -s inicia la nueva instancia de LocalDB una vez se haya creado.|  
|' delete\|d. "nombre de la instancia" '|Elimina la instancia de LocalDB con el nombre especificado.|  
|' inicio|"nombre de la instancia" s "|Inicia la instancia de LocalDB con el nombre especificado.|  
|' Stop|"nombre de instancia" p [-i\|-k]'|Detiene la instancia de LocalDB con el nombre especificado, cuando las consultas actuales terminan de ejecutarse.<br /><br /> -i solicita el cierre de la instancia de LocalDB con la opción de NOWAIT.<br /><br /> -k elimina el proceso de la instancia de LocalDB sin ponerse en contacto con ella.|  
|' share\|h ["SID de propietario o cuenta"] "privada""compartido nombre" '|Comparte la instancia privada especificada con el nombre compartido especificado. Si se omite el SID del usuario o el nombre de la cuenta, usa de forma predeterminada el usuario actual.|  
|' unshare\|u "nombre de recurso compartido" '|No comparte la instancia compartida de LocalDB especificada.|  
|' info\|'|Enumera todas las instancias existentes de LocalDB que son propiedad del usuario actual y todas las instancias de LocalDB compartidas.|  
|' info\|'nombre de la instancia"i'|Imprime información sobre la instancia de LocalDB especificada.|  
|' versions\|v'|Enumera todas las versiones de LocalDB que se hayan instalado en el equipo.|  
|||  
|' trace\|t on\|desactivar '|Activa y desactiva el seguimiento.|  
  
 SqlLocalDB trata los espacios como delimitadores; debe escribir entre comillas los nombres de instancia que contienen espacios y caracteres especiales. Por ejemplo:  
  
 `SqlLocalDB create "My instance name with spaces"`  
  
  
